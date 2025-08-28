# Khoros Care Components & Architecture

**Owner:** pankaj.menariya@trilogy.com
**Assessment Date:** 2025-08-28

---

## Purpose Statement

### Issue 1: Missing Measurable Metrics

#### Feedback

The Purpose Statement lacks clear, measurable outcomes with specific metrics. While it mentions 'eliminates guesswork, speeds up onboarding, and reduces build failures,' there are no specific business-related metrics like 'reduces onboarding time by X%' or 'decreases build failure rate from Y% to Z%' that would allow measurement of success.

#### Coaching

Add quantifiable metrics such as "reduce engineer onboarding time from 2 weeks to 3 days" or "decrease CI/CD pipeline failures by 40%." Without metrics, you can't prove this BrainLift works or justify the effort to maintain it.

### Issue 2: Unclear Scope Definition

#### Feedback

The Purpose Statement doesn't clearly define what's in scope and out of scope for this BrainLift domain. It mentions 'care microservices' and 'CI/CD pipeline' but doesn't specify which components, environments, or processes are included versus excluded, creating ambiguity about the BrainLift's boundaries.

#### Coaching

Specify exactly which Care services are covered (list the 15-20 core components) and which are excluded (legacy services, external dependencies, third-party integrations). Clear boundaries prevent scope creep and set proper expectations.

### Issue 3: Unfocused Problem Definition

#### Feedback

The problem definition is too broad and lacks focus on a specific, important problem. It conflates documentation consolidation, onboarding improvement, and AI-driven development decisions into one unclear problem space without establishing which is the primary problem or how they relate strategically.

#### Coaching

Pick one primary problem to solve: either "engineers waste 8 hours per week hunting for correct build commands" OR "AI development decisions lack architectural context." Don't try to solve documentation, onboarding, and AI strategy simultaneously.

## Experts

### Zoltan Szalontai

#### Issue 1: Missing Critical Analysis

#### Feedback

The expert entry lacks explicit notes about what the BrainLift creator agrees with AND disagrees with regarding this expert's views. Only generic 'Key Views' are mentioned without the creator's personal stance or critical evaluation of the expert's perspectives.

#### Coaching

Add specific agreements and disagreements: "I agree with Zoltan's emphasis on AI-human collaboration for debugging complex distributed systems, but disagree with his timeline for full AI automation - Khoros Care's legacy integrations will require human oversight for longer than he anticipates."

#### Issue 2: Missing Why Follow Section

#### Feedback

The 'Why Follow' section is missing - there's no clear explanation of this expert's specific relevance to the BrainLift's purpose or how following this expert contributes to becoming an expert in Khoros Care architecture and CI/CD processes.

#### Coaching

Explain specifically why Zoltan matters for your CI/CD expertise goals: "Follow Zoltan because he architected the current Care service mesh and understands which build patterns scale versus which create technical debt - his insights prevent repeating painful architectural mistakes."

### Carlos Costa

#### Issue 1: Missing Critical Analysis

#### Feedback

The expert entry lacks explicit notes about what the BrainLift creator agrees with AND disagrees with regarding this expert's views. The entry is nearly identical to Zoltan's without demonstrating critical evaluation or personal stance.

#### Coaching

Differentiate Carlos from Zoltan with specific perspectives: "Carlos focuses on operational reliability while Zoltan emphasizes development velocity - I lean toward Carlos's stability-first approach for core Care services but prefer Zoltan's innovation stance for new experimental features."

### Issue 3: Echo Chamber Risk

#### Feedback

The Experts section lacks diversity of perspectives and appears to create an echo chamber. Both experts are from the same organization (Trilogy) and share identical 'Key Views' about AI augmenting rather than replace engineers, providing no contrasting viewpoints or alternative approaches to Care architecture.

#### Coaching

Add external experts who disagree with your internal team's approaches - find microservices critics, DevOps skeptics, or competitors who've solved similar problems differently. Echo chambers produce mediocre expertise.

## DOK1 Facts

### Issue 1: Missing Source Attribution

#### Feedback

Many build command facts lack proper attribution with source links. For example, build commands for components like 'mailman', 'gopher', 'roybean' are presented as facts without linking to specific documentation, repository files, or runbooks that verify these commands.

#### Coaching

Link every build command to its source - Jenkins job definitions, Dockerfile references, or README files. Unverifiable facts become organizational rumors that mislead engineers when commands change.

### Issue 2: Mixing Facts with Interpretations

#### Feedback

Architecture facts often contain subjective interpretations mixed with objective information. For instance, descriptions like 'Function: Named "Gopher" because it "goes for things"' blend factual technical information with interpretive explanations that should be separated into DOK2 summaries.

#### Coaching

Separate pure facts ("Gopher processes webhook events from social media APIs") from interpretations ("Named 'Gopher' because it fetches additional data"). Keep DOK1 purely objective and verifiable.

## DOK2 Summaries

### Issue 1: Missing Causal Logic

#### Feedback

Integration summaries fail to show clear logical connections between facts to explain how/why the architecture works. The summaries list what components do but don't synthesize the underlying facts to explain causal relationships or architectural reasoning.

#### Coaching

Transform component descriptions into cause-effect statements: "BECAUSE Mailman normalizes social platform schemas, IC-Backend can route messages uniformly, BUT this creates a single point of failure that requires careful error handling and circuit breaking patterns."

### Issue 2: Lack of Objective Grounding

#### Feedback

The summary contains subjective interpretations not directly supported by underlying DOK1 facts. Statements about 'significant focus' and design intentions should be grounded in specific architectural documentation or design decision records referenced in the facts.

#### Coaching

Ground every summary claim in specific DOK1 facts. Instead of "significant focus on data flow," reference specific facts like "18 of 25 core services use Kinesis streams for async communication" and explain why this pattern exists.

## DOK3 Insights

### Issue 1: Too Generic and Obvious

#### Feedback

This insight is too generic and obvious rather than surprising or counterintuitive. 'Adding proper documentation for local setup' is a common development practice that doesn't demonstrate strategic thinking or provide a practical rule of thumb based on synthesizing multiple sources.

#### Coaching

Find surprising patterns across your Care components: "Care's complexity isn't in individual services but in the 47 different ways they handle retries - standardizing retry patterns would eliminate 60% of production incidents faster than fixing any single component bug."

### Issue 2: Standard Software Engineering Observations

#### Feedback

The insight about code reviews being critical and JIRA linkage being inconsistent is a standard software development observation that doesn't transcend multiple sources or provide surprising patterns. It lacks the subjective analysis expected from DOK3 insights.

#### Coaching

Connect JIRA discipline to specific Care architecture challenges: "Poor JIRA linkage creates cascading debugging hell because Care's service dependencies change faster than documentation - without ticket trails, fixing routing issues becomes archaeological guesswork."

### Issue 3: Technical Documentation vs Strategic Insights

#### Feedback

While the component insights (IC-Backend, Mailman, Switchboard, Analytics) contain more technical depth, they read more like technical documentation than strategic insights. They don't formulate practical rules of thumb or reveal surprising patterns across multiple sources that help with decision-making.

#### Coaching

Transform technical observations into actionable patterns: "Care services fail in predictable sequences - Mailman errors cascade through Switchboard within 3 minutes, so monitoring Mailman connection pools predicts system-wide failures better than traditional application metrics."

## DOK4 SPOVs

### Issue 1: IC-Backend SPOV Lacks Actionability

#### Feedback

This SPOV lacks actionability beyond a testing recommendation. While it identifies a risk ('single misconfigured persona can silently short-circuit routing graph'), it doesn't provide a clear decision rule or operational framework that guides broader architectural or development decisions.

#### Coaching

Make it a decision framework: "Never deploy persona changes without A/B routing tests in production - persona config is code, and misconfigured routing loses more customer messages than service outages. Treat persona updates with the same deployment rigor as database schema changes."

### Issue 2: Mailman SPOV Needs Better Grounding

#### Feedback

While the stance about APIs being liabilities is more controversial, the SPOV lacks grounding in specific DOK3 insights from this BrainLift. It reads like a general API management principle rather than being supported by the actual insights about Mailman's role in the Care architecture.

#### Coaching

Ground it in your specific Care experience: "Because Care ingests from 12+ social platforms with different rate limits and schema changes, we treat every external API as hostile - build circuit breakers, version mappers, and fallback queues before the first integration, not after the first outage."

### Issue 3: Switchboard SPOV Creates Confusion

#### Feedback

The SPOV conflates queue behavior with product features ('delay tuning and deduplication aren't engineering afterthoughts—they are the product'). This creates confusion about whether it's addressing technical architecture decisions or product positioning, reducing its actionability.

#### Coaching

Clarify the decision framework: "Prioritize queue reliability over new features - customers notice message delays immediately but ignore flashy features if their messages disappear. Every sprint should include queue optimization before feature development."

### Issue 4: Analytics SPOV Too Widely Accepted

#### Feedback

This SPOV is essentially a monitoring best practice presented as controversial stance. The position that 'metrics without traceable instrumentation are a mirage' is widely accepted in observability engineering and doesn't represent new knowledge or a spiky point of view.

#### Coaching

Make it genuinely controversial: "Stop building dashboards, start building decision trees - Care generates 10M+ events daily, but executives need 3 binary decisions: scale up, investigate, or ignore. Raw metrics are procrastination disguised as data-driven decisions."

---