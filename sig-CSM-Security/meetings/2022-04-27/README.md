# 2022-04-27

## Status

### Update on CSM 1.2.0-beta.106 (pre-release) container image vulnerability statistics and response

* Update on CSM 1.2.0-rc.1 (release candidate) container image vulnerability statistics and response
    * CSM's focus is on remediation of high and critical vulns for non-exceptions
        * Exceptions == version locks where decisions are optimized for stability through integration testing
            * 16 / 24 images currently have exceptions, critical review for a couple of these
        * .4% critical, 3.1% high, 43.4% medium, 53.1% low
        * Auto-container rebuild functionality to 'pause' leading into 1.2 GA for stabilization, resume once GA avail
* Open discussion, are sites independently assessing or adopting VMM-style container sand-boxing and host (kernel) isolation?
    * For context, https://katacontainers.io/
    * Some are working with OpenShift for other applications, and noted some value in the integrated sand-boxing techniques, specifics not discussed

## Round-table

### New "Headliner" CVEs Announced

https://www.microsoft.com/security/blog/2022/04/26/microsoft-finds-new-elevation-of-privilege-linux-vulnerability-nimbuspwn/