# BrainLift 25 Outcome Report: Using AI in Software Maintenance

**Owner:** Mohammad Azhari  
**Assessment Date:** 2025-09-03

---

## Purpose Statement

### Issue 1: Vague Goals Without Measurable Outcomes

#### Feedback

"Learn the best practices of using AI in daily maintenance work" is a learning objective, not a problem statement with business impact. What maintenance inefficiency costs are you solving? What metrics will improve?

#### Coaching

Rewrite with concrete problems and metrics: "Reduce bug resolution time in production systems from 4 hours to 1 hour using AI-assisted debugging" or "decrease code review cycles by 50% through AI-powered analysis." Define what "best practices" means in measurable terms - faster fixes, fewer regressions, or reduced technical debt.

### Issue 2: Missing Business Context

#### Feedback

No explanation of why this matters to your organization. What's the cost of current maintenance inefficiencies? Which teams benefit? What business outcomes drive this need?

#### Coaching

Add business context: "Each hour of maintenance delay costs $10K in SLA penalties" or "reducing maintenance overhead frees 30% of engineering capacity for feature development." Connect AI adoption to specific business value, not abstract improvement.

## Experts

### Issue 1: Generic AI Thought Leaders

#### Feedback

Your experts (Andrew Ng, Fei-Fei Li, Karpathy) are general AI luminaries, not software maintenance specialists. Their high-level AI perspectives don't translate directly to maintenance-specific challenges.

#### Coaching

Replace with maintenance-focused practitioners: Simon Maple (DevOps maintenance patterns), Michael Feathers (legacy code maintenance), or Kelly Shortridge (production system resilience). You need experts who've actually implemented AI in maintenance contexts, not AI visionaries.

### Issue 2: No Agreement/Disagreement Analysis

#### Feedback

Missing explicit notes on what you agree or disagree with for each expert. This prevents developing your own perspective and creates an echo chamber of accepted wisdom.

#### Coaching

Add your stance: "Agree with Ng's emphasis on practical applications, disagree with his optimism about AI handling complex debugging without human oversight." Show critical analysis, not passive consumption.

### Issue 3: Broken Source Citations

#### Feedback

Citation format is broken with mixed bracketed text like "[Nextotech][+3][CIO Dive]" making sources unverifiable and unprofessional.

#### Coaching

Fix citations properly: "Source: CIO Dive, '11 AI Experts to Follow,' 2024, [link]". Each expert needs clean, verifiable source attribution that readers can actually follow.

## DOK4 SPOVs

### Issue 1: Conventional Wisdom, Not Spiky

#### Feedback

"Engineers should delegate code creation to AI and evolve into high-leverage reviewers" is already mainstream thinking. This isn't controversial or spiky - it's what GitHub Copilot marketing already promotes.

#### Coaching

Develop truly controversial positions: "AI-generated code should be quarantined for 30 days before production deployment - immediate deployment creates invisible technical debt" or "Maintenance teams should deliberately avoid AI for critical path bugs - AI suggestions mask root cause understanding." Challenge accepted practices.

### Issue 2: Disconnected from Maintenance Focus

#### Feedback

Your SPOVs about code generation and test cases are generic AI-in-development positions, not specific to software maintenance challenges.

#### Coaching

Make SPOVs maintenance-specific: "Never use AI to fix production incidents - it optimizes for quick patches over systemic solutions" or "AI should only suggest maintenance changes that reduce code, never add it - complexity reduction trumps feature preservation in legacy systems."

## DOK3 Insights

### Issue 1: Too Broad and Obvious

#### Feedback

"AI Significantly Enhances Automation, But Context and Human Judgment Remain Critical Gaps" is a generic observation everyone already knows. It lacks the surprising pattern recognition that makes insights valuable.

#### Coaching

Develop specific maintenance insights: "AI maintenance suggestions become less reliable after 6 months - model drift means yesterday's fixes become tomorrow's bugs" or "AI excels at fixing symptoms but consistently misses architectural debt - 80% of AI fixes require human refactoring within 3 months."

### Issue 2: No Connection to Knowledge Tree

#### Feedback

Your insights aren't grounded in the facts and summaries from your knowledge tree. They appear to be assumptions rather than patterns discovered through research.

#### Coaching

Connect insights to evidence: "Based on analysis of AI automation tools (Knowledge Area 1), AI-generated test cases catch 90% of regression bugs but miss 100% of performance degradations because they optimize for functional correctness over system behavior."

## Knowledge Tree

### Issue 1: Missing Source Attribution

#### Feedback

All DOK1 facts lack source attribution. "AI-driven tools generate and prioritize software test cases" - according to whom? Which tools? What evidence?

#### Coaching

Add sources to every fact: "GitHub Copilot generates test cases covering 67% of code paths (Source: GitHub Engineering Blog, 2024)" or "Diffblue Cover automatically generates Java unit tests achieving 73% coverage (Source: Diffblue Case Study, Oracle, 2023)."

### Issue 2: Structure Doesn't Follow BrainLift Framework

#### Feedback

Your knowledge tree mixes DOK1 and DOK2 under knowledge areas without proper source organization. The framework requires sources with their facts and summaries, not floating facts without attribution.

#### Coaching

Restructure properly:
```
AI in Automation
├── Source: GitHub Copilot Study 2024
│   ├── DOK1: Generates 40% of code in maintenance PRs
│   ├── DOK1: 73% acceptance rate for bug fixes
│   └── DOK2: AI accelerates simple fixes but struggles with complex interdependencies
```

### Issue 3: Incomplete Knowledge Areas

#### Feedback

Knowledge areas like "AI for Legacy Code Comprehension" have minimal content - just three unsourced facts. This shallow coverage prevents meaningful expertise development.

#### Coaching

Expand each area with multiple sources, proper facts, and synthesis. Add vendor case studies, research papers, and practitioner blogs. Each knowledge area needs at least 5 sources with documented facts and summaries to build real expertise.

## Overall Assessment

### Issue 1: Misplaced Meta-Content

#### Feedback

Including "How Ephore.ai helped me" and "Time Tracking" in your BrainLift confuses the purpose. BrainLifts document expertise, not your learning process or tool experiences.

#### Coaching

Remove meta-content about your learning journey. Focus entirely on the expertise itself - the knowledge, insights, and SPOVs about AI in maintenance. Save process notes in a separate document.

### Fundamental Issue: Generic AI Knowledge vs. Maintenance Expertise

#### Feedback

This BrainLift reads like general AI awareness rather than deep software maintenance expertise. The superficial coverage and lack of maintenance-specific research suggests you're aggregating AI hype rather than building practical maintenance knowledge.

#### Coaching

Choose your path:
1. **Narrow to specific maintenance domain:** Focus on one area like "AI for production incident response" with deep research, real case studies, and specific tooling analysis
2. **Abandon for existing resources:** If you just want general AI knowledge, use existing courses and documentation rather than building a BrainLift

The current approach provides neither general AI expertise nor specific maintenance value.