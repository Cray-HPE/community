# 2022-04-20

## Status

### Update on CSM 1.2.0-beta.106 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * .5% critical, 3.4% high, 42.8% medium, 53.3% low
* Focusing away from 1.2.5, towards 1.3
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams (1.2)
* Discussion of Chainguard's 'apko' tool for building 'distroless' images, using a declarative format, with a novel (?) approach to SBOM creation, based on Alpine: https://blog.chainguard.dev/introducing-apko-bringing-distroless-nirvana-to-alpine-linux/
* Kubernetes API (etcd) Encryption in CSM
    * Encryption at rest provided by K8S API, not etcd
    * When introduced in CSM release, configuration file and K8S API Server integration is planned
    * Keys will need to be configured and managed by users of CSM
    * Recommend only encrypting K8S Secret Resources

## Round-table

### Some references on etcd, K8S API Encryption (etcd)

K8S API Etcd Encryption: https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/

Etcd Performance: https://etcd.io/docs/v3.4/op-guide/performance/

Etcd KV Versioning: https://etcd.io/docs/v3.4/dev-guide/interacting_v3/#read-past-version-of-keys

### Is HPE considering introducing solutions like Falco into CSM?

https://falco.org/

Yes, but trying to reason about it 'roadmap'-wise relative to other controls, like K8S security broadly, K8S Pod security controls, SECCOMP, etc. So, some prioritization and further disussion is needed to move this forward.

One CSM user indicated that they were looking to HPE and CSM/Shasta to both integrate (ship) with types of controls, and provide best pratices in their implementation. 

The team noted that stacks like Falco could provide a platform for mitigating controls, for emergent security vulnerabilities -- providing time for longer-term response. 

The team talked through the operational and development overhead introduced by tools in this category. As an example, some of this controls actually reject legitimate admin behavior (shell in a container) if it doesn't match the workloads runtime profile.

A couple of other solutions, broadly, were discussed. Namely:

* https://www.stackrox.io/
* https://www.paloaltonetworks.com/prisma/cloud

### CSM Version Plan Changes

User community expressed a desire to know more about version strategy changes around CSM 1.2, 1.2.5, and 1.3. In short, alignment is currently taking place and discussions will need to continue.

### Vulnerabilty Scanning Transparency

Similar to how CSM now provides granular transparency with Snyk-based container-vulnerabilty scanning results, the user community expressed a desire to see similar result sharing around CIS Kubernetes Benchmarks. In short, CSM releases should include scan results in a consumable format. 