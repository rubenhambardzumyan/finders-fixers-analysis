# Serverless API Architecture on AWS: Patterns, Trade-offs, and Proven Strategies

**Owner:** Bhanu Mittal
**Assessment Date:** 2025-08-29

---

## Purpose Statement

### Issue 1: Vague Problem Definition

#### Feedback

The purpose states "capture, synthesize, and expand knowledge" but doesn't identify the specific problem being solved. What failures occur without this expertise? What metrics improve when teams have this knowledge?

#### Coaching

Reframe as a measurable problem: "Teams waste 80% of Lambda costs on NAT gateways and face 40% failure rates during monolith-to-serverless migrations." This justifies expertise beyond AWS documentation.

### Issue 2: No Measurable Outcomes

#### Feedback

The purpose lacks specific metrics or targets. "Scalable serverless APIs" is a goal, not a measurable outcome. Without metrics, you can't validate if this BrainLift achieves its purpose.

#### Coaching

Add three metrics: 1) Reduce serverless migration time from 6 months to 2 months, 2) Cut Lambda costs by 60% through VPC optimization, 3) Achieve 99.9% API availability. Track these to prove value.

## Experts

### Dr Milan Milanović

### Issue 1: Insufficient Expert Details

#### Feedback

The expert entry only mentions "shares insights on software engineering" without explaining his specific views on serverless, what you agree/disagree with, or why he's relevant to AWS Lambda patterns.

#### Coaching

Expand with specifics: "Milan advocates for event-driven architectures (agree) but promotes microservices over serverless (disagree - serverless reduces operational overhead by 70%)." This shows critical engagement.

### Issue 2: Single Expert Echo Chamber

#### Feedback

Having only one expert creates an echo chamber. Where are the AWS architects, serverless critics, or cost optimization specialists who would challenge your views?

#### Coaching

Add three expert categories: 1) AWS serverless architects (Werner Vogels, Eric Johnson), 2) Serverless critics (DHH, Kelsey Hightower), 3) FinOps specialists for cost perspectives. Diverse views sharpen SPOVs.

## DOK1 Facts

### Lambda /var/task is read-only; /tmp is writable with 512MB limit

### Issue 1: Missing Source Attribution

#### Feedback

All DOK1 facts lack source attribution. These appear to be from memory or experience rather than verifiable external sources, making them impossible to validate or update.

#### Coaching

Add sources: "Lambda /tmp has 512MB limit (AWS Lambda Limits Documentation, 2024)" or "VPC Endpoints cost $7.75/month (AWS Pricing Calculator, Q1 2024)." This ensures facts remain current.

## DOK2 Summaries

### Lambda VPC Networking Pattern

### Issue 1: Missing Causal Explanation

#### Feedback

The summary states to "use split architecture" but doesn't explain WHY this pattern works or HOW it solves the internet access problem. It's a prescription without diagnosis.

#### Coaching

Explain the mechanism: "Split architecture works because Lambda's ENI attachment to VPC blocks internet routing - delegation bypasses this by keeping internet-facing functions outside VPC while maintaining secure DB access through internal invocation."

## DOK3 Insights

### Infrastructure Constraints Shape Architecture

### Issue 1: Too Obvious

#### Feedback

"Constraints shape architecture" is a truism in any engineering domain. This isn't a surprising pattern or controversial observation that advances understanding.

#### Coaching

Make it counterintuitive: "AWS constraints are features, not bugs - embracing Lambda's 15-minute limit forces better decomposition than unlimited compute would allow." This challenges the "constraints are bad" assumption.

### Cost-Performance-Simplicity Triangle

### Issue 1: Generic Trade-off Statement

#### Feedback

Every engineering decision involves trade-offs between cost, performance, and simplicity. This insight doesn't reveal anything specific to serverless or provide actionable guidance.

#### Coaching

Be specific: "In serverless, simplicity beats performance 80% of the time - a 200ms slower Lambda that's easy to debug saves more money than a complex 50ms optimization." This guides actual decisions.

## DOK4 SPOVs

### Converting monolithic applications to serverless APIs

### Issue 1: Not Controversial Enough

#### Feedback

"Decomposing workflows into independently scalable components" is accepted serverless best practice. Any AWS architect would agree. This lacks the spikiness needed for an SPOV.

#### Coaching

Make it spiky: "Never decompose beyond 10 Lambda functions - serverless spaghetti is worse than monolithic lasagna. Better to have one fat Lambda than 50 micro-functions." This forces readers to pick sides.

### Issue 2: No Connection to DOK3 Insights

#### Feedback

The SPOV doesn't reference or build upon any DOK3 insights. Without this grounding, it's an opinion rather than a conclusion drawn from pattern recognition.

#### Coaching

Connect to insights: "Based on my Cost-Performance-Simplicity insight and Cross-Lambda Delegation pattern, I believe monolith decomposition should stop at service boundaries, not function boundaries." This shows reasoning.

### Issue 3: Not Actionable

#### Feedback

"Embracing serverless constraints as design drivers" is philosophical but doesn't guide specific architectural decisions. How does this SPOV change what you build tomorrow?

#### Coaching

Make it actionable: "Start every serverless design with a 15-minute Lambda limit assumption - if your process needs more, redesign with SQS fan-out before considering containers." This drives specific choices.

---