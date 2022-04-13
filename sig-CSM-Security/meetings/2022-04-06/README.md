# 2022-04-06

## Status

### Update on CSM 1.2.0-beta.97 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * 3% critical, 5.5% high, 41.2% medium, 52.9% low
        * Cursory analysis suggests high uptick is due to a zlib memory corruption bug on deflate, originally found in 2018, but reported as a CVE a few days ago... (CVE-2018-25032)
* 1.2.5 Branch has been opened, focus will remain on burn down in 1.2 for now, progress towards rebuild automation starting in ~ 1.2.5
* Planning underway re: delivery of security patch sets in 1.2.x series going forward
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams (1.2)
* Update on 'non-root' Container Hardening
    * Broader integration testing has started
    * Part of this feature will be delivered as part of Helm "Base" Charts, part using Kyverno mutating policies
* Update/comment on specific CVEs
    * CVE-2022-23648 - CSM is aware thanks to customers raising awareness, need to create ticket out for remediation going forward. Appears to require a specfically crafted container image to exploit. 
* Update on multi-tenancy SIG status
    * Working to constitute/reconstitute SIG
    * Will cross-brief the security SIG on tenant operator architecture

## Round-table

### When will Kubernetes 1.23 be available in CSM?

No confirmed plan. CSM 1.2 will ship with Kubernetes 1.20. Generally upgrading one version per CSM major release, but looking into options to bring K8S upgrades in certain CSM minor releases as well. Features of note for interest in the upgrade are ephemeral debug containers (1.23 K8S beta) and removal of managed fields (1.21 K8S (?)). 

### UAI Security Posture

Concerns were raised over the network adjaceny and lack of isolation between UAIs and the CSM Control Plane (Kubernetes). Some expressed a desire to move UAIs outside of the control plane and rely on UANs until a solution was available to do so, even when considering the introduction of sandboxing methods (e.g., Kata, gVisor, etc). Aside from security, the ability to dynamically provision UAIs was cited as a strength of the feature, a property that should be considered as the feature set evolves. There was some comparison and debate around how UAIs would be used vs. other HPC Container Runtimes in use.

### User Container HPC Runtimes

As a tangent to the UAI disussion, SIG attendees noted that there are multiple HPC Container Runtimes in use across different HPC centers. A few that were mentioned are [Charlie Cloud](https://github.com/hpc/charliecloud), [Saurus](https://sarus.readthedocs.io/en/stable/), and [Shifter](https://github.com/NERSC/shifter).

### Security Posture of DVS on K8S Worker Nodes

Concerns were raised over the presence of DVS on the K8S worker nodes. The concerns raised were focused on lack of isolation (security) and DVS kernel module residence. The latter perceived as complicating CSM control plane updates, which may lead to delays in getting critical security patches out. 

### Fast Track Security Mitigation

The SIG briefly discussed the concept of CSM providing 'fast track' security mitigations. In short, procedures, patches, and policies (e.g., securty controls) that could be easily applied, and backed out, without being subject to the delay (or asssurances) of integration testing. As a segue to the next topic, there was general consensus that such an approach might require gains in runtime test capabilities. 

### CSM Helm Test Inclusion Improvements

Andrew Nieuwsma (HPE CSM) verbally briefed the team on [Helm Test[(https://helm.sh/docs/helm/helm_test/)] enhancements that are being added to some Kubernetes workloads within CSM. Tests can be invoked during runtime, to verify basic control-plane functionality. The SIG expressed interest in the feature set, and asked Andrew to follow-up and share the design if possible -- this on the balance that others within the SIG might be able to adopt a similar approach. 