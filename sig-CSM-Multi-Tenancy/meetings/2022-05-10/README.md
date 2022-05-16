# 2022-05-10

## Status

* (Design/Discussion) Details around mapping process between LDAP and CSM KeyCloak (shasta realm)
    * MVP mapping would be done manually (import users from LDAP, map to shasta realm roles)
        * Role mapping to express that a user
            * is a tenant administrator
            * is a tenant administrator, for a specific set of tenants
        * Need CSCS IAM SME to participate
        * Outcome
            * Team landed on a procedural approach for tenant administrator configuration in CSM KeyCloak (Shasta Realm), for the multi-tenancy MVP. This building upon established (CSCS) procedures for infrastructure administrator mappings and upstream federation, and avoiding a prescriptive approach for IdP integration. 
            * HPE to investigate options for role mappings and JWT claims for Shasta API authorization. 
            * Team agreed this area is ripe for future automation once a solid integration pattern is established. 
* HPE to brief architecture and the demo Tenant Operator
    * Briefing and demo completed, CSCS validated the operator solution path

## Round-table

Need follow-up discussion on mapping a tenant administrator, to a tenant in Kubernetes. One possibility is via [Kubernetes OIDC Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens), using KeyCloak as the OIDC IdP, as this would unify Shasta API and Kubernetes access from an RBAC perspective. 

HPE to demo K8S Operator for Slurm, at next SIG. CSCS to tentatively demo tenant orchestration and deployment architcture currently in use (~ 2 weeks out).