---
layout: post
tags: Platform-Engineering DevOps
---
The [CNCF Platform Engineering Maturity Model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/) has useful insights for IT organizations with platform engineering teams.

I want to relate some of my own thoughts and experience with the Platform Adoption / Maturity graph.

![Platform Engineering Maturity Model — Adoption/Maturity (Credit: CNCF)]({{site.url}}/assets/images/20231105/adoption-curve.jpg)


“L2: Operational” is not a happy place and should not be considered a viable status quo in any organization that aspires to implement platform engineering. While it is a necessary foundation for the third stage “L3: Scalable”, the developer experience in these two stages could not be more different. L2 is essentially a consolidation phase after the discovery in L1 “Provisional”. Development teams have freedom to experiment and create in L1 but it comes at the cost of technology stack sprawl, possible scalability and security issues resulting from the experimentation and sometimes technical debt for later rework. New organizations and initiatives then try to remediate the issues from L1 with introducing technology standards and formalization of requirements.

L2 highly depends on the organization’s IT architecture vision. It is the stage at which the organization decides on the foundations and standards to streamline application development. If the vision is too broad then the implementation will take a long time and synergies from code reuse and promotion of shared libraries are lost. If the vision is too narrow, then it can have a toxic effect on innovation and risks that the approved platform choices become museum relics instead of evolving best-practices.

A hypothetical IT standards directive for platform engineering offerings could be: “We have standardized our development on Java 1.8 and Oracle 12.” The standards committee reaches this conclusion after hiring consultants to evaluate the existing technology stacks across the organization for commonalities. Such an assignment is problematic in itself as it disregards higher-level questions: “How modern are the tech stacks across our development teams and vendors? What are modern technologies in the market today that allow us to build software?”

Setting too narrow standards together with a rigid standards approval process means that technology choices are artificially restricted and can easily become entrenched thanks to groupthink. It is easy for siloed stakeholders to keep the existing standard as status quo. Anyone challenging this will need to overcome objections based on outdated information and stakeholders unwilling to change and improve.

Another issue created in L2 is that it fosters manual processes and reviews that are then seen as standard offering. Coupled with siloed stakeholders, this leads to scenarios where development teams have to file tickets and wait for manual approval and work queue processes for weeks to create their IT infrastructure.

If there was one thing that IT organizations should have learned from Cloud providers by now, it is that **standard infrastructure resources can be created in a matter of minutes.** It should not be seen in any way as acceptable to have to wait for weeks for things like virtual machines, database and middleware instances, or network configurations. Moreover, manually provisioned resources are prone to configuration drift that may or may not be immediately detected. Defect remediation in these cases usually is flawed with well-intended but misplaced change control directives.

Platform offerings and capabilities need to set the standard degree for automation in order to be accepted by the developer community. This means that they should be self-service and scalable by design. Which brings us to L3 in the maturity model.

**In my view, work on forming the L3 state needs to commence early in L2 and allow for enough flexibility to easily extend the platform automation for new choices. Automation should be a key driver for the L3 platform deliverables and platform teams should be held accountable for their degree of product automation.**




![Engineering platforms are not ticket generators]({{site.url}}/assets/images/20231105/no-ticket.png)

Portals for autoamted IT-ticket generation are not engineering platforms!

**If a platform engineering product is a UI that merely masks a “IT ticket generator” then the product is a failure and cannot be considered a L3 capability.** It does not scale at all and just continues the manual L2 workflow toil in a hidden shadow-IT way.

![CI/CD pipelines — fully automated.]({{site.url}}/assets/images/20231105/bot.png)

CI/CD pipelines — fully automated.
A platform engineering portal is flexible and considers API as its main interface.

A platform engineering product that fulfils L3 requirements is API-first and scalable by design. Its workflows are fully automated and visualize for transparency.

Application teams can manage their infrastructure as-code or configuration. This config-as-code then becomes their source-of-truth for any queries and frees the wider organization from outdated configuration management database (“CMDB”) approaches. A central CMDB can still exist, however, with a configuration-as-code workflow, it would get its data from the platform engineering pipelines. Updating the CMDB would just be another API call from the platform whenever platform-managed resources are created, modified or deleted.

High-level, platform engineering infrastructure workflows are not different from software engineering CI/CD workflows.

Sample build-test-deploy workflow for an automated software pipeline:

![CI/CD pipelines — fully automated.]({{site.url}}/assets/images/20231105/sdlc-pipeline.png)

Automated SDLC: CI/CD pipeline

An infrastructure-as-code portal uses the same artifacts to automatically create IT infrastructure resources.

![Sample plan-test-deploy workflow for an automated infrastructure pipeline.]({{site.url}}/assets/images/20231105/IaC-pipeline.png)

Automated infrastructure-as-code (IaC): CI/CD pipeline

![Sample plan-test-deploy workflow for an automated infrastructure pipeline.]({{site.url}}/assets/images/20231105/IaC-pipeline-implementation.png)

Automated infrastructure-as-code: Sample implementation

**Organizations that fully embrace software development workflows for their IT infrastructure are more agile, secure, and standards compliant as opposed to organizations that are stuck with various manual ways of working in legacy processes. Being too restrictive and focused on existing process and technology in the operationalization phase (L2) will hinder the organization from embracing the benefits of the scalable platform engineering state (L3).**
