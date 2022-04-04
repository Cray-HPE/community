# 2022-03-23

## Status

### Update on CSM 1.2.0-beta.90 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
    * .3% critical, 2.4% high, 42% medium, 55.3% low
* 1.2.5 Branch has been opened, focus will pivot, details TBD
* Planning underway re: delivery of security patch sets in 1.2.x series going forward
* Current Remediation
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Approval in place, two implementation work packages
            * Improving small set of container best practices, automating current approach with mutable opaque image tags/investing in OCI metadata for build source provenance
            * Enabling ephemeral containers when CSM reaches K8S 1.23. Moving down a path of minimal production images (content).
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams
* Update on Spire TPM-based Remote Attestation
    * TPM provisioning initially planned to be administrator action, enrollment control based
    * Backwards compatibility and mixed hardware support for Spire Join token in BSS
    * Longer term plans for HPE MFG specfic TPM identity provisioning, ~ 2 years out
* Admin, SIG Chairs, feedback on SIG format
    * Teams represented were good with the status quo in terms of frequency and format
    * Reaching out to all chairs and verifying desire to remain a chair

## Round-table

### Concern around COS patching cadence

SIG raised a desire to know more about the COS patching cadence and strategy. As we don't have SIG representation for COS, passed a note along to the appropriate HPE contacts.

### CSM 1.2 Availability

Targeting ~ end of April, only release critical content being admitted. Need to work through 4-6 weeks of full (Shasta) product stack integration.

The Nexus change to enable authentication/authorization for write has raise some issues with other teams, as has some changes in artifactory conventions. 

### RDMA Security

Some interest was raised around RDMA (SS) Security Controls. A presentation will be organized outside of the SIG for now, but perhaps be briefed to the SIG later. 