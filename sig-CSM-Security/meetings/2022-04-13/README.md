# 2022-04-13

## Status

### Update on CSM 1.2.0-beta.101 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * .3% critical, 3.4% high, 42.4% medium, 53.9% low
* 1.2.5 Branch has been opened, focus will remain on burn down in 1.2 for now, progress towards rebuild automation starting in ~ 1.2.5
* Planning underway re: delivery of security patch sets in 1.2.x series going forward
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams (1.2)
* Overview of the tenant operator architecture (joined by Brad Klein, HPE CSM)
    * In support of CSM soft multi-tenancy feature set, focally
    * Uses K8S Operator pattern, provides declarative configuration support
    * Tenant operator is base declarative data model for orchestration across constituent tenant building blocks (referential, declarative configuration tree)

## Round-table

### Tenant Operator, references of note

Here is some upstream documentation on the Kubernetes Operator Pattern:

https://kubernetes.io/docs/concepts/extend-kubernetes/operator/

And, to offer a sense of how prolific the pattern is, here's a community directory of operators:

https://operatorhub.io/

As a bit of a twist, The [Crossplane](https://crossplane.io/) project takes the concept further, turning K8S into a platform building platform (using K8S to orchestrate external infrastructure, across multiple 'clouds', ...).

Here is an incomplete list of the (non K8S core) operators/controllers we currently use in CSM: 

* Cert-manager
* Vault (bank-vaults)
* Istio
* etcd
* postgresql
* kafka
* Velero
* HPE TrustedCerts (CSM)

Other HPE peers working on HPC-focused storage solutions are also invested in custom operators. 

Here is an approachable read on the Hierachical Namespace Controller (HNC) component also covered in the presentation:

https://www.redhat.com/architect/kubernetes-hierarchical-namespaces

And (finally), if you want to learn more about one approach to GitOps + K8S (Flux):

https://fluxcd.io/ 
