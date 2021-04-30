---
name: Production Readiness Review Request
about: Request software review for production readiness
title: ''
labels: production readiness
assignees: ''

---

- [ ] Deployment
- [ ] Testing
- [ ] Security
- [ ] Scale and Resiliency
- [ ] Disaster Recovery
- [ ] Troubleshooting and Observability

**Deployment**
A concise description of the installation and upgrade procedure for this software with links to detailed documentation.

Please include information about:
  * rollback support
  * any service-impacting downtime
  * backup and recovery procedures

**Testing**
A summary of the manual and automated testing for this service that indicates it is ready for production.

Please include any functional, scale, resiliency, and integration tests.
Links to test reports are very valuable in this section.

**Scale and Resiliency**
A summary of the administrator instructions for handling scale and resiliency events with links to any applicable documentation.


**Disaster Recovery**
A summary of any service-specific disaster recovery procedures beyond basic backup and recovery.


**Security**
A section with a brief description of the security plan for the software.

Please describe how any user data or credentials are handled.

Please include information about the containers or internal dependencies in use and how administrators should view any CVEs that may arise within those components.

Confirm which automated security tools have already validated the service.

**Troubleshooting and Observability**
A summary of basic troubleshooting and monitoring features with links to administrative documentation.  Consider what metrics or logs indicate proper function as well as what leading indicators of problems might be. If there is a service dashboard or reporting tool included with the software, link to it here with instructions for use.
