Central Product - Q4'25 Plan
Prior Quarter Review
Delivered 43 of 46 BU Kanban goals
Started the quarter with 44 committed goals and 2 stretch goals. Added 3 more during the quarter, bringing the total to 49 initiatives under active tracking. We delivered 43 goals (93%), missed 2 goals, and canceled (with BU alignment) 3 goals.
The goals we missed are:
Skyvera - CloudSense R38: underestimated the complexity of the work; we expect being 3 weeks late
Ignite - Jive Patch Management: stretch goal that we did not get to
Khoros - canceled 3 goals to make up room for the higher complexity behind X data removal, making new releases with important features and bugs,as well as fixing systemic stability issues that required extensive manual work from a large legacy team
Cost Optimization - huge savings and a notable miss
Data modeling error in AWS forecast negatively impacted the budget by $900k total over three quarters (detailed report). We have taken accountability and have committed to very aggressive targets, aiming to get AWS cost in model by EoQ1 by delivering $3M annualized savings for 3 quarters in a row, at a cost $200k/$1M of annualized savings. We have also standardized the DD process to prevent this.
Khoros: $3.8M realized annualized savings. While this does not bring Khoros into the PP model, it is an achievement in itself and was accomplished with the help of two Kanbans and extensive AI use.
Tivian: $850K/year realized annualized savings. While we missed the target AWS cost mark in Tivian in Q2, we worked on that with SaaS in Q3 and beat the PP by $120k/quarter
Other products (SaaS CO slot): $500k realized annualized savings spread across the entire product portfolio
Khoros Import completed - took over 5 massive products in 90 days following our structured import framework
Wins
Completed import by the end of Oct, arguably 1-month late, but that is still a success given that other acquisitions still had loose ends 9+ months later, and plenty of non-import work was done.
We’ve done a lot of non-import work that was important for the business-critical: X deletion, new feature releases, aggressive CO, stack upgrades for social integrations, etc.
Streamlined work across technical streams - while we continue to operate in silos, the Eng/SaaS/TPMs work as joint teams, which means fewer things falling through the cracks
Losses
We faced product instability as the legacy phased out. In retrospect, Khoros had tens of people performing manual tasks to keep systems running (such as restarts, follow-through noise alerts, etc.). Due to being somewhat too reliant on them, we only realized this after the RIF was completed.
Unplanned costs of ~200k/year with two vendors that were supposed to be terminated but proved to be critical to the operations (OneLogin and DigiCert - summary)
SaaS has inherited an alerting infrastructure that proved too noisy for the team capacity, a topic that we will work to optimize in Q4.
Lessons learned (listing the more important ones):
DD improvements: Standardize CO planning and cover activities that were previously overlooked by Khoros, resulting in unplanned vendor costs.
Day-30 monitoring: In future acquisitions, we will initiate monitoring setup earlier to establish feature monitoring—absent in Khoros—at an early stage, even if incomplete
WorkSmart AI Vision for Legacy Teams: Legacy teams performing untracked, important manual work is a recurring theme. We propose setting up WorkSmart AI Vision for legacy team members to reverse engineer the work that is happening in those teams, work that is not always tracked correctly or at all in their systems.
AI-driven work highlights

> $4.5M in AWS cost savings are the result of pairing AI agents (Claude Code) with BrainLifts, Product Mind context, and CloudFix facts, enabling quicker identification and validation of cost opportunities (DRI: David)
> CloudSense Version consolidation planning - with 40 packages, with 10-15 versions each, plus custom code per customer, each CloudSense customer in a snowflake, and the upgrades were daunting (including for the legacy team). Using Claude Code and product context, we have mapped the compatibility matrix and are now able to define upgrade paths for each customer to the latest version. (DRI: Marcelo, brainlift)
> AI RCAs: moved RCA QC to AI and built an RCA coach (https://rcacoach.xyz) (DRI: David)
> Social Integration Alert Analysis: encoded the “defensive” social tax work that Khoros was doing manually into AI agents that sip through alerts and notifications from social tax and routes problems according to TPM, BU or Support (DRI: Milad)
> AI-driven KT system (summary) streamlines knowledge transfer for acquisitions (DRIs: Pablo, Leo):
> We covered a structured list of topics across Product, Eng and SaaS, processed 500+sessions and created a structured KB available in git for IDE consumption or Ephor.
> TPM got the most value from these sessions, as it guided import and spec writing.
> Engineering value was not fully realized due to late completion, as the work done was largely on import and less so on feature development (that would have been better served by this context)
> SaaS got little value - sessions covered were not complete, and it missed capturing concrete things, such as specific commands and scripts.
> AI-driven core TPM work - fact gathering, problem analysis, decision making and even UX creation is done solely through AI agents (Cursor, Claude Code, and Windsurf), with the bulk of the non-AI work today being around communication and program management.
> CTO Service - TPMs collaborated with BUs on strategic technical decisions, took ownership of and problem-solved cross-functional issues, supported the resolution of key customer escalations, and addressed security & compliance escalations. For example:
> Strategic Technical Decisions
> Khoros: Care-in-a-Box feasibility analysis, Social Tax strategy for 15+ social platform accounts, Brightcove renewal analysis, Pendo subscription capacity review
> IgniteTech: Jive search backend modernization (ElasticSearch→OpenSearch)
> GFI: Kerio Control build infrastructure decision, FaxMaker Online teardown
> Skyvera: AI-based upgrade path analysis
> Cross-functional Problem Ownership
> Khoros: DKIM email delivery operational issues resolution
> IgniteTech: DNN/StreetSmart migration coordination across BU/SaaS/COO teams
> GFI: External contributor framework refinement for dual-team Kerio Control collaboration
> Skyvera: Process streamlining (release, tech debt, handover), Product simplification (deprecated 4 Salesforce packages, 6 ECS clusters, $28K savings)
> Tivian: Cost optimization execution ($486K→$220K/quarter, beat PP target)
> Key Customer Escalations
> IgniteTech: Mercedes-Benz/Porsche Patch Management, CSA professional services security architecture support, WCAG compliance advisory and customer feedback coordination
> Skyvera: Etisalat P1 escalation (non-production environment issues)
> Contently: Multiple RFC compliance support requests
> Security & Compliance Escalations
> Khoros: Certificate Management long-term strategy delivered
> IgniteTech: Amazon Bedrock security issue resolution for Evoq AI
> Skyvera: Telstra CyberGRX Questionnaire (SaaS/TPM portions completed)
> AIPIs - the first take at this problem:
> Khoros Communities: AIPIs use the Khoros data model (well-established and a leader in the space) and the GraphQL APIs exposed through MCP.
> The approach greatly simplifies development, making the work of exposing Level 1 AIPIs for the existing capabilities more about validation and less about development.
> We validated AIPI Level 1 use-cases (LLM caller for AIPIs): Simple Answer + Attribution, Multi-Source Synthesis, No Results
> Khoros Care: Care/K1: AIPIs data structure is based on the Schema.org standard, with semantic AIPIs exposed via MCP. Implementation was put on hold, given the stringent defense-type priorities, but can resume

Q3 BU Kanban Goals (Orders)
Customer
Kanban Business Objective

BU
Order
Product
Goal
End of Quarter
Skyvera
1L
Kandy
Commit: Support secondary AS for etisalat to enable 100k+ domains
done
Commit: High priority escalations and backlog
done
Commit: Support Safe Call feature for Etisalat
done
1L
Cloudsense
Commit: Deliver critical functionality for R38 Version: 6 journeys + Bulk order
NOT done
Commit: Deliver 15 backlog items required by customers
done
New: Deliver Telstra CyberGRX Questionnaire
done
Commit: Cloudsense Disaster Recovery
done
IgniteTech
2L
Jive
Feature Strategy: Jive Unity
Commit: Release the outcome of Jive Unity as Jive 13.
done
Feature Strategy: Jive Unity
Commit: Migrate all customers currently using Jive Cloud to Jive 13 in new Jive Unity UAT environment.
done
Feature Strategy: Jive Dawn
Commit: Deliver a new user interface with 3 core Jive user journeys (defined in feature strategy) to a small group of customers with early access.
done
Feature Strategy: Jive Compass
Commit: Create e2e tests covering core features of Jive (defined in feature strategy), using a modern framework
done
Feature Strategy: Jive Patch Management
Stretch: Support customers to perform minor upgrades through simplifying the patch process and separating security upgrades from functionality changes
canceled
9L
Khoros Communities (incl. Aurora)
Import Strategy
Commit: Complete the import by EOM August
done
Commit: Complete form customization and search results page features, as required to unblock customer migrations to Aurora
canceled
Commit: Delivering incrementally a foundational AI-PI layer for Communities supporting the AI Vision
done
Commit: Establish and communicate a baseline metric for “reliability”
done
Flow AI
Import Strategy
Commit: Complete the import by EOM August
done
Khoros K1
(incl. Spredfast)
Feature Strategy: Twitter Contingency Plan
Feature Strategy: Twitter Sunset
Commit: Support the business direction of potentially disconnecting X/Twitter by changing the product in a way that enables a graceful transition
done
Import Strategy
Commit: Complete the Care/K1 import by EOM August
done
Import Strategy
Commit: Complete the Spredfast import by EOM August
done
Commit: Remove known blockers that allow PS to migrate customers to K1, consolidate infrastructure and EOL Spredfast - scope TBD
canceled
Commit: Delivering incrementally a foundational AI-PI layer for Care supporting the AI Vision
est. NOT done
Commit: Maintain compatibility for integrated social platforms
done
Khoros (All)
Commit: Upgrade critical dependencies to prevent outages or security incidents - scope TBD
done
Commit: deliver $3.8M/annualized savings
done
GFI
2L + 1S
Kerio Connect
Commit: Improve email security and compliance with DMARC implementation, and provide users with greater control over agent operations to ensure privacy and regulatory alignment.
done
Commit: Ability to disable AppManager agent (GDPR Compliance)
done
Mail Essentials
Commit: Optimize spam filtering accuracy while improving delivery of legitimate emails through enhanced greylisting controls.
done
Kerio Control
Commit: dynamic IP groups based on Clearview/ Exinda's Application groups.
done
Commit:ability to change “limit per service” number of connections
done
Commit: Hardware accelerated AES Tunnel
done
AppManager
Commit: Centralize network and security operations by integrating device management, licensing, authentication, updates, and monitoring into a unified platform.
done
Commit: Complete Languard integration
done
Commit: EULA Telemetry
done
Commit: AST Dashboard integration
done
Commit: Enhance security with modern authentication and password policies.
done
Exinda
Commit: Deliver complete visibility into all network traffic, including encrypted (HTTPS) sessions, to support advanced traffic analysis and policy decisions.
done
Archiver
Commit: Simplify integration and licensing for both end customers and MSPs through automated directory sync, mailbox tracking, and licensing models.
done
Contently
2S
Contently
Commit: 923 Onboarding
done
Commit: Fill v3 feature gaps
done
New: AI Features - Model upgrade, Outline fact checking, Word count accuracy
done
New: AI Features - Functional Feedback and Agentic flow
done
CloudFix
1L
Various
Commit: Save $500k
done
SaaS
1L
SaaS
Commit: Cost reduction - Save $40k in AWS costs
done
Commit: Save $500k
done
Crossover
2S
Crossover
Commit: Fix critical infrastructure
done
Commit: Improve AI and BrainLift detection for WorkSmart
done
JigTree

- Tivian
  Commit: Get AWS cost to $267,471/quarter
  done

Next Quarter Plan
Deliver Committed Q4 Goals: starting the quarter with 56 goals and aiming to achieve 95% on-time delivery for the committed quarterly goal
Improve Core Competencies (competencies map); highlights:
Standardized Imports: the focus will be on improving the framework based on Khoros learnings (DRI: Ben)
Cost Optimization: will continue to evolve as we deliver the committed $3.6M in annualized savings
End-to-end AI agents: we have ordered one Kanban and are teaming up with Eng to deliver working end-to-end AI agents capable of doing work units on top of our old, messy, huge enterprise software codebases. This is not about building from scratch, but about leveraging the best AI agents with proper context engineering and brainlifts.
Stack Upgrades Agent: the Q4 focus is
Moving the engineering & product work that Khoros tagged as “social tax” to AI with agents that handle Khoros codebase updates required by Social Platform API deprecations or evolutions. The definition of success is in the reduction of required effort and thus cost (DRI: Pablo)
Simplifying hairy stack upgrades for frameworks with complex upgrade paths across versions that are 10 years apart - case in subject are stack upgrades on Ignite Config (DRI: Ben)
Accessibility Fixes Agent: while not sexy, this is a common and tedious problem across all products - new regulations require accessibility changes that range in complexity from low to high. This is a concrete problem to solve for Khoros and handy for other products in the portfolio of future acquisitions (DRI: Pablo)
CostCop: AI agent that enables TPMs to stay on top of AWS budgets and identify variations, preventing the common case of realizing that products are over budget at the very end of the quarter (DRI: David)
Proposal: Incorporate CloudFix into the TPM CO service: Although the product is no longer actively sold, CloudFix remains a core part of the internal CO strategy.
Fact: 50% of the Q3 savings on Khoros came from TPM cost insights turned productized in CloudFix finders.
How it works: CloudFix finders serve as the flashlight for cost smells, feeding inputs into AI agents, while fixers automate savings that do not require code changes. CloudFix cannot become a stale product, as that will limit our ability to cut costs.
Ask: CloudFix to be owned by TPM and serve as a CO tool. Development would be funded by CO Kanban orders having the goal to enable actual savings at a 3x multiple (enable $ 3 per year of savings by spending $ 1 per quarter). Note: some finders have automated fixers, others are delivered
Q4 BU Kanban Goals (Orders)
Risks to the plan:
Three goals on Khoros start the quarter with a clear direction but lack a defined objective and scope. We are working on concrete proposals or inputs that will enable the BU to make decisions and align with customers.
Customer
Kanban Business Objective
BU
Order
Product
Goal
GFI
2L+1S
AppManager
Commit: GFI Helpdesk integration with AppManager
Commit: Languard Integration with AppManager (Cont)
Commit: Address scalability, consistency and stability issues in AppManager by rearchitecting the application
Kerio Connect
Commit: KOFF: Create web add-in for new Outlook, introduce extended caching
Commit: RFC 8058 Compliance
Commit: Exchange Migration Tool support for exchange 2016 and 2019
Commit: KOFF: Provide caching controls and configuration capabilities in Web and COM Addin
Kerio Control
Commit: Add 10GB speed option in the UI.
Commit: Display the most and recently used firewall rules
Commit: Enhance system stability, security, and operational efficiency by addressing excessive change logs, limits based on bandwidth and connections, and shield matrix white-list
MailEssentials
Commit: Prevent mismatches with changing sender IPs, MailEssentials should allow users to configure greylisting to consider only the sender's domain and not the IP address.
Commit: User-friendly method for SMTP server, aiming to reduce current common misconfigurations
Commit: Implement DMARC as the final DNS-based check to complement its existing SPF and DKIM capabilities
Commit: Exchange SE support
Exinda
Commit: Targeted improvements on the AI wizard in Exinda (remembering user input, ability to directly assign policies to virtual circuits, and warning about non-existent applications)
Languard
Commit: Automate refresh for vulnerability database update process.
Commit: Upgrade SDK to address WAN agents' stability issues
Commit: Fix for agents' expired license key issues
IgniteTech
2L
Jive
Commit: Prod2 Feature Strategy - IgniteTech:Jive - Jive Unity

- All customers migrated to pre-production environment, excluding customer actions or integrations.
- For customers scheduled by arrangement before EOW46, full migration to pre-production including integrations.
- Internal instances (Thrive, Brewspace, Aurea51, Worx, Latest, Latest EU) production migration completed.
- Fix issues with Search backend and EAE.
  Commit: Prod2 Feature Strategy - IgniteTech:Jive - Jive Dawn
  Provide materials for the BU sell-design-build approach:
- Design mockups (Figma) and demos (Lovable or similar) for modern UI and reimagined Jive UX.
- Partial implementation of new UI connected to Thrive backend.
- Overview of SDK integration approach.
- Demo of porting a plugin to the SDK approach.
  Commit: Prod2 Feature Strategy - IgniteTech:Jive - Jive Patch Management
- Implement the flexible patch and dependency management solution defined in Q3.
- Make it available to customers.
  DNN
  Commit: Release Evoq 10
- Integrate, test and release the BU contribution to upgrade Evoq from DNN 9 to DNN 10.
- Verify Evoq AI functionality in the new version.
- Fix any Evoq AI output quality issues.
  N/A
  StreetSmart + DNN
  Commit: Migrate multiple VM instances from TeraSky to AWS, in conjunction with BU
  Khoros
  3L + 1S
  Communities
  Commit: Fix 100 high-severity accessibility issues reported by customers to EOQ3
  Khoros Communities Accessibility
  Commit: Fix 5 security vulnerabilities reported by customers by EOQ3
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - Q4-25 Security Fixes
  Migrate >=2 customers to a managed solution to replace legacy homegrown bin-packing.
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - Replace Homegrown Host Management Solution
  Commit: Fix out-of-memory errors in Aurora.
  Commit: Long-term solution for community certificate renewal/management
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - Certificate Management Long-term Strategy
  Commit: Fix Firehose reliability/stability issues.
  Stretch: Define long-term strategy - completeness of events and role in the AI ecosystem
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - Improve Firehose Reliability
  Commit: Represent outage, response and health metrics on a reliability dashboard
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - Define Site Reliability Metrics & Strategy
  Commit: Finish and release the Automation and Rule Builder for Aurora
  Prod2 Feature Strategy - IgniteTech:Khoro Communities - Rule Builder
  Commit: Create a comprehensive comparison between Analytics in Khoros Classic and Aurora
  Commit: Improve and Productionize GraphQL AIPI.
  Prod2 Feature Strategy - IgniteTech:Khoros Communities - AIPI
  1M
  K1
  Commit: Make customer General Motors successful in using K1 for Marketing use cases (TBD - customer feedback required to scope it)
  Prod2 Feature Strategy - IgniteTech:Khoros - Khoros - K1 product consolidation
  Prod2 Feature Strategy - IgniteTech: K1 analytics v2 - Analytics v2
  Commit: Social Tax - fix issues based on impact timeline
  Commit: Support 16kB memory page size for Android apps + API version.
  Prod2 Mini Spec - IgniteTech:Mobile updates - 16KB memory size update and API version
  Stretch: Complete Polychat feature - manage conversations during authentication workflows.
  2L
  All Khoros
  Commit: Khoros has no bugs older than 7 days
  3L
  Commit: Deliver $3M in annualized AWS cost savings
  CloudFix
  1L
  CloudFix
  Commit: Launch AWS Marketplace with tiered pricing model
  Commit: Deploy validator system tracking actual vs estimated savings
  Commit: Deliver $500k annualized savings
  SaaS
  1M
  All
  Commit: Deliver 600k in annualized savings
  Contently
  1S
  Contently
  Commit: 2 Customer use cases (brand voice driven, content refresh)
  Commit: Enable programmatic access to the agentic AI Content Writer
  Skyvera
  1S
  Lithium
  Commit: Expanding External Condition Attributes Capacity for ALTAN REDES Mexico
  1S
  Kandy
  Commit: Stack Upgrades
  Commit: Geoblocking for WebRTC (Mobile and Desktop)
  1L (Eng Only)
  Commit: Deliver AS2+CoreSBC deployment for Etisalat
  1L
  CloudSense
  Commit: R38 Baseline Versions with Media, Telco1 and Standard Telco baselines
  Commit: Cloudsense Stability improvements across 6 services
  Commit: Stack Upgrades and SOC audit improvements
  JigTree
  1L
  Kayako
  Commit: Upgrade Froala to 2.9
  Tivian DXI
  Commit: Export the Unipark customer base
  AdvocateHub
  Commit: Reduce costs of Analytics platform by at least $80k / yr
  Messenger
  Commit: Java 17 with Eclipse
  Crossover
  1M
  Crossover
  Commit: Enable WorkSmart to be the source of truth for active users needing access to company resources
  Commit: Deliver functional WorkSmart AI Vision use-cases for engineering & support (scope TBD - pending BU)
