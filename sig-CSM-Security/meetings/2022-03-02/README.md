# 2022-03-02

## Status

### Update on CSM 1.2.0-alpha.71 (pre-release) container image vulnerability statistics and response

* Update on CSM 1.2.0-alpha.76 (pre-release) container image vulnerability statistics and response
    * CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
        * .6% of vulns are critical, 2.3% high
    * Trends still relatively flat, now on Alpha 78, see burn down of crit/highs (progress)
    * Current Remediation
        * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
            * Approval in place, two implementation work packages
                * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
                * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
        * Weekly reviews by engineering and product management
        * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams

### Update on container runtime security ("non-root") status

Considerable restrictions landing in 1.2, further restrictions landing in 1.2.5. 1.2.5 focus is on workloads that have a network ingress path.

### Roadmap Status Update

Currently reviewing the security-specific roadmap and trying to align with capacity, requirements, and value. Please forgive me if I reach out and ask questions of specific folks/customers in the SIG. Don't yet have date, but will present to the SIG (and need to start doing so on a routine basis). 

### Multi-tenancy

No one in security SIG earnestly pursuing multi-tenant use cases, but there is perhaps longer term interest in carving out a tenant for TDS-like or CI/CD flows.

## Round-table

### Any thought about breaking the Ceph Storage Cluster out into a separate product? 

Context: possibly making upgrades easier (decoupling storage cluster operation).

Thought yes, but no product direction at this juncture. The expert that could speak to this isn't typically present in this SIG forum, but the HPE Team can help facilitate a discussion.

### Any thougth to producing more frequent updates and maybe separating updates by system target (control plane, user access, compute)?

Context: Need more frequent updates to keep pace with security vulnerabilities. If updates are going to be more frequent and only impact management plane, customers could "live" with disruption to management plane if it didn't impact compute plane. Customers want to break maintenance operations down if possible. They need to (clearly) understand operational impact.  