# 2022-02-23

## Status

### Update on CSM 1.2.0-alpha.71 (pre-release) container image vulnerability statistics and response

* CSM's focus is on remediation of high and critical vulns, with further prioritization on addressing 'fixable' vulnerabilities
* Total overall vuln trend is relatively flat, critical and high vulns are tending down, as are critical and high 'fixables'
    * Metric comes from Snyk, defined as "Is this vulnerability fixable by upgrading a dependency?" (or there is a nearestFixedVersion)
* .4% of vulns are critical (100% of those fixable), 1.2% are high (96.8% of those fixable)
    * 15 of 177 images have critical or high vulns
* Current remediation efforts
    * SDLC enhancement proposal for contributors: https://github.com/Cray-HPE/community/issues/32
        * Proposal approved, now turning towards implementation definitions
    * Weekly reviews by engineering and product management
    * Triage of all images with critical and high vulnerabilities, ticketing and assignment out to development teams
* Focus on container image vulnerability remediation until beta release of 1.2 (~ 1st week of March), then turn to stabilization
    * May lead to higher vulnerability counts

### Update on container runtime security ("non-root") status

* Initial policies have started to land (1.2 pre-release), https://github.com/Cray-HPE/cray-kyverno-policies

### SIG Poll on Container Image Signing Use Cases

Not one actively pursuing internal signing at this time, SIG interested in HPE signing delivery. 

Sites may or may not have the ability to sign, need flexible policies. They need the ability to create namespaces (or otherwise tune policy) that are not signed or signed differently, etc. Need to ensure air-gapped operation is inherent in design. 

