# 2022-04-22

## Status

* Identity management for the tenant administrator
    * Starter Solution Discussed
        * CSM KeyCloak will be used, as AuthN/Z for CSM API access currently requires JWT validation in this way
        * CSM KeyCloak will be federating with an upstream directory provider (e.g., LDAP)
        * CSM KeyCloak will need to be configured with a new general RBAC role, e.g., tenant administrator, mapped to upstream directory attributes (to designate an identity as a tenant admin)
        * CSM KeyCloak will need to be configured with a way to associate specific tenants with a tenant administrator, mapped to upstream directory attributes (to designate an identity as having permissions to a set of tenants)
    * The model above was well received, with the following discussion/feedback
        * Tenant users currently do not use CSM KeyCloak, but rather native LDAP
        * Ultimately needs to translate to claims or similar attribution in the 'shasta' OIDC Realm (e.g., private claims)
        * The initial feature set should focus on CSM KeyCloak -> LDAP Integration
        * It should be possible for infrastructure admins to manually map tenant administrator roles in CSM KeyCloak
            * If a CSM user decides to manage the CSM KeyCloak <-> LDAP Sync in custom ways
        * Ensure the feature supports a single tenant administrator that can manage zero or more tenants (0,1,2,...)
        * Team discussed naming contraints on tenants (Brad Klein, HPE)
            * No preferences noted, team agreed we needed constraints, HPE described initial approach in Tenant Operator 
        * Requires further vetting by CSCS IAM Architect
* (Initial) selectors for compute partition associated with a tenant
    * The HPE model so far has been mocked up as a 'list of xnames'
    * Mark Klein to share what CSCS has in place/is thinking about
        * CSCS also using xnames, HSM group definitions stored in Git
            * Groups change when ~ git changes
            * Concern about using static xname maps on much larger systems (mgmt overhead)
                * Currently using smaller system
                * Might be nice to support hardware selectors to abstract explicit xname mapping
                    * e.g., 10 GPU nodes, 30 multi-core nodes
                * Eventually need to discuss placement constraints and trade-offs (not MVP)
                    * HSN and chassis placement
                    * Cooling groups
        * HSM groups are used to define tenant-specific boot artifacts
        * Using HSM groups vs. partitions
            * At one time, couldn't use partitions due to boot failures
            * Partitions are desired to enforce non-overlapping tenants
        * Using CFS for post-boot orchestration
        * Local modifications to the Slurm generator to query HSM group membership
            * David Gloe (HPE) indicated that the WLM Team at HPE is making the same/similar change

* Future Topics
    * Details around mapping process between LDAP and CSM KeyCloak (shasta realm)
        * MVP mapping would be done manually (import users from LDAP, map to shasta realm roles)
            * Role mapping to express that a user is
                * A tenant administrator
                * Has administrative access to a set of tenants (one user can manage zero or more tenants)
            * (Mark Klein) Need CSCS IAM SME to participate
    * How a tenant administrator is provided access to the CSM Kubernetes Cluster
        * One option to explore, Kubernetes OIDC Integration with CSM KeyCloak
    * How tenant user directory federation needs to take shape
        * Would ostensibly use 'external' directory services, not expected to integrate with CSM KeyCloak
        * (Mark Klein) Need CSCS IAM SME on this

## Round-table

No meeting the week of 2022-05-02 due to CUG. Meeting series to start week of 2022-05-09. 