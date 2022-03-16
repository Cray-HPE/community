# 2022-03-09

## Status

### Update on CSM 1.2.0-beta.81 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * .4% critical, 5.7% high, 44.2% medium, 49.7% low
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams

### Specific CVE Updates

* CAST/CVE-2022-0492 (responding)
    * Issue was raised with specific concern to rootless podman, discuss blocking unshare syscall via SECCOMP as mitigation while patch in the works
* CAST/CVE-2022-0847 (not vulnerable)
    * Issue was raised with specific concern to user facing nodes, SLES distributions are not currently vulnerable based on SUSE guidance
* CAST/CVE-2022-23218 and CVE-2022-23219 (responding)
    * Issue was raised with specific concern to user facing nodes (SP1 and SP2 SLES), SLES distributions are vulnerable, at least for 23218 SLES has rated at a CVSS 3 Score of 5.3 vs. NVD score of 9.8, SP1 and SP2 patches not yet avail

### Update on 3rd Party Red Team Engagement

* Remediations for the LANL assessment are planned to be released generally across the 1.2, 1.2.5, and 1.3 timeframe
* Plan to work in close coordination with LANL on the test team scope and timing

## Round-table

### Is there still a solid comitment of using SLES on the NCNs? What about other distros that "move faster" (are faster to adopt upstream changes, incorporate security fixes, and so forth)?

There is no initiative underway to investigate a distribution change. There is currently a fair amount of coupling to SLES within both the management plane, and across the management and managed plane, as it relates to COS and other product streams.

If there is continued interest, this SIG should probably transition the topic to a different forum, first stating the Security SIG's Concern/Interest.