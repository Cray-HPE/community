# SIG Roles and Organizational Governance

This charter will be updated as needed to meet the current needs of the CSM project and the Cray-HPE OSS community. Note that in Phase 1 we will not meet allof the ceremony as defined here. This is a best effort directive for the Phase 1 period of time. 

In order to standardize Special Interest Group efforts, create maximum transparency, and route contributors to the appropriate SIG, SIGs should follow these guidelines:

- Create a charter and have it approved according to the SIG charter process
- Meet regularly, at least for 30 minutes every 3 weeks, except November and December
- Keep up-to-date meeting notes, linked from the SIG's page in the community repo
- Record meetings and make them publicly available (mechanism  T.B.D.)
- Report activity with the community via the appropriate mailing list at least once a year, i.e. Shasta-CSM-OSS@hpe.com
    - Each SIG is assigned an update during the monthly community meeting throughout the year from sig-contributor-experience. The meeting host will publish the notes to the kubernetes-dev mailing list with the update.
    - This is separate from the annual report.
- Paricipate in release planning meetings and retrospectives, and burndown meetings, as needed
- Ensure related work happens in a project-owned github org and repository, with code and tests explicitly owned and supported by the SIG, including issue triage, PR reviews, test-failure response, bug fixes, etc.
- Use the forums provided as the primary means of working, communicating, and collaborating, as opposed to private emails and meetings
- Ensure contributing instructions (CONTRIBUTING.md) are defined in the SIGs folder located in the Kubernetes/community repo if the groups contributor steps and experience are different or more in-depth than the documentation listed in the general contributor guide and devel folder.
- Help and sponsor working groups that the SIG is interested in investing in
- Track and identify all SIG features in the current release and k/enhancements


## Roles

### Notes on Roles

Within this section "Lead" refers to someone who is a member of the union of a Chair, Tech Lead or Subproject Owner role. There is no one lead to any Kubernetes community group. Leads have specific decision making power over some part of a group and thus additional accountability. Each role is detailed below.

- Initial roles are defined at the founding of the SIG or Subproject as part of the acceptance of that SIG or Subproject.

### Activity Expectations

- Leads SHOULD remain active and responsive in their Roles.
- Leads taking an extended leave of 1 or more months SHOULD coordinate with other leads to ensure the role is adequately staffed during the leave.
- Leads going on leave for 1-3 months MAY work with other Leads to identify a temporary replacement.
- Leads of a role SHOULD remove any other leads or roles that have not communicated a leave of absence and either cannot be reached for more than 1 month or are not fulfilling their documented responsibilities for more than 1 month.
    - This may be done through a super-majority vote of Leads. If there are not enough active Leads, then a super-majority vote between Chairs, Tech Leads and Subproject Owners may decide the removal of the Lead.

### Requirements

- Leads MUST be at least a "member" on our contributor ladder to be eligible to hold a leadership role within a SIG.
- SIGs MAY prefer various levels of domain knowledge depending on the role. This should be documented.
- People management interests - there's a lot of us!

### Escalations

- Lead membership disagreements MAY be escalated to the SIG Chairs. SIG Chair membership disagreements may be escalated to the Steering Committee.

On-boarding and Off-boarding Leads
- Leads MAY decide to step down at anytime and propose a replacement. Use lazy consensus amongst other Leads with fallback on majority vote to accept proposal. The candidate SHOULD be supported by a majority of SIG contributors or the Subproject contributors (as applicable).
- Leads MAY select additional leads through a super-majority vote amongst leads. This SHOULD be supported by a majority of SIG contributors or Subproject contributors (as applicable).

### Chair

- Number: 2-3

- Membership tracked in sigs.yaml
    - If no tech lead role is present, Chair assumes responsibilities from #tech-lead section.

In addition, run operations and processes governing the SIG:

- SHOULD define how priorities and commitments are managed and delegate to other leads as needed

- SHOULD drive charter changes (including creation) to get community buy-in but MAY delegate content creation to SIG contributors

- SHOULD identify, track, and maintain the SIGs enhancements for current release and serve as point of contact for the release team, but MAY delegate to another Lead to fulfill these responsibilities

    - MAY delegate the creation of a SIG roadmap to other Leads
    - MUST organize a main group meeting and make sure sigs.yaml is up to date including subprojects and their meeting information but SHOULD delegate the need for subproject meetings to subproject owners
    - SHOULD facilitate meetings but MAY delegate to other Leads or future chairs/chairs in training
    - MUST ensure there is a maintained CONTRIBUTING.md document in the appropriate SIG folder if the contributor experience or on-boarding knowledge is different than in the general contributor guide. MAY delegate to contributors to create or update.
    - MUST organize KubeCon/CloudNativeCon Intros and Deep Dives with CNCF Event staff and approve presented content but MAY delegate to other contributors to create material and present
    - MUST ensure meetings are recorded and made available
    - MUST report activity with the community via k-dev mailing list at least once a quarter (slides, video from kubecon, etc)
    - MUST coordinate sponsored working group updates to the SIG and the wider community
    - MUST coordinate communication and be a connector with other community groups like SIGs and the Steering Committee but MAY delegate the actual communication and creation of content to other contributors where appropriate

- MUST provide updates through the monthly community meeting

- MUST present yearly annual report for the group but SHOULD get help with curation from other SIG participants

### Tech Lead

- Optional Role: SIG Technical Leads
    - Establish new subprojects
    - Decommission existing subprojects
    - Resolve X-Subproject technical issues and decisions
    - Number: 2-3
    - Membership tracked in sigs.yaml
    - Role description in technical-lead.md

### Subproject Owner

- Subproject Owners
    - Scoped to a subproject defined in sigs.yaml
    - Seed leads and contributors established at subproject founding
    - SHOULD be an escalation point for technical discussions and decisions in the subproject
    - SHOULD set milestone priorities or delegate this responsibility
    - Number: 2-3
    - Membership tracked in sigs.yaml

### All Leads

- SHOULD maintain health of at least one subproject or the health of the SIG
- SHOULD show sustained contributions to at least one subproject or to the SIG
- SHOULD hold some documented role or responsibility in the SIG and / or at least one subproject (e.g. reviewer, approver, etc)
- MAY build new functionality for subprojects
- MAY participate in decision making for the subprojects they hold roles in
- Includes all reviewers and approvers in OWNERS files for subprojects
- MUST take an inclusive speaker training course in support of our community values within 30 days from the date of their appointment.

### Security Contact

- Security Contact
    - MUST be a contact point for the Product Security Committee to reach out to for triaging and handling of incoming issues
    - MUST accept the Embargo Policy
    - Defined in SECURITY_CONTACTS files, this is only relevant to the root file in the repository. Template SECURITY_CONTACTS

****

#### Subproject Creation

Option 1: by SIG Technical Leads

- Subprojects may be created by KEP proposal and accepted by lazy-consensus with fallback on majority vote of SIG Technical Leads. The result SHOULD be supported by the majority of SIG Leads.
    - KEP MUST establish subproject owners
    - sigs.yaml MUST be updated to include subproject information and OWNERS files with subproject owners
    - Where subprojects processes differ from the SIG governance, they must document how
        - e.g. if subprojects release separately - they must document how release and planning is performed

Option 2: by Federation of Subprojects

- Subprojects may be created by KEP proposal and accepted by lazy-consensus with fallback on majority vote of subproject owners in the SIG. The result SHOULD be supported by the majority of leads.
    - KEP MUST establish subproject owners
    - sigs.yaml MUST be updated to include subproject information and OWNERS files with subproject owners
    - Where subprojects processes differ from the SIG governance, they must document how
        - e.g. if subprojects release separately - they must document how release and planning is performed

- Subprojects may create repos under github.com/kubernetes-sigs through lazy-consensus of subproject owners.

****

- Subprojects must define how releases are performed and milestones are set. Example:
> - Release milestones
>   - Follows the kubernetes/kubernetes release milestones and schedule
>   - Priorities for upcoming release are discussed during the SIG meeting following the preceding release and shared through a PR. Priorities are finalized before feature freeze.
> - Code and artifacts are published as part of the kubernetes/kubernetes release

### Technical processes

Subprojects of the SIG MUST use the following processes unless explicitly following alternatives they have defined.

- Proposing and making decisions

    - Proposals sent as KEP PRs and published to googlegroup as announcement
    - Follow KEP decision making process

- Test health

    - Canonical health of code published to dashboard
    - Consistently broken tests automatically send an alert to their google group.
    - SIG contributors are responsible for responding to broken tests alert. PRs that break tests should be rolled back if not fixed within 24 hours (business hours).
    - Test dashboard checked and reviewed at start of each SIG meeting. Owners assigned for any broken tests and followed up during the next SIG meeting.

Issues impacting multiple subprojects in the SIG should be resolved by either:

    - Option 1: SIG Technical Leads
    - Option 2: Federation of Subproject Owners

### SIG Retirement

- In the event that the SIG is unable to regularly establish consistent quorum or otherwise fulfill its Organizational Management responsibilities
    - after 3 or more months it SHOULD be retired
    - after 6 or more months it MUST be retired