# 2022-03-16

## Status

### Update on CSM 1.2.0-beta.85 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * .2% critical, 1.7% high, 46.3% medium, 51.7% low
* Good overall burn-down, overall down largely to removal of unused content
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams

### Specific CVE Updates

* CVE-2022-25636 (watching/researching, only CSM 1.2 would be impacted, patches not yet avail)
    * Use of user namespaces seems to be a common attack vector. While they may be needed in places where sites are leveraging non-mgmt plane container orchestration for 'rootless' mode (e.g., on compute nodes), not sure there is a use currently for the CSM mgmt plane. Might look at disabling as a default posture in CSM 1.2+ (until/if a decision comes o adopt a version of K8S that supports rootless). 
* CVE-2022-0811 (not vuln, CSM uses containerd)