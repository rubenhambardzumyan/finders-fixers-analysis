# BrainLift 28 Outcome Report: Kandy SBC-AS Configuration Management and Troubleshooting

**Owner:** Rafal Hryniow  
**Assessment Date:** 2025-09-03

---

## Purpose Statement

### Issue 1: Missing Measurable Business Metrics

#### Feedback

Your purpose mentions "prevent project delays" and "resolve SBC configuration issues" but lacks specific metrics. How much delay are you preventing? What's the current vs. target resolution time? Without metrics, you can't demonstrate value.

#### Coaching

Add concrete metrics: "Reduce SBC configuration-related project delays from 2 weeks to 2 days" or "decrease mean time to resolve trunk setup issues from 48 hours to 4 hours." Include business impact like "saving $50K per prevented delay" to justify the expertise investment.

### Issue 2: Knowledge Transfer Goal Isn't Expertise Development

#### Feedback

"Preserve troubleshooting knowledge" and "prevent knowledge silos" are documentation goals, not expertise development. BrainLifts are for developing spiky points of view, not creating knowledge repositories.

#### Coaching

Reframe around expertise: "Develop contrarian approaches to SBC configuration that challenge vendor recommendations" or "Create novel troubleshooting methodologies that outperform standard practices." Focus on developing new knowledge, not preserving existing knowledge.

## Experts

### Issue 1: Names Without Context

#### Feedback

Listed as just names (Neihls Jacobson, Stephen Brown, Phil Karam) without any information about their expertise, main views, or why to follow them. This violates BrainLift requirements for expert documentation.

#### Coaching

Complete each expert entry: "Stephen Brown - Ribbon SBC architect, Main Views: Advocates for centralized PSX routing over distributed IP routing, Why Follow: 15 years implementing carrier-grade SBC deployments, Disagree: His preference for heavy PSX dips adds unnecessary latency." Include links to their blogs, LinkedIn, or publications.

### Issue 2: Missing Diverse Perspectives

#### Feedback

Only three experts, likely all from similar backgrounds. No vendor representatives, no competing viewpoints, no academic perspectives on SIP/SBC architecture.

#### Coaching

Add diverse experts: Kamailio open-source SBC developers (different philosophy), Oracle SBC architects (competing vendor), IETF SIP working group members (standards perspective). Include someone who challenges traditional SBC architecture entirely.

## DOK4 SPOVs

### Issue 1: Operational Observations, Not Spiky Views

#### Feedback

SPOVs like "SBC configuration issues are critical blockers" and "Knowledge concentration creates bottlenecks" are obvious operational truths, not controversial positions that challenge conventional thinking.

#### Coaching

Develop truly spiky views: "SBCs should be eliminated entirely - modern application servers can handle border security better than dedicated appliances" or "Manual SBC configuration is superior to automation because it forces engineers to understand call flows." These are debatable positions that force stance-taking.

### Issue 2: Too Many Scattered SPOVs

#### Feedback

Seven SPOVs covering different topics (configuration, compliance, registration, routing) without coherent theme. SPOVs should build a unified contrarian worldview, not list random observations.

#### Coaching

Focus on 2-3 strong, related SPOVs: "All SBC routing should be username-based, numeric routing is legacy debt" leading to "PSX centralized routing creates more problems than it solves" leading to "Distributed edge routing beats centralized policy servers." Create a coherent alternative vision.

## DOK3 Insights

### Issue 1: Technical Details, Not Pattern Recognition

#### Feedback

Insights like "Zone isolation principles recommend one SIP SIG port per zone" and "Registration flows between SBC and AS involve complex session timers" are technical specifications, not surprising patterns discovered across sources.

#### Coaching

Develop real insights: "SBC failures follow power law distribution - 80% trace to 3 misconfigurations that vendors never document" or "Teams that name trunk groups in lowercase have 50% fewer routing failures than UPPERCASE users." Show non-obvious patterns.

### Issue 2: No Source Grounding

#### Feedback

Insights aren't connected to DOK1/DOK2 foundation. "Username routing versus standard routes" insight appears without evidence from your knowledge tree.

#### Coaching

Connect to sources: "Based on analysis of 500 Ribbon support tickets (DOK1) and UAE routing implementations (DOK2), username routing failures increase exponentially with non-ASCII characters, explaining 60% of emirate-specific routing issues." Show the research trail.

## Knowledge Tree

### Issue 1: Mixed Structure and Incomplete Content

#### Feedback

Knowledge tree mixes different organizational approaches - some areas are topics ("SBC Configuration Fundamentals"), others are facts floating without sources, and Confluence links appear randomly at the end.

#### Coaching

Structure properly:
```
SBC Routing Patterns
├── Source: Ribbon SBC 9.2 Documentation
│   ├── DOK1: PSX dips add 50-200ms latency
│   ├── DOK1: Username routing triggers on first alphabetic character
│   └── DOK2: PSX routing provides flexibility at the cost of performance because...
```

### Issue 2: Facts Without Sources

#### Feedback

"SBC caches REGISTRATION requests" and other facts lack source attribution. These could be assumptions, vendor claims, or discovered patterns - without sources, they're unverifiable.

#### Coaching

Add proper attribution: "SBC caches REGISTRATION requests to prevent SESM overload (Source: Ribbon SBC 7.2 Admin Guide, Chapter 12, page 455)" or "Discovered through packet capture analysis of 1000 registration flows, January 2024 lab testing."

### Issue 3: Key Terms Section Misplaced

#### Feedback

Lines 7-32 contain extensive terminology definitions that should be part of the knowledge tree with proper DOK structure, not floating at the top of the document.

#### Coaching

Move definitions into knowledge tree as DOK1 facts under a "Core Concepts" knowledge area, each with proper source attribution. This isn't a glossary - it's part of your expertise foundation.

## Overall Assessment

### Fundamental Issue: Knowledge Preservation vs. Expertise Development

#### Feedback

This BrainLift reads like a technical documentation project aimed at preserving existing SBC knowledge rather than developing new expertise with spiky points of view. The focus on preventing knowledge loss and capturing siloed information suggests you're creating a wiki, not building expertise.

#### Coaching

Choose your path:
1. **Transform into real expertise BrainLift:** Develop controversial positions about SBC architecture ("SBCs are obsolete, use API gateways instead"), research evidence, build coherent worldview
2. **Convert to technical documentation:** Move this content to Confluence as a proper SBC troubleshooting guide and runbook collection
3. **Narrow to specific expertise:** Focus on one aspect like "UAE-specific SBC routing patterns" where you can develop deep, contrarian expertise

The current mix of knowledge preservation and shallow technical details provides neither good documentation nor valuable expertise.