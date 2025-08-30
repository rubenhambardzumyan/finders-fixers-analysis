# Core Principles of Production Database Design & Operation [WIP]

**Owner:** Yashar Heidarnezhad, Sergio Tomas
**Assessment Date:** 2025-08-30

---

## Purpose Statement

### Issue 1: Scope Boundaries Need Clarification

#### Feedback

Your Purpose Statement mentions being "bounded to initial schema design, indexing strategy, and core operational monitoring" while excluding "advanced query optimization or database-specific tuning." However, the line between "core" and "advanced" optimization isn't clearly defined, which could lead to scope creep.

#### Coaching

[BrainLift 110: Pick the BrainLift You Need to Create](https://coach.crossover.com/curriculum)

Define specific boundaries with examples: "In scope: Index strategy for tables >1M rows. Out of scope: Query plan analysis, vendor-specific configuration tuning." This prevents confusion about what constitutes "advanced" optimization.

### Issue 2: Success Metrics Need Quantification

#### Feedback

You mention ensuring systems "meet target SLOs for performance and reliability" but don't specify what those targets should be. Without concrete metrics, it's impossible to measure whether this BrainLift achieves its purpose.

#### Coaching

[BrainLift 110: Pick the BrainLift You Need to Create](https://coach.crossover.com/curriculum)

Add specific SLO targets: "Enable systems to achieve <50ms p95 query latency, 99.9% uptime, <2s database deployment time." These concrete goals make success measurable and actionable.

## Experts

### Martin Kleppmann

#### Feedback

Your expert profile for Kleppmann is comprehensive, including credentials, viewpoints, and starter content. The connection between his distributed systems expertise and your database design principles is well-established.

#### Coaching

[BrainLift 121: Building Your Expert Network](https://coach.crossover.com/curriculum)

No issues found! Your expert curation provides clear learning paths and establishes why Kleppmann's perspective is relevant to your database design principles.

### Markus Winand

#### Feedback

Winand's inclusion as the "SQL Performance Explained" author directly aligns with your indexing and query performance focus. The practical, actionable nature of his work supports your operational emphasis.

#### Coaching

[BrainLift 121: Building Your Expert Network](https://coach.crossover.com/curriculum)

No issues found! Winand's expertise directly supports your SPOVs about indexing strategy and provides practical implementation guidance for your principles.

## DOK1 Facts

### Database Monitoring Metrics

#### Feedback

Your facts about the "four golden signals" and Amazon RDS Performance Insights provide solid foundation metrics. The specific mention of db.load above vCPU count as a performance indicator is actionable and measurable.

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

No issues found! These monitoring facts provide concrete, implementation-ready guidance that teams can immediately apply to their database operations.

## DOK2 Facts

### SLO Definition Framework

#### Feedback

Your DOK2 summary effectively synthesizes the four golden signals into practical database SLO implementation. The emphasis on p95/p99 latency over averages demonstrates sophisticated understanding of user impact measurement.

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

No issues found! Your SLO framework summary bridges theoretical monitoring concepts with practical implementation steps, enabling teams to create meaningful reliability targets.

### Index Trade-offs Summary

#### Feedback

Your DOK2 summary about indexes being a "trade-off where we earn performance on specific queries at the cost of making related writes slower" is accurate but could be more specific about when this trade-off becomes problematic.

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

Add quantitative guidance: "Indexes become counterproductive when write operations exceed 60% of total database load" or similar thresholds. This makes the trade-off analysis actionable.

## DOK3 Insight

### Write Speed Impact

#### Feedback

Your insight that "adding too many indexes can significantly impact write speeds, which is especially bad if the table being indexed has a high write ratio" is valuable but needs more supporting data to be compelling.

#### Coaching

[BrainLift 200: Deriving DOK3 Insights from Patterns](https://coach.crossover.com/curriculum)

Strengthen with specific metrics: "Each additional index reduces write performance by 5-15% for high-write tables (>1000 writes/minute)." Provide the quantitative foundation that makes this insight actionable.

## DOK4 SPOVs

### Preemptive Index Restriction

#### Feedback

Your SPOV that "we don't add unnecessary preemptive indexes" is practical and directly addresses common over-optimization problems. However, it needs clearer criteria for determining when indexes are "really needed."

#### Coaching

[BrainLift 201: Building DOK4 SPOVs That Stand Out](https://coach.crossover.com/curriculum)

Add decision criteria: "Add indexes only when query latency exceeds 100ms or when query frequency exceeds 1000/hour." Give teams specific thresholds for index decisions rather than subjective judgments.

### Single Source of Truth Principle

#### Feedback

Your SPOV about not duplicating information maintains database integrity, but the exception handling ("other parties or services can store calculated values") could lead to confusion about when duplication is acceptable.

#### Coaching

[BrainLift 201: Building DOK4 SPOVs That Stand Out](https://coach.crossover.com/curriculum)

Clarify the boundary: "Data duplication is acceptable only across service boundaries with explicit ownership contracts. Within a single service, maintain strict single source of truth." This prevents misinterpretation.

---