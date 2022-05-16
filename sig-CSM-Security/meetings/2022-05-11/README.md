# 2022-05-11

## Status

* Update on CSM 1.2.0-beta.120 (pre-release) container image vulnerability statistics and response
    * CSM's focus is on remediation of high and critical vulns for non-exceptions
        * 4453 total vulns: .4% critical, 2.5% high, 45.3% medium, 51.8% low
        * 17/20 images with critical or high on exception list
            * Continuing to review exceptions, patch certain areas with priority (e.g., Nexus, Keycloak) relative to version locking
        * ~ 81% of all container images being rebuilt
            * Auto-container rebuild functionality to 'pause' leading into 1.2 GA for stabilization, resume once GA avail
* Update on non-root containers (Kyverno)
    * HPE Team filed upstream https://github.com/kyverno/kyverno/issues/3732, evaluating pulling Kyverno 1.7.x vs. 1.6.2 into release
    * Impacted team 'sign-off' testing underway
* Update on 3rd Party Red Team Engagement
    * Phase 1 very close to completion, out-brief meetings being scheduled
    * Starting work this week on system build to host test team (phase 2)

## Round-table

Some SIG attendees attended the Cray User Group (CUG) Conference. They expressed a desire to have a more open dialogue around system security, in that forum. 

The SIG expressed interest in both monitoring Kubernetes for unauthorized change, and being able to revert a change. Categorically, the discussion centered on use of K8S API audit log stream monitoring, Helm for deployed resource differences (where resources covered by Helm), and backup/restore facilities in place (etcd for Kubernetes, Velero for select applications like Vault, ...).