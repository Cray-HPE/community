# Architecture Special Interest Group

The Architecture SIG maintains and evolves the design principles of Kubernetes, and provides a consistent body of expertise necessary to ensure architectural consistency over time.

The [charter](charter.md) defines the scope and governance of the Architecture Special Interest Group.

## Meetings
* Regular SIG Meeting: [Thursdays at 11:00 PT (Pacific Time)](https://zoom.us/j/845605479) (biweekly). [Convert to your timezone](http://www.thetimezoneconverter.com/?t=11:00&tz=PT%20%28Pacific%20Time%29).
  * [Meeting notes and Agenda](https://docs.google.com/document/d/1BlmHq5uPyBUDlppYqAAzslVbAO8hilgjqZUTaNXUhKM/edit).
  * [Meeting recordings](https://www.youtube.com/playlist?list=PL69nYSiGNLP2m6198LaLN6YahX7EEac5g).
* code organization Office Hours: [Thursdays at 14:00 PT (Pacific Time)](https://zoom.us/j/159990793) (biweekly). [Convert to your timezone](http://www.thetimezoneconverter.com/?t=14:00&tz=PT%20%28Pacific%20Time%29).
  * [Meeting notes and Agenda](https://docs.google.com/document/d/1HtTI0rJEGP_MSf6eO87aCmx_tzpovPAAg7U2Zxwm8FE/edit#).
  * [Meeting recordings](https://www.youtube.com/playlist?list=PL69nYSiGNLP03VEluzh0wpSRPzgve8kI5).
* conformance office Hours: [Tuesdays at 19:00 UTC](https://zoom.us/j/427337923) (biweekly). [Convert to your timezone](http://www.thetimezoneconverter.com/?t=19:00&tz=UTC).
  * [Meeting notes and Agenda](https://docs.google.com/document/d/1W31nXh9RYAb_VaYkwuPLd1hFxuRX3iU0DmaQ4lkCsX8/edit#).
  * [Meeting recordings](https://www.youtube.com/playlist?list=PL69nYSiGNLP2m6198LaLN6YahX7EEac5g).

## Leadership

### Chairs
The Chairs of the SIG run operations and processes governing the SIG.

* Alex Lovell-Troy (**[@alexlovelltroy](https://github.com/alexlovelltroy)**), HPE
* , HPE
* , Exascale Computing Group
* , EuroHPC Joint Undertaking

## Contact
- Slack: [#sig-architecture](https://kubernetes.slack.com/messages/sig-architecture)
- [Mailing list](https://groups.google.com/forum/#!forum/kubernetes-sig-architecture)
- [Open Community Issues/PRs](https://github.com/cray-hpe/community/labels/sig%2Farchitecture)

- Steering Committee Liaison: Alex Lovell-Troy (**[@alexlovelltroy](https://github.com/alexlovelltroy)**)

## Subprojects

The following [subprojects][subproject-definition] are owned by sig-architecture:

<!-- BEGIN CUSTOM CONTENT -->

# Details about SIG-Architecture sub-projects

## Architecture and API Governance

Establishing and documenting design principles, documenting and evolving the system architecture, reviewing, curating, and documenting new extension patterns

Establishing and documenting conventions for system and user-facing APIs, define and operate the APl review process, final API implementation consistency validation, co-own top-level API directories with API machinery; maintaining, evolving, and enforcing the deprecation policy

* [Kubernetes Design and Architecture](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/architecture.md)
* [Design principles](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/principles.md)
* [API conventions](/contributors/devel/sig-architecture/api-conventions.md)
* [API Review process](https://github.com/kubernetes/community/blob/master/sig-architecture/api-review-process.md)
* [Deprecation policy](https://kubernetes.io/docs/reference/deprecation-policy/)

Please see the [API Reviews](https://github.com/orgs/kubernetes/projects/13) tracking board to follow the work of this sub-project. Please reach out to folks in the [OWNERS](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/OWNERS) file if you are interested in joining this effort.

## Enhancement Proposals

Kubernetes Enhancement proposals (KEPs) are used to propose and communicate changes to sub-projects of SIG-Architecture. Following the KEP process is mandatory for all enhancements since Kubernetes 1.14 release.

* Answers to our FAQs can be found here [FAQs](https://github.com/kubernetes/enhancements/tree/master/keps#faqs) 
* Full details of the KEP process can be found in [KEP-1](https://github.com/kubernetes/enhancements/blob/master/keps/0001-kubernetes-enhancement-proposal-process.md)
* Please follow the KEP template available at [KEP Template](https://github.com/kubernetes/enhancements/blob/master/keps/NNNN-kep-template/README.md) for the enhancement proposal.
* Progress of KEPs can be tracked on our github project board at [Kubernetes Enhancements](https://github.com/kubernetes/enhancements/projects/4) 
* Please review [OWNERS](https://github.com/kubernetes/enhancements/commit/ed46d6956b616e46cd62ac9a3d98449a0a313c89) to connect with enhancement chairs, approvers, and reviewers

## Conformance Definition

Reviewing, approving, and driving changes to the conformance test suite; reviewing, guiding, and creating new conformance profiles

* [Conformance Tests](https://github.com/kubernetes/kubernetes/blob/master/test/conformance/testdata/conformance.yaml)
* [Test Guidelines](/contributors/devel/sig-architecture/conformance-tests.md)

Please see the [Conformance Test Review](https://github.com/kubernetes-sigs/architecture-tracking/projects/1) tracking board to follow the work for this sub-project. Please reach out to folks in the [OWNERS](https://github.com/kubernetes/kubernetes/blob/master/test/conformance/testdata/OWNERS) file if you are interested in joining this effort. There is a lot of overlap with the [Kubernetes Software Conformance Working Group](https://github.com/cncf/k8s-conformance/blob/master/README-WG.md) with this sub project as well. The github group [cncf-conformance-wg](https://github.com/orgs/kubernetes/teams/cncf-conformance-wg) enumerates the folks on this working group. Look for the `area/conformance` label in the kubernetes repositories to mark [issues](https://github.com/kubernetes/kubernetes/issues?q=is%3Aissue+is%3Aopen+label%3Aarea%2Fconformance) and [PRs](https://github.com/kubernetes/kubernetes/pulls?q=is%3Apr+is%3Aopen+label%3Aarea%2Fconformance) 

## Code Organization

Overall code organization, including github repositories and branching methodology, top-level and pkg OWNERS of kubernetes/kubernetes, vendoring

Please see the [Code Organization](https://github.com/orgs/kubernetes/projects/27) tracking board to follow the work of this sub-project. Please reach out to folks in the [OWNERS](https://github.com/kubernetes/kubernetes/blob/master/vendor/OWNERS) file if you are interested in joining this effort. Look for the `area/code-organization` label in the kubernetes repositories to mark [issues](https://github.com/kubernetes/kubernetes/issues?q=is%3Aissue+is%3Aopen+label%3Aarea%2Fcode-organization) and [PRs](https://github.com/kubernetes/kubernetes/pulls?q=is%3Apr+is%3Aopen+label%3Aarea%2Fcode-organization). We also use `area/dependency` label as well [issues](https://github.com/kubernetes/kubernetes/issues?q=is%3Aissue+is%3Aopen+label%3Aarea%2Fdependency) and [PRs](https://github.com/kubernetes/kubernetes/pulls?q=is%3Apr+is%3Aopen+label%3Aarea%2Fdependency).

## Production Readiness

Defining and documenting the processes for ensuring production readiness of new and
promoted features, as well as producing tooling to enforce those processes.

<!-- END CUSTOM CONTENT -->