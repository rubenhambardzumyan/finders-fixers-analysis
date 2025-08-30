# Web Extension Development

**Owner:** Denys Yefimenko
**Assessment Date:** 2025-08-30

---

## Purpose Statement

### Issue 1: Missing Problem Context

#### Feedback

Your Purpose Statement mentions establishing "best practices" but doesn't explain what specific problems current web extension development faces. What pain points make existing approaches insufficient? Why is this expertise needed now versus five years ago?

#### Coaching

[BrainLift 110: Pick the BrainLift You Need to Create](https://coach.crossover.com/curriculum)

Start with the problem: "Current web extension development suffers from X, Y, Z specific issues that cost teams weeks of debugging." Then position your expertise as solving these concrete problems, not just capturing generic best practices.

### Issue 2: Success Metrics Absent

#### Feedback

Your Purpose Statement lacks measurable outcomes. How will you know this BrainLift succeeded? What metrics should improve when teams apply your expertise (development time, bug rates, cross-browser compatibility, etc.)?

#### Coaching

[BrainLift 110: Pick the BrainLift You Need to Create](https://coach.crossover.com/curriculum)

Add specific metrics: "Reduce cross-browser debugging time by 70%, eliminate manifest-related deployment failures, achieve 95%+ compatibility across Chrome/Firefox/Safari on first deployment." Make success measurable.

## Experts

### Rob Wu

#### Issue 1: Expertise Utilization Unclear

#### Feedback

You list Rob Wu as a "Chrome extension security & API expert" but don't specify which of his insights shaped your SPOVs or where you might disagree with his approaches. This makes it hard to understand how his expertise influenced your framework.

#### Coaching

[BrainLift 121: Building Your Expert Network](https://coach.crossover.com/curriculum)

Add explicit connections: "Wu's emphasis on security in MV3 aligns with our runtime permissions SPOV. However, we disagree with his X approach and instead advocate Y because..." This shows active engagement with expert perspectives.

### Nathan Bierema

#### Issue 1: Context-Specific Relevance

#### Feedback

Bierema's Redux DevTools experience is relevant, but you don't clarify how his complex stateful UI expertise specifically applies to extension contexts versus regular web apps. The unique challenges of extension Redux usage need clearer connection.

#### Coaching

[BrainLift 121: Building Your Expert Network](https://coach.crossover.com/curriculum)

Specify why DevTools extension patterns are relevant: "Bierema's work on Redux DevTools across extension contexts directly informs our SPOV that Redux should be treated as a cache, not source of truth in extensions."

## DOK1 Facts

### Framework Comparisons

#### Issue 1: Quantitative Benchmarks Missing

#### Feedback

Your facts about frameworks (WXT, Plasmo) mention capabilities but lack performance data or adoption metrics. Which framework performs better for specific use cases? What are the actual build time differences or bundle size impacts?

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

Add measurable comparisons: "WXT builds 40% faster than manual webpack configs" or "Plasmo reduces bundle size by 15% vs custom Vite setups." Make framework choices data-driven, not opinion-based.

## DOK2 Facts

### Extension Architecture Patterns

#### Feedback

Your DOK2 summary of extension contexts (Service Worker, content scripts, page scripts, UI surfaces) provides excellent foundational understanding with clear capability boundaries. This effectively synthesizes the architectural constraints that drive your SPOVs.

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

No issues found! Your architectural summary clearly explains why different contexts exist and how they should interact, providing solid foundation for your technical recommendations.

### Storage as Event Bus Pattern

#### Feedback

Your DOK2 explanation of using storage.onChanged for state fan-out is well-documented and directly supports your SPOV about treating storage as an event bus. The technical rationale is clear and actionable.

#### Coaching

[BrainLift 123: Extracting DOK1 Facts and DOK2 Summaries](https://coach.crossover.com/curriculum)

No issues found! This pattern explanation effectively bridges technical constraints with practical implementation, showing exactly why this approach works better than direct messaging.

## DOK3 Insight

### Cold Start Message Loss

#### Feedback

Your insight about worker spin-up timing causing lost messages is genuinely valuable and addresses a common but poorly understood extension development problem. This directly informs practical architectural decisions.

#### Coaching

[BrainLift 200: Deriving DOK3 Insights from Patterns](https://coach.crossover.com/curriculum)

No issues found! This insight captures a subtle but critical timing issue that many developers encounter but don't understand. Your focus on handshake/retry logic provides actionable solutions.

### Redux as Cache Pattern

#### Feedback

Your insight that "Redux is a cache, not the source of truth" in extensions challenges conventional Redux usage and is well-grounded in extension architecture constraints. However, it could benefit from more specific implementation guidance.

#### Coaching

[BrainLift 200: Deriving DOK3 Insights from Patterns](https://coach.crossover.com/curriculum)

Add concrete examples: "When user clicks X in popup, dispatch command to service worker via runtime.sendMessage, then update Redux store via storage.onChanged subscription." Show the exact flow developers should implement.

## DOK4 SPOVs

### Hand-Edited Manifests as Malpractice

#### Feedback

Your SPOV calling hand-edited manifests "malpractice" is appropriately provocative and well-supported by technical evidence about build fragility. The framework recommendation provides clear action guidance.

#### Coaching

[BrainLift 201: Building DOK4 SPOVs That Stand Out](https://coach.crossover.com/curriculum)

No issues found! This SPOV forces developers to abandon manual approaches and provides specific tooling alternatives. It's both controversial and immediately actionable.

### Page-World Script Boundaries

#### Feedback

Your SPOV about page-world scripts having only one job (hijacking page runtime) provides excellent architectural clarity with specific size limits (<2KB) and use case boundaries. This prevents common misuse patterns.

#### Coaching

[BrainLift 201: Building DOK4 SPOVs That Stand Out](https://coach.crossover.com/curriculum)

No issues found! This SPOV provides both philosophical guidance (why page-world exists) and practical constraints (size, communication patterns) that prevent architectural mistakes.

---