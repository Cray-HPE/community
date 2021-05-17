# Cray System Management (CSM) API Conventions and Guidelines

The conventions of the CSM API (and related APIs in the ecosystem) are intended to ease client development and ensure that configuration mechanisms can be implemented that work across a diverse set of use cases consistently.  These conventions are heavily inspired by the Kubernetes API Conventions.

The general style of the CSM API is RESTful - clients create, update, delete, or retrieve a description of an object via the standard HTTP verbs (POST, PUT, DELETE, and GET) - and those APIs preferentially accept and return JSON. CSM also allows alternative content types. All of the JSON accepted and returned by the server has a schema, identified by the "kind" and "apiVersion" fields. Where relevant HTTP header fields exist, they should mirror the content of JSON fields, but the information should not be represented only in the HTTP header.

The documentation method for CSM API behavior is an OpenAPI document.  At the time of writing, the current standard version is [3.0.2](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md).  Existing APIs that implement the earlier OpenAPI 2 or Swagger standards are acceptable and must be compliant with those standards.  Future APIs must use the current standard.  Automatic documentation and clients are generated from the OpenAPI documents.  High quality OpenAPI documents ease client development and interoperability.

- [Cray System Management (CSM) API Conventions and Guidelines](#cray-system-management-csm-api-conventions-and-guidelines)
  - [Terms](#terms)
  - [Types (Kinds)](#types-kinds)
    - [Resources](#resources)
    - [Primitive types](#primitive-types)
    - [Constants](#constants)
    - [Unions](#unions)
    - [Lists and Simple kinds](#lists-and-simple-kinds)
  - [Verbs on Resources](#verbs-on-resources)
    - [PATCH operations](#patch-operations)
    - [Idempotency](#idempotency)
  - [Serialization Format](#serialization-format)
  - [Units](#units)
  - [HTTP Status codes](#http-status-codes)
    - [Success codes](#success-codes)
    - [Error codes](#error-codes)
  - [Naming conventions](#naming-conventions)
  - [Validation](#validation)
  - [References](#external-references)

## Terms

The following terms are defined:

- **Kind** the name of a particular object schema (e.g. the "Cat" and "Dog"
kinds would have different attributes and properties)
- **Resource** a representation of a system entity, sent or retrieved as JSON
via HTTP to the server. Resources are exposed via:
  - Collections - a list of resources of the same type, which may be queryable
  - Elements - an individual resource, addressable via a URL
- **API Group** a set of resources that are exposed together, along
with the version exposed in the "apiVersion" field as "GROUP/VERSION", e.g.
"policy.cray.io/v1".
Each resource typically accepts and returns data of a single kind. A kind may be accepted or returned by multiple resources that reflect specific use cases. For instance, the kind "Pod" is exposed as a "pods" resource that allows end users to create, update, and delete pods, while a separate "pod status" resource (that acts on "Pod" kind) allows automated processes to update a subset of the fields in that resource.

Resources are bound together in API groups - each group may have one or more versions that evolve independent of other API groups, and each version within the group has one or more resources. Group names are typically in domain name form - the CSM project reserves use of the empty group, all single word names ("extensions", "apps"), and any group name ending in "*.cray.io" for its sole use. When choosing a group name, we recommend selecting a subdomain your group or organization owns, such as "widget.mycompany.com".

Resource collections should be all lowercase and plural, whereas kinds are CamelCase and singular. Group names must be lower case and be valid DNS subdomains.

## Types (Kinds)

Kinds are grouped into three categories:

1. **Objects** represent a persistent entity in the system.

   Creating an API object is a record of intent - once created, the system will
work to ensure that resource exists. All API objects have common metadata.

   An object may have multiple resources that clients can use to perform
specific actions that create, update, delete, or get.

   Examples: `Pod`, `ReplicationController`, `Service`, `Namespace`, `Node`.

2. **Lists** are collections of **resources** of one (usually) or more
(occasionally) kinds.

   The name of a list kind must end with "List". Lists have a limited set of
common metadata. All lists use the required "items" field to contain the array
of objects they return. Any kind that has the "items" field must be a list kind.

   Most objects defined in the system should have an endpoint that returns the
full set of resources, as well as zero or more endpoints that return subsets of
the full list. Some objects may be singletons (the current user, the system
defaults) and may not have lists.

   Examples: `PodList`, `ServiceList`, `NodeList`.

3. **Simple** kinds are used for specific actions on objects and for
non-persistent entities.

   Given their limited scope, they have the same set of limited common metadata
as lists.

   For instance, the "Status" kind is returned when errors occur and is not
persisted in the system.

   Many simple resources are "subresources", which are rooted at API paths of
specific resources. When resources wish to expose alternative actions or views
that are closely coupled to a single resource, they should do so using new
sub-resources. Common subresources include:

   - `/binding`: Used to bind a resource representing a user request (e.g., Pod,
PersistentVolumeClaim) to a cluster infrastructure resource (e.g., Node,
PersistentVolume).
   - `/status`: Used to write just the status portion of a resource. For
example, the `/pods` endpoint only allows updates to `metadata` and `spec`,
since those reflect end-user intent. An automated process should be able to
modify status for users to see by sending an updated Pod kind to the server to
the "/pods/&lt;name&gt;/status" endpoint - the alternate endpoint allows
different rules to be applied to the update, and access to be appropriately
restricted.
   - `/scale`: Used to read and write the count of a resource in a manner that
is independent of the specific resource schema.

The standard REST verbs (defined below) MUST return singular JSON objects. Some
API endpoints may deviate from the strict REST pattern and return resources that
are not singular JSON objects, such as streams of JSON objects or unstructured
text log data.

A common set of "meta" API objects are used across all API groups and are
thus considered part of the API group named `meta.cray.io`. These types may
evolve independent of the API group that uses them and API servers may allow
them to be addressed in their generic form. Examples are `ListOptions`,
`DeleteOptions`, `List`, `Status`, `WatchEvent`, and `Scale`. For historical
reasons these types are part of each existing API group. Generic tools like
quota, garbage collection, autoscalers, and generic clients like kubectl
leverage these types to define consistent behavior across different resource
types, like the interfaces in programming languages.

The term "kind" is reserved for these "top-level" API types. The term "type"
should be used for distinguishing sub-categories within objects or subobjects.

### Resources

All JSON objects returned by an API MUST have the following fields:

- kind: a string that identifies the schema this object should have
- apiVersion: a string that identifies the version of the schema the object
should have

These fields are required for proper decoding of the object. They may be
populated by the server by default from the specified URL path, but the client
likely needs to know the values in order to construct the URL path.

#### Primitive types

- Avoid floating-point values as much as possible, and never use them in spec.
  Floating-point values cannot be reliably round-tripped (encoded and
  re-decoded) without changing, and have varying precision and representations
  across languages and architectures.
- All numbers (e.g., uint32, int64) are converted to float64 by Javascript and
  some other languages, so any field which is expected to exceed that either in
  magnitude or in precision (specifically integer values > 53 bits) should be
  serialized and accepted as strings.
- Do not use unsigned integers, due to inconsistent support across languages and
  libraries. Just validate that the integer is non-negative if that's the case.
- Do not use enums. Use aliases for string instead (e.g., `NodeConditionType`).
- Look at similar fields in the API (e.g., ports, durations) and follow the
  conventions of existing fields.
- All public integer fields MUST use the Go `(u)int32` or Go `(u)int64` types,
  not `(u)int` (which is ambiguous depending on target platform). Internal
  types may use `(u)int`.
- Think twice about `bool` fields. Many ideas start as boolean but eventually
  trend towards a small set of mutually exclusive options.  Plan for future
  expansions by describing the policy options explicitly as a string type
  alias (e.g. `TerminationMessagePolicy`).

#### Constants

Some fields will have a list of allowed values (enumerations). These values will
be strings, and they will be in CamelCase, with an initial uppercase letter.
Examples: `ClusterFirst`, `Pending`, `ClientIP`. When an acronym or initialism
each letter in the acronym should be uppercase, such as with `ClientIP` or
`TCPDelay`. When a proper name or the name of a command-line executable is used
as a constant the proper name should be represented in consistent casing -
examples: `systemd`, `iptables`, `IPVS`, `cgroupfs`, `Docker` (as a generic
concept), `docker` (as the command-line executable). If a proper name is used
which has mixed capitalization like `eBPF` that should be preserved in a longer
constant such as `eBPFDelegation`.

All API within Kubernetes must leverage constants in this style, including
flags and configuration files. Where inconsistent constants were previously used,
new flags should be CamelCase only, and over time old flags should be updated to
accept a CamelCase value alongside the inconsistent constant. Example: the
Kubelet accepts a `--topology-manager-policy` flag that has values `none`,
`best-effort`, `restricted`, and `single-numa-node`. This flag should accept
`None`, `BestEffort`, `Restricted`, and `SingleNUMANode` going forward. If new
values are added to the flag, both forms should be supported.

#### Unions

Sometimes, at most one of a set of fields can be set.  For example, the
[volumes] field of a PodSpec has 17 different volume type-specific fields, such
as `nfs` and `iscsi`.  All fields in the set should be
[Optional](#optional-vs-required).

Sometimes, when a new type is created, the api designer may anticipate that a
union will be needed in the future, even if only one field is allowed initially.
In this case, be sure to make the field [Optional](#optional-vs-required)
In the validation, you may still return an error if the sole field is unset. Do
not set a default value for that field.

### Lists and Simple kinds

Every list or simple kind SHOULD have the following metadata in a nested object
field called "metadata":

- resourceVersion: a string that identifies the common version of the objects
returned by in a list. This value MUST be treated as opaque by clients and
passed unmodified back to the server. A resource version is only valid within a
single namespace on a single kind of resource.

Every simple kind returned by the server, and any simple kind sent to the server
that must support idempotency or optimistic concurrency should return this
value. Since simple resources are often used as input alternate actions that
modify objects, the resource version of the simple resource should correspond to
the resource version of the object.

## Verbs on Resources

API resources should use the traditional REST pattern:

- GET /&lt;resourceNamePlural&gt; - Retrieve a list of type
&lt;resourceName&gt;, e.g. GET /pods returns a list of Pods.
- POST /&lt;resourceNamePlural&gt; - Create a new resource from the JSON object
provided by the client.
- GET /&lt;resourceNamePlural&gt;/&lt;name&gt; - Retrieves a single resource
with the given name, e.g. GET /pods/first returns a Pod named 'first'. Should be
constant time, and the resource should be bounded in size.
- DELETE /&lt;resourceNamePlural&gt;/&lt;name&gt;  - Delete the single resource
with the given name. DeleteOptions may specify gracePeriodSeconds, the optional
duration in seconds before the object should be deleted. Individual kinds may
declare fields which provide a default grace period, and different kinds may
have differing kind-wide default grace periods. A user provided grace period
overrides a default grace period, including the zero grace period ("now").
- DELETE /&lt;resourceNamePlural&gt; - Deletes a list of type
&lt;resourceName&gt;, e.g. DELETE /pods a list of Pods.
- PUT /&lt;resourceNamePlural&gt;/&lt;name&gt; - Update or create the resource
with the given name with the JSON object provided by the client.
- PATCH /&lt;resourceNamePlural&gt;/&lt;name&gt; - Selectively modify the
specified fields of the resource. See more information [below](#patch-operations).
- GET /&lt;resourceNamePlural&gt;&quest;watch=true - Receive a stream of JSON
objects corresponding to changes made to any resource of the given kind over
time.

### PATCH operations

The API supports three different PATCH operations, determined by their
corresponding Content-Type header:

- JSON Patch, `Content-Type: application/json-patch+json`
  - As defined in [RFC6902](https://tools.ietf.org/html/rfc6902), a JSON Patch is
a sequence of operations that are executed on the resource, e.g. `{"op": "add",
"path": "/a/b/c", "value": [ "foo", "bar" ]}`. For more details on how to use
JSON Patch, see the RFC.
- Merge Patch, `Content-Type: application/merge-patch+json`
  - As defined in [RFC7386](https://tools.ietf.org/html/rfc7386), a Merge Patch
is essentially a partial representation of the resource. The submitted JSON is
"merged" with the current resource to create a new one, then the new one is
saved. For more details on how to use Merge Patch, see the RFC.
- Strategic Merge Patch, `Content-Type: application/strategic-merge-patch+json`
  - Strategic Merge Patch is a custom implementation of Merge Patch. For a
detailed explanation of how it works and why it needed to be introduced, see
[here](/contributors/devel/sig-api-machinery/strategic-merge-patch.md).

## Idempotency

All compatible CSM APIs MUST support "name idempotency" and respond with
an HTTP status code 409 when a request is made to POST an object that has the
same name as an existing object in the system.

Names generated by the system may be requested using `metadata.generateName`.
GenerateName indicates that the name should be made unique by the server prior
to persisting it. A non-empty value for the field indicates the name will be
made unique (and the name returned to the client will be different than the name
passed). The value of this field will be combined with a unique suffix on the
server if the Name field has not been provided. The provided value must be valid
within the rules for Name, and may be truncated by the length of the suffix
required to make the value unique on the server. If this field is specified, and
Name is not present, the server will NOT return a 409 if the generated name
exists - instead, it will either return 201 Created or 504 with Reason
`ServerTimeout` indicating a unique name could not be found in the time
allotted, and the client should retry (optionally after the time indicated in
the Retry-After header).

## Serialization Format

APIs may return alternative representations of any resource in response to an
Accept header or under alternative endpoints, but the default serialization for
input and output of API responses MUST be JSON.

All dates should be serialized as RFC3339 strings.

## Units

Units must either be explicit in the field name (e.g., `timeoutSeconds`), or
must be specified as part of the value (e.g., `resource.Quantity`). Which
approach is preferred is TBD, though currently we use the `fooSeconds`
convention for durations.

Duration fields must be represented as integer fields with units being
part of the field name (e.g. `leaseDurationSeconds`). We don't use Duration
in the API since that would require clients to implement go-compatible parsing.

## HTTP Status codes

The server will respond with HTTP status codes that match the HTTP spec. See the
section below for a breakdown of the types of status codes the server will send.

The following HTTP status codes may be returned by the API.

### Success codes

- `200 StatusOK`
  - Indicates that the request completed successfully.
- `201 StatusCreated`
  - Indicates that the request to create kind completed successfully.
- `204 StatusNoContent`
  - Indicates that the request completed successfully, and the response contains
no body.
  - Returned in response to HTTP OPTIONS requests.

#### Error codes

- `307 StatusTemporaryRedirect`
  - Indicates that the address for the requested resource has changed.
  - Suggested client recovery behavior:
    - Follow the redirect.

- `400 StatusBadRequest`
  - Indicates the requested is invalid.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `401 StatusUnauthorized`
  - Indicates that the server can be reached and understood the request, but
refuses to take any further action, because the client must provide
authorization. If the client has provided authorization, the server is
indicating the provided authorization is unsuitable or invalid.
  - Suggested client recovery behavior:
    - If the user has not supplied authorization information, prompt them for
the appropriate credentials. If the user has supplied authorization information,
inform them their credentials were rejected and optionally prompt them again.

- `403 StatusForbidden`
  - Indicates that the server can be reached and understood the request, but
refuses to take any further action, because it is configured to deny access for
some reason to the requested resource by the client.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `404 StatusNotFound`
  - Indicates that the requested resource does not exist.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `405 StatusMethodNotAllowed`
  - Indicates that the action the client attempted to perform on the resource
was not supported by the code.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `409 StatusConflict`
  - Indicates that either the resource the client attempted to create already
exists or the requested update operation cannot be completed due to a conflict.
  - Suggested client recovery behavior:
    - If creating a new resource:
      - Either change the identifier and try again, or GET and compare the
fields in the pre-existing object and issue a PUT/update to modify the existing
object.
    - If updating an existing resource:
      - See `Conflict` from the `status` response section below on how to
retrieve more information about the nature of the conflict.
      - GET and compare the fields in the pre-existing object, merge changes (if
still valid according to preconditions), and retry with the updated request
(including `ResourceVersion`).

- `410 StatusGone`
  - Indicates that the item is no longer available at the server and no
forwarding address is known.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `422 StatusUnprocessableEntity`
  - Indicates that the requested create or update operation cannot be completed
due to invalid data provided as part of the request.
  - Suggested client recovery behavior:
    - Do not retry. Fix the request.

- `429 StatusTooManyRequests`
  - Indicates that the either the client rate limit has been exceeded or the
server has received more requests then it can process.
  - Suggested client recovery behavior:
    - Read the `Retry-After` HTTP header from the response, and wait at least
that long before retrying.

- `500 StatusInternalServerError`
  - Indicates that the server can be reached and understood the request, but
either an unexpected internal error occurred and the outcome of the call is
unknown, or the server cannot complete the action in a reasonable time (this may
be due to temporary server load or a transient communication issue with another
server).
  - Suggested client recovery behavior:
    - Retry with exponential backoff.

- `503 StatusServiceUnavailable`
  - Indicates that required service is unavailable.
  - Suggested client recovery behavior:
    - Retry with exponential backoff.

- `504 StatusServerTimeout`
  - Indicates that the request could not be completed within the given time.
Clients can get this response ONLY when they specified a timeout param in the
request.
  - Suggested client recovery behavior:
    - Increase the value of the timeout param and retry with exponential
backoff.

## Naming conventions

- Go field names must be PascalCase. JSON field names must be camelCase. Other
than capitalization of the initial letter, the two should almost always match.
No underscores or dashes in either.
- Field and resource names should be declarative, not imperative (SomethingDoer,
DoneBy, DoneAt).
- Use `Node` where referring to
the node resource in the context of the cluster. Use `Host` where referring to
properties of the individual physical/virtual system, such as `hostname`,
`hostPath`, `hostNetwork`, etc.
- `FooController` is a deprecated kind naming convention. Name the kind after
the thing being controlled instead (e.g., `Job` rather than `JobController`).
- The name of a field that specifies the time at which `something` occurs should
be called `somethingTime`. Do not use `stamp` (e.g., `creationTimestamp`).
- We use the `fooSeconds` convention for durations, as discussed in the [units
subsection](#units).
  - `fooPeriodSeconds` is preferred for periodic intervals and other waiting
periods (e.g., over `fooIntervalSeconds`).
  - `fooTimeoutSeconds` is preferred for inactivity/unresponsiveness deadlines.
  - `fooDeadlineSeconds` is preferred for activity completion deadlines.
- Do not use abbreviations in the API, except where they are extremely commonly
used, such as "id", "args", or "stdin".
- Acronyms should similarly only be used when extremely commonly known. All
letters in the acronym should have the same case, using the appropriate case for
the situation. For example, at the beginning of a field name, the acronym should
be all lowercase, such as "httpGet". Where used as a constant, all letters
should be uppercase, such as "TCP" or "UDP".
- The name of a field referring to another resource of kind `Foo` by name should
be called `fooName`. The name of a field referring to another resource of kind
`Foo` by ObjectReference (or subset thereof) should be called `fooRef`.
- More generally, include the units and/or type in the field name if they could
be ambiguous and they are not specified by the value or value type.
- The name of a field expressing a boolean property called 'fooable' should be
called `Fooable`, not `IsFooable`.

## Validation

API objects are validated upon receipt by the apiserver. Validation errors are
flagged and returned to the caller in a `Failure` status with `reason` set to
`Invalid`. In order to facilitate consistent error messages, we ask that
validation logic adheres to the following guidelines whenever possible (though
exceptional cases will exist).

- Be as precise as possible.
- Telling users what they CAN do is more useful than telling them what they
CANNOT do.
- When asserting a requirement in the positive, use "must".  Examples: "must be
greater than 0", "must match regex '[a-z]+'".  Words like "should" imply that
the assertion is optional, and must be avoided.
- When asserting a formatting requirement in the negative, use "must not".
Example: "must not contain '..'".  Words like "should not" imply that the
assertion is optional, and must be avoided.
- When asserting a behavioral requirement in the negative, use "may not".
Examples: "may not be specified when otherField is empty", "only `name` may be
specified".
- When referencing a literal string value, indicate the literal in
single-quotes. Example: "must not contain '..'".
- When referencing another field name, indicate the name in back-quotes.
Example: "must be greater than `request`".
- When specifying inequalities, use words rather than symbols.  Examples: "must
be less than 256", "must be greater than or equal to 0".  Do not use words
like "larger than", "bigger than", "more than", "higher than", etc.
- When specifying numeric ranges, use inclusive ranges when possible.

## External References

1. Follow [Postel's Law](https://en.wikipedia.org/wiki/Robustness_principle) _"Be conservative in what you send, be liberal in what you accept"_
1. Reference the [Kubernetes Conventions](https://github.com/kubernetes/community/blob/master/contributors/devel/api-conventions.md) for missing scope
1. REST, as a pattern, was first codified by Roy Fielding in his [dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) in 2000.
1. [API Design Guidelines example](https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9)
1. Google's [API Design Guide](https://cloud.google.com/apis/design/)
1. Azure's [API Design Guide](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
1. OpenStack's [API Style Guide](https://wiki.openstack.org/wiki/APIStyleGuide)
