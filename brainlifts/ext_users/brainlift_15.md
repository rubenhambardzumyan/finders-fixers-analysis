Brainlift on Converting Autogen Core to API

# Serverless API Architecture on AWS: Patterns, Trade-offs, and Proven Strategies

### Owner

Bhanu Mittal ([bhanu.mittal@trilogy.com](mailto:bhanu.mittal@trilogy.com))

### Purpose

To capture, synthesize, and expand knowledge on converting monolithic applications into scalable serverless APIs using AWS infrastructure.

**In scope:** AWS Lambda, serverless architecture patterns, orchestration strategies, VPC networking, cost-performance trade-offs.

**Out of scope:** Non-AWS cloud providers, on-premise deployment strategies.

### DOK4

- Converting monolithic applications to serverless APIs is not about “lifting and shifting” code into Lambda, it’s about decomposing workflows into independently scalable components and embracing serverless constraints as design drivers.

### DOK3

- Infrastructure Constraints Shape Architecture: AWS SAM and service limitations often necessitate practical compromises over ideal architectures.
- Cost-Performance-Simplicity Triangle: Finding the sweet spot between cost, performance, and simplicity is critical in serverless designs.
- Cross-Lambda Delegation Pattern: Splitting VPC and non-VPC Lambdas with delegation preserves both database access and internet connectivity.

### Experts

- [Dr Milan Milanović](https://x.com/milan_milanovic)
  - Shares insights on software engineering and leadership.

## Knowledge Tree

### DOK2

- Lambda VPC Networking Pattern: Use split architecture with delegation to avoid NAT costs while enabling secure DB and internet access.
- Lambda File System Strategy: Design for /tmp usage from the start to avoid filesystem errors.
- Security Group as Firewall: Outbound rules must explicitly cover HTTP and HTTPS for API calls.
- Systematic Lambda Debugging: Address architectural layers sequentially - filesystem, networking, external APIs.
- Hybrid File Transfer Strategy: Small files via base64, large files via signed URLs.
- SQS Fan-out Pattern: Use SQS to parallelize processing and avoid sequential bottlenecks.
- Separation of Concerns Architecture: Assign different network contexts to specialized Lambdas to avoid trade-offs between security and connectivity.

### DOK1

- Lambda /var/task is read-only; /tmp is writable with 512MB limit.
- Lambda timeout maximum: 15 minutes (hard AWS limit).
- Lambda cold starts can cause >300s delays for heavy imports.
- AWS SAM cannot reference external S3 buckets in event triggers.
- Lambda response payload limit: 6MB synchronous, 256KB asynchronous.
- Security groups require explicit outbound rules for ports 80 & 443.
- Base64 encoding adds ~33% overhead to file size.
- VPC Lambda functions lose internet access without NAT or VPC endpoints.
- MySQL connection pool size for Lambda should be 1 to prevent exhaustion.
- VPC Endpoints are ~$7.75/month vs NAT Gateway ~$45/month.
