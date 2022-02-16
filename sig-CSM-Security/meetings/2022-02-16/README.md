# 2022-02-16

## Status

### Update on CSM 1.2.0-alpha.67 (pre-release) container image vulnerability statistics and response

* Seeing further improvement in Alpha 68 an 69
* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
* Total overall vuln trend is relatively flat, critical and high vulns are tending down, as are critical and high 'fixables'
    * Metric comes from Snyk, defined as "Is this vulnerability fixable by upgrading a dependency?"
* 1.3% of vulns are critical (68.8% of those fixable), 2.6% are high (73.2% of those fixable)
    * 19 of 178 images have critical or high vulns
* Current remediation efforts
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Focus, container build best practices, leverage deterministic automation, build upon existing initiatives
    * Future work to investigate image minimization techniques and CRI runtime controls
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams

### Update on container runtime security ("non-root") status

* Team assessing impact has completed first pass against 84 Helm Charts (index into review)
    * Team used mutating [Kyverno](https://kyverno.io/) policies to apply pod and container security contexts to complete assessment (initial increment used Helm 'base' charts)
    * Review of assessment is underway, working requirement is to set runas user/group to non-root, explicitly disallow non-root UID, and disallow privilege escalation
    * Feature set is currently scheduled for a 1.2.5 release, release planned to include Kyverno and central policy set

### Discussion of Kubernetes 'system:masters' credential presence on NCNs

* Access directly to NCNs (shell/login) should be strictly limited as an operational practice
* The credentials (canonically in /etc/kubernetes/admin.conf) are being used by various provisioning and/or automated processes
* Prospectively, one solution path to resolve includes brining in OIDC authentication for K8S, and then further refining non-person/machine SP credentials, and anchoring OIDC issuance in Spire (w/ TPM RoT)

### CSM 3rd Party Red-Team Assessment

* 1st architecture briefing with team this week

## Roundtable

### Spire TPM-based Attestation

CSM is planning to support Spire with TPM-based attestation, on NCNs, in 1.3. The plan for CN support has not yet been finalized and will depend, at least initially, on specific blade types. 

### Version of K8S in CSM 1.2

Currently planning to ship 1.20.x. 

### Nexus vulnerable to log4j vulnerabilities?

Was not detected in scanning/enumeration exercises involved in HPE response. Based on current information, Nexus uses the "Logback" library for logging, not log4j. 

### CSM 1.2 is currently in alpha, is it expected that there will be a beta phase?

Yes, plan to enter beta after upgrade path stabilization. 

### Question about multi-cluster federation

Tim Pletcher, HPE Security Engineering, polled the SIG about interest in multi-cluster federation use cases. No one on the call indicated they were actively pursuing this type of federation, currently.