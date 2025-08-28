CCAB Project Development

- DOK constructs and BrainLift invariants
  - BrainLift structure and organization - Key terms: - Brainlift: core human knowledge data structure - BrainMaxxing: core knowledge creation process - High Level organization - Owner - Muhammad Mutahir Latif - Purpose - Primary Purpose - Enhance understanding of the CCAB (Cloud Charging & Billing) project architecture, implementation, and operational processes to improve development effectiveness and technical decision-making - Specific Areas covered - Export Device Lambda functionality and maintenance stack components - Integration testing methodologies and local development workflows - Cloudformation error handling methodologies and workflows - Out of Scope - CCAB billing algorithm internals - Customer-facing UI components - Pricing strategy and business logic - Non-CCAB related AWS services - General software development concepts not specific to CCAB context - Success Criteria - Ability to independently troubleshoot CCAB export issues - Improved code review effectiveness for CCAB components - Faster onboarding of new team members using this knowledge base - Reduced time to implement new export features - _----------- Depth of Knowledge / DOK starts here ----------_ - Maintenance Stack export Lambda - Purpose - The Purpose of this is to help me in understanding the lambda function for exporting production data - DOK - 1 - Project Overview: The project is an Export Device Lambda function, part of the Maintenance Stack, responsible for exporting provider settings and hierarchical data from the Cloud Charging & Billing system. - Functionality: The Lambda exports data in a format suitable for declarative Java tests or manual DynamoDB loading. - Input Event Format: The Lambda accepts input events in a specific JSON format, including providerId, deviceId, accountId, planIds, isForTests, zipAll, edrsFrom, and edrsTo. - Environment Variables: The Lambda requires environment variables, such as MAIN_TABLE, EDR_TABLE, JOB_TABLE, BUCKET, OUTPUT_PREFIX, and AWS_REGION. - DOK2 - Knowledge Tree - Data Hierarchy: The Lambda exports a hierarchical data structure, including provider configuration, rating groups, field mappings, balance types, device data, account data, plans, and event data records (EDRs). - Export Process: The export process involves compressing data using zlib's DEFLATE algorithm with pre-trained dictionaries and storing it in S3. - Placeholder System: The Lambda implements a placeholder system to handle sensitive data and timestamps, ensuring that exported data can be safely used in test environments. - The datetimes are replaced by placeholders of varying degrees of accuracy. The placeholders contain the offset of the actual time in the data with the reference time. This reference time is then exported as well so that these tests can be loaded into DeclarativeTests > > - Relationships between Components: The Lambda's functionality is connected to various components, such as DynamoDB tables, S3 buckets, and the Cloud Charging & Billing system. - Steps for running various Integration tests - Purpose - Help me in understand the prerequisite steps required for running integration tests - ManualBulkUpload - DOK1 - The bulk upload system is a critical component that allows for batch processing of account, device, and subscription data - The test cases cover various scenarios including: - Basic CRUD operations (Create, Read, Update, Delete) - Validation of input data - Error handling for invalid inputs - Large file processing - Multiple file processing - Nested operations - Cross-account operations - DOK2 – Knowledge Tree: Bulk Upload Testing - Overview: Bulk upload tests stress DynamoDB with large-scale data using DeclarativeTests. - Common Issues Encountered: - Directory confusion for running generators leads to command not found errors. - Output file location and CLI argument mismatches cause missing output and warning messages. - Test discovery issues (wrong Gradle task). - Assertion failures due to missing infrastructure (bulk-upload-\* stack). - Validation failures from schema drift in generated files. - Solutions and Workarounds: - Must run generator from `ccab` directory. - Ignore some CLI warnings; find output in `misc-tools/`. - Use `itest:manualTest` for correct test execution. - Ensure bulk-upload stack is deployed in test environment. - Use custom validation scripts/tests for debugging file syntax. - Update bulk upload generator to match latest schema. - Tooling and Documentation Issues: - Generator lacked up-to-date documentation for usage and output. - Required ad-hoc tools and code inspection for troubleshooting. - Outdated instructions in code comments. - References: -  [https://docs.google.com/document/d/1Pm0sZoTflJFXgpW19_u9zfOtiTWAxmKZlQ7a_Sbt30k/edit?tab=t.0](https://docs.google.com/document/d/1Pm0sZoTflJFXgpW19_u9zfOtiTWAxmKZlQ7a_Sbt30k/edit?tab=t.0) - [Bulk Export README.md](https://github.com/trilogy-group/ccab/tree/staging/itest/itest/src/test/resources/bulk-upload/README.md) - Personal log and troubleshooting notes (see above) - [Bulk upload schema documentation] - Steps for deleting Cloudformation Stacks. - DOK1: Facts About CloudFormation Stack Deletion Issue - Introduction: When dealing with the deployment of environments using CloudFormation stacks created by CDK, one might encounter issues where the stack is not properly deleted during the environment destruction process. This can lead to resources being left behind, causing unintended costs and complexity in managing cloud resources. - Key Facts - Issue Persistence: Despite the destroy environment workflow showing success, the CloudFormation stack may remain undeleted. - Error Messages: Custom resources (e.g., Custom::S3AutoDeleteObjects) can fail to delete, resulting in a DELETE_FAILED state. An example error message includes: This Custom::S3AutoDeleteObjects resource is in a DELETE_FAILED state. - CloudFormation did not receive a response from your Custom Resource. Please check your logs for requestId [0dbefe67-030c-4eac-8f43-003d1184066b]. If you are using the Python cfn-response module, you may need to update your Lambda function code so that CloudFormation can attach the updated version. - Resource Status: The DELETE_FAILED status for custom resources prevents the entire stack from being deleted. - Manual Intervention: Manual steps are required to delete the stack with resource retention, followed by the cleanup of orphaned resources. - Tools and Commands: Utilization of AWS CLI, CloudFormation commands, and the Resource Groups Tagging API is necessary for troubleshooting and resolving the issue. - Diagnostic and Deletion Commands - Listing Failed Resources: The command to list resources in a `DELETE_FAILED` state is: - `aws cloudformation describe-stack-resources --stack-name monitoring-stack-mdvuseast1 --query "StackResources[?ResourceStatus=='DELETE_FAILED'].[LogicalResourceId, ResourceType, ResourceStatusReason]" --output table` - Deleting Stack with Retention: To delete a stack but retain a failed resource, use: - `aws cloudformation delete-stack --stack-name monitoring-stack-mdvuseast1 --retain-resources ec2resourcesbucketAutoDeleteObjectsCustomResource6A4F7895` - DOK2: Analysis and Solution for CloudFormation Stack Deletion Issue - OverviewThe primary reason for stacks not being deleted is often due to custom resources with lifecycles maintained by Lambda functions that do not support the necessary deletion functions. This leads to a `DELETE_FAILED` state, requiring manual intervention for deletion.Steps for Manual Deletion - Identify Failed Resources: Use AWS CLI commands to list resources that failed to delete. - Delete Stack with Retention: Delete the stack while retaining the problematic resources. - Find Orphaned Resources: Utilize the Resource Groups Tagging API to discover resources left behind after stack deletion. - Manually Delete Orphaned Resources: Use specific AWS CLI commands to delete each orphaned resource. - Script for Enumerating Orphaned ResourcesFor projects with multiple stacks, a script can automate the process of scanning for orphaned resources: - bash - ```
    #!/bin/bash

# List of deleted stack names

stacks=(
  engine-app-stack-mgit
  job-processing-mgituseast1
  appsync-api-mgituseast1
  notifier-stack-mgituseast1
  appsync-lambdas-mgituseast1v2
  stateless-stack-mgituseast1
  dynamo-lambdas-mgituseast1v2
  edr-exporter-mgituseast1
  stateful-stack-mgituseast1
  neptune-stack-mgit
  ccab-stack-mgit
)

output_file="orphaned-resources.txt"

> "$output_file"  # Clear or create the file

echo "Scanning for orphaned resources..."

for stack in "${stacks[@]}"; do
  echo "Processing stack: $stack"
  aws resourcegroupstaggingapi get-resources \
    --tag-filters Key=aws:cloudformation:stack-name,Values=$stack \
    --query "ResourceTagMappingList[].ResourceARN" \
    --output text >> "$output_file"
done

# Add quotes and remove duplicates

sort -u "$output_file" | sed 's/^/"/;s/$/"/' > temp && mv temp "$output_file"

echo "Done. Orphaned resource ARNs saved to: $output_file"

```
          - Best Practices and Lessons Learned
            - Verify Stack Deletions: Always check the AWS console after environment destruction to ensure all stacks and resources are properly deleted.
            - Improve Workflow Outputs: Modify workflows to clearly report any failures or partial successes during stack deletion.
      - CCAB Alarm-to-Component Troubleshooting Matrix Description
        - DOK1: Facts
          - CCAB uses standard AWS ALB metrics for charge engine monitoring, specifically tracking HTTPCode_Target_4XX_Count and HTTPCode_Target_5XX_Count to detect application-level errors and server failures
          - CCAB uses EventBridge rules to capture AWS Health events and routes them to CloudWatch Logs at `/aws/events/health-events-{env}`, where metric filters parse JSON log patterns to count specific event types
        - DOK2: Technical details
          - Health event monitoring uses JSON path filtering in metric filters - `$.detail.eventTypeCode = "AWS_ABUSE_NOTIFICATION"` for abuse events and `$.detail.eventTypeCategory = "issue"` for general health issues. These filters increment counters that trigger alarms when any matching event occurs (threshold >= 1)
      - DOK4 - SPOV
        - Unlocking Organizational Memory and Expertise
          - The conventional approach to documentation focuses on clarity, completeness, and ease of use, but overlooks its potential as a tool for organizational memory and risk management. Documentation should be treated as a strategic asset, encoding the hard-won scars of senior engineers and capturing the nuances of past failures and lessons learned. This approach acknowledges that documentation is not just for new team members, but for the organization's future self, ensuring that critical knowledge is retained even as personnel change. Key aspects of this approach include:
          - Capturing the "why" behind design decisions, to prevent future teams from unknowingly undoing critical fixes or optimizations.
          - Documenting past failures and near-misses, to inform future risk assessments and prevent recurrence.
          - Surfacing non-obvious, high-leverage lessons, to make documentation an asset that teaches valuable, non-Googleable insights.
          - By shifting the focus of documentation from basic onboarding to encoding expert-level war stories, teams can unlock the true value of their documentation. This means moving beyond checklists and feature guides, and instead creating docs that share the rare, expert-level knowledge that even veterans forget over time. Good documentation should actively weaponize senior engineers' hard-won scars, using them to inform and improve future decision-making, and ultimately becoming a key driver of organizational success.
        - Deletion as a measure of automation success
          - Deletion is a separate process from creation, often neglected.
          - If CloudFormation can't reliably delete what it creates, you don't have Infrastructure-as-Code.
          - Deletion success rate measures automation maturity.
          - Custom resources indicate CloudFormation failed.
          - Real automation means deletion works as reliably as creation.
          - Teams that can't destroy infrastructure cleanly have technical debt factories.
          - Measure success by what gets cleanly removed, not what gets provisioned.
          - Treat every custom resource as a red flag that needs justification.
          - Build post-destroy validation before celebrating deployment automation.
          - If your infrastructure can't be deleted as easily as it's created, you're doing Infrastructure-as-Wishful-Thinking.
          - Prioritize deletion and documentation over provisioning speed.
          - Documentation should capture the "why" behind deletion decisions and past failures.
          - Deletion failures should be documented to inform future risk assessments.
        - Cloud providers are failing developers by not solving cross-service consistency—stop forcing us into brittle Saga patterns, start building native ACID transactions across services.
          - Reference "DOK3-Multiple Entities in Cloud sync", systems having to perform background checks on two or more service states sync is a waste of resource and compute cycles.
          - SAGA patterns are provided in some services of AWS and Azure but they do not meet the requirement
      - DOK3 - Insights
        - Truth About Documentation
          - For a project of this scale there should be a central repository of documentation, where a new engineer on the project can look into the various issues and problems that are faced when running things for the first time. Documentation is not just about documenting what works, but also about exposing what breaks? The industry lie is that documentation should only cover the happy path. In reality, real value lies in surfacing how things go wrong.
            - Key Insights
              - Documentation is useless if it only covers the happy path.
              - Undocumented failure modes cost more dev time than missing features.
              - AI assistants are especially vulnerable to poorly documented failure modes.
              - If your docs don’t list what breaks, how, and how to spot it—you’re not helping engineers, you’re slowing them down (and AI can’t help either).
              - Documentation that only covers success scenarios is worse than no documentation at all—it creates false confidence that leads to deeper rabbit holes.
              - Comprehensive documentation means covering every way things break, not every feature.
            - Evidence
              - Bulk upload: Docs say run in misc-tools/—fails; actually must run in ccab/.
              - Generator: Unclear warnings look like errors—no doc tells you which to ignore.
              - Outdated schemas: Docs never mention planVersionId change; hours wasted chasing silent failures.
              - Test failures: Error output tells you nothing; custom test scripts needed to find root cause.
              - Bulk upload generator docs omit critical directory information.
              - Generator warnings resemble errors but should be ignored.
              - Deprecated fields cause validation failures with unhelpful error messages.
            - Why This Matters
              - New engineers waste 80% of setup time on undocumented failure modes, not missing features.
              - AI systems can't distinguish "ignore this warning" from "fix this error" without explicit guidance.
              - Perfect-world docs create false confidence that leads to deeper debugging holes.
            - Recommendations
              - Document warnings to ignore.
              - Include common failure scenarios in setup instructions.
              - Add "what probably broke" to every setup step.
              - Make error decision trees explicit.
              - Write docs assuming Murphy's Law, not best-case scenarios.
            - Conclusion
              - Documentation must prioritize failure modes to be useful. Stop documenting the 10% of time things work perfectly. Document the 90% of time they don't. By doing so, you'll create a truly comprehensive and helpful documentation that saves time and reduces frustration for engineers and AI systems alike. Your README should have more "what went wrong" sections than "how to use" sections.
        - CloudFormation Stack Deletion Issues
          - Overview
            - CloudFormation stack deletions can be problematic, especially with custom resources. Here are the key issues and best practices:
          - Key Issues
            - Custom resources can cause DELETE_FAILED states and leave orphaned resources behind
            - Automation pipelines may not catch partial stack failures, leading to hidden costs and complexity
            - Manual intervention is often required to resolve these issues
            - Orphaned resources (e.g., log groups, S3 buckets) can accumulate over time if not proactively found and deleted
          - Root Cause
            - The problem stems from:
            - CDK abstractions not handling custom resource lifecycles properly, especially during deletion
            - Custom resources with Lambda backends often lacking proper DELETE operation support
            - Automation pipelines reporting "success" even when resources fail to delete
          - Best Practices
            - Verify deletion manually: Ensure everything is properly deleted
            - Improve workflow outputs: Clearly report failures or partial successes
            - Document manual processes: Troubleshoot and resolve stack deletion issues
            - Regularly review cloud resources: Clean up orphaned resources
            - Audit Lambda custom resources: Check for DELETE operation support before deployment
            - Build post-destroy validation: Into automation pipelines to catch partial failures
          - Why This Matters
            - Manual cleanup becomes the norm instead of the exception
            - Resource sprawl leads to unexpected AWS bills
            - Team velocity slows down due to cleanup overhead
            - Knowledge gets trapped in manual processes instead of being automated
          - Takeaway
            - To manage CloudFormation stacks effectively, it's crucial to:
            - Understand the nuances of custom resource deletion
            - Implement robust error handling and post-destroy validation
            - Plan for partial failures, not just happy paths
            - Make resource cleanup failures explicit, not hidden
            - Document the manual cleanup process as a first-class workflow, not an afterthought
          - By following these best practices, teams can reduce manual cleanup, prevent resource sprawl, and improve infrastructure-as-code workflow reliability.
        - Multiple Entities in Cloud sync
          - As shown in "DOK2- Multiple entities synchronization", when a system when performing update on a  logical object that is written in two different cloud entities, then there must be a background process that should be checking if any of the entity has become out of sync
      - *----------  BRIGHT LINE.  Above this is based on the owner's opinion and expertise.  Below this is based on the external flow of information  ----------*
      - Experts
        - Microsoft Azure. Saga Patterns. [https://learn.microsoft.com/en-us/azure/architecture/patterns/saga](https://learn.microsoft.com/en-us/azure/architecture/patterns/saga)
      - DOK2 - Knowledge Tree
        - DOK2 -summaries
        - DOK1 - facts
        - links to original sources
      - *----------  BRIGHT LINE.  Above this is the BrainLift, the user creates this without AI.  Below this is not the BrainLift, it is however the user gets sources from the flow of external information ----------*
      - BrainMaxxing, other feeds, etc.
  -
  -
```

CCAB Project Development

- DOK constructs and BrainLift invariants
  - BrainLift structure and organization - Key terms: - Brainlift: core human knowledge data structure - BrainMaxxing: core knowledge creation process - High Level organization - Owner - Muhammad Mutahir Latif - Purpose - Primary Purpose - Enhance understanding of the CCAB (Cloud Charging & Billing) project architecture, implementation, and operational processes to improve development effectiveness and technical decision-making - Specific Areas covered - Export Device Lambda functionality and maintenance stack components - Integration testing methodologies and local development workflows - Cloudformation error handling methodologies and workflows - Out of Scope - CCAB billing algorithm internals - Customer-facing UI components - Pricing strategy and business logic - Non-CCAB related AWS services - General software development concepts not specific to CCAB context - Success Criteria - Ability to independently troubleshoot CCAB export issues - Improved code review effectiveness for CCAB components - Faster onboarding of new team members using this knowledge base - Reduced time to implement new export features - _----------- Depth of Knowledge / DOK starts here ----------_ - Maintenance Stack export Lambda - Purpose - The Purpose of this is to help me in understanding the lambda function for exporting production data - DOK - 1 - Project Overview: The project is an Export Device Lambda function, part of the Maintenance Stack, responsible for exporting provider settings and hierarchical data from the Cloud Charging & Billing system. - Functionality: The Lambda exports data in a format suitable for declarative Java tests or manual DynamoDB loading. - Input Event Format: The Lambda accepts input events in a specific JSON format, including providerId, deviceId, accountId, planIds, isForTests, zipAll, edrsFrom, and edrsTo. - Environment Variables: The Lambda requires environment variables, such as MAIN_TABLE, EDR_TABLE, JOB_TABLE, BUCKET, OUTPUT_PREFIX, and AWS_REGION. - DOK2 - Knowledge Tree - Data Hierarchy: The Lambda exports a hierarchical data structure, including provider configuration, rating groups, field mappings, balance types, device data, account data, plans, and event data records (EDRs). - Export Process: The export process involves compressing data using zlib's DEFLATE algorithm with pre-trained dictionaries and storing it in S3. - Placeholder System: The Lambda implements a placeholder system to handle sensitive data and timestamps, ensuring that exported data can be safely used in test environments. - The datetimes are replaced by placeholders of varying degrees of accuracy. The placeholders contain the offset of the actual time in the data with the reference time. This reference time is then exported as well so that these tests can be loaded into DeclarativeTests > > - Relationships between Components: The Lambda's functionality is connected to various components, such as DynamoDB tables, S3 buckets, and the Cloud Charging & Billing system. - Steps for running various Integration tests - Purpose - Help me in understand the prerequisite steps required for running integration tests - ManualBulkUpload - DOK1 - The bulk upload system is a critical component that allows for batch processing of account, device, and subscription data - The test cases cover various scenarios including: - Basic CRUD operations (Create, Read, Update, Delete) - Validation of input data - Error handling for invalid inputs - Large file processing - Multiple file processing - Nested operations - Cross-account operations - DOK2 – Knowledge Tree: Bulk Upload Testing - Overview: Bulk upload tests stress DynamoDB with large-scale data using DeclarativeTests. - Common Issues Encountered: - Directory confusion for running generators leads to command not found errors. - Output file location and CLI argument mismatches cause missing output and warning messages. - Test discovery issues (wrong Gradle task). - Assertion failures due to missing infrastructure (bulk-upload-\* stack). - Validation failures from schema drift in generated files. - Solutions and Workarounds: - Must run generator from `ccab` directory. - Ignore some CLI warnings; find output in `misc-tools/`. - Use `itest:manualTest` for correct test execution. - Ensure bulk-upload stack is deployed in test environment. - Use custom validation scripts/tests for debugging file syntax. - Update bulk upload generator to match latest schema. - Tooling and Documentation Issues: - Generator lacked up-to-date documentation for usage and output. - Required ad-hoc tools and code inspection for troubleshooting. - Outdated instructions in code comments. - References: -  [https://docs.google.com/document/d/1Pm0sZoTflJFXgpW19_u9zfOtiTWAxmKZlQ7a_Sbt30k/edit?tab=t.0](https://docs.google.com/document/d/1Pm0sZoTflJFXgpW19_u9zfOtiTWAxmKZlQ7a_Sbt30k/edit?tab=t.0) - [Bulk Export README.md](https://github.com/trilogy-group/ccab/tree/staging/itest/itest/src/test/resources/bulk-upload/README.md) - Personal log and troubleshooting notes (see above) - [Bulk upload schema documentation] - Steps for deleting Cloudformation Stacks. - DOK1: Facts About CloudFormation Stack Deletion Issue - Introduction: When dealing with the deployment of environments using CloudFormation stacks created by CDK, one might encounter issues where the stack is not properly deleted during the environment destruction process. This can lead to resources being left behind, causing unintended costs and complexity in managing cloud resources. - Key Facts - Issue Persistence: Despite the destroy environment workflow showing success, the CloudFormation stack may remain undeleted. - Error Messages: Custom resources (e.g., Custom::S3AutoDeleteObjects) can fail to delete, resulting in a DELETE_FAILED state. An example error message includes: This Custom::S3AutoDeleteObjects resource is in a DELETE_FAILED state. - CloudFormation did not receive a response from your Custom Resource. Please check your logs for requestId [0dbefe67-030c-4eac-8f43-003d1184066b]. If you are using the Python cfn-response module, you may need to update your Lambda function code so that CloudFormation can attach the updated version. - Resource Status: The DELETE_FAILED status for custom resources prevents the entire stack from being deleted. - Manual Intervention: Manual steps are required to delete the stack with resource retention, followed by the cleanup of orphaned resources. - Tools and Commands: Utilization of AWS CLI, CloudFormation commands, and the Resource Groups Tagging API is necessary for troubleshooting and resolving the issue. - Diagnostic and Deletion Commands - Listing Failed Resources: The command to list resources in a `DELETE_FAILED` state is: - `aws cloudformation describe-stack-resources --stack-name monitoring-stack-mdvuseast1 --query "StackResources[?ResourceStatus=='DELETE_FAILED'].[LogicalResourceId, ResourceType, ResourceStatusReason]" --output table` - Deleting Stack with Retention: To delete a stack but retain a failed resource, use: - `aws cloudformation delete-stack --stack-name monitoring-stack-mdvuseast1 --retain-resources ec2resourcesbucketAutoDeleteObjectsCustomResource6A4F7895` - DOK2: Analysis and Solution for CloudFormation Stack Deletion Issue - OverviewThe primary reason for stacks not being deleted is often due to custom resources with lifecycles maintained by Lambda functions that do not support the necessary deletion functions. This leads to a `DELETE_FAILED` state, requiring manual intervention for deletion.Steps for Manual Deletion - Identify Failed Resources: Use AWS CLI commands to list resources that failed to delete. - Delete Stack with Retention: Delete the stack while retaining the problematic resources. - Find Orphaned Resources: Utilize the Resource Groups Tagging API to discover resources left behind after stack deletion. - Manually Delete Orphaned Resources: Use specific AWS CLI commands to delete each orphaned resource. - Script for Enumerating Orphaned ResourcesFor projects with multiple stacks, a script can automate the process of scanning for orphaned resources: - bash - ```
    #!/bin/bash

# List of deleted stack names

stacks=(
  engine-app-stack-mgit
  job-processing-mgituseast1
  appsync-api-mgituseast1
  notifier-stack-mgituseast1
  appsync-lambdas-mgituseast1v2
  stateless-stack-mgituseast1
  dynamo-lambdas-mgituseast1v2
  edr-exporter-mgituseast1
  stateful-stack-mgituseast1
  neptune-stack-mgit
  ccab-stack-mgit
)

output_file="orphaned-resources.txt"

> "$output_file"  # Clear or create the file

echo "Scanning for orphaned resources..."

for stack in "${stacks[@]}"; do
  echo "Processing stack: $stack"
  aws resourcegroupstaggingapi get-resources \
    --tag-filters Key=aws:cloudformation:stack-name,Values=$stack \
    --query "ResourceTagMappingList[].ResourceARN" \
    --output text >> "$output_file"
done

# Add quotes and remove duplicates

sort -u "$output_file" | sed 's/^/"/;s/$/"/' > temp && mv temp "$output_file"

echo "Done. Orphaned resource ARNs saved to: $output_file"

````
          - Best Practices and Lessons Learned
            - Verify Stack Deletions: Always check the AWS console after environment destruction to ensure all stacks and resources are properly deleted.
            - Improve Workflow Outputs: Modify workflows to clearly report any failures or partial successes during stack deletion.
      - CCAB Alarm-to-Component Troubleshooting Matrix Description
        - DOK1: Facts
          - CCAB uses standard AWS ALB metrics for charge engine monitoring, specifically tracking HTTPCode_Target_4XX_Count and HTTPCode_Target_5XX_Count to detect application-level errors and server failures
          - CCAB uses EventBridge rules to capture AWS Health events and routes them to CloudWatch Logs at `/aws/events/health-events-{env}`, where metric filters parse JSON log patterns to count specific event types
        - DOK2: Technical details
          - Health event monitoring uses JSON path filtering in metric filters - `$.detail.eventTypeCode = "AWS_ABUSE_NOTIFICATION"` for abuse events and `$.detail.eventTypeCategory = "issue"` for general health issues. These filters increment counters that trigger alarms when any matching event occurs (threshold >= 1)
      - DOK4 - SPOV
        - Unlocking Organizational Memory and Expertise
          - The conventional approach to documentation focuses on clarity, completeness, and ease of use, but overlooks its potential as a tool for organizational memory and risk management. Documentation should be treated as a strategic asset, encoding the hard-won scars of senior engineers and capturing the nuances of past failures and lessons learned. This approach acknowledges that documentation is not just for new team members, but for the organization's future self, ensuring that critical knowledge is retained even as personnel change. Key aspects of this approach include:
          - Capturing the "why" behind design decisions, to prevent future teams from unknowingly undoing critical fixes or optimizations.
          - Documenting past failures and near-misses, to inform future risk assessments and prevent recurrence.
          - Surfacing non-obvious, high-leverage lessons, to make documentation an asset that teaches valuable, non-Googleable insights.
          - By shifting the focus of documentation from basic onboarding to encoding expert-level war stories, teams can unlock the true value of their documentation. This means moving beyond checklists and feature guides, and instead creating docs that share the rare, expert-level knowledge that even veterans forget over time. Good documentation should actively weaponize senior engineers' hard-won scars, using them to inform and improve future decision-making, and ultimately becoming a key driver of organizational success.
        - Deletion as a measure of automation success
          - Deletion is a separate process from creation, often neglected.
          - If CloudFormation can't reliably delete what it creates, you don't have Infrastructure-as-Code.
          - Deletion success rate measures automation maturity.
          - Custom resources indicate CloudFormation failed.
          - Real automation means deletion works as reliably as creation.
          - Teams that can't destroy infrastructure cleanly have technical debt factories.
          - Measure success by what gets cleanly removed, not what gets provisioned.
          - Treat every custom resource as a red flag that needs justification.
          - Build post-destroy validation before celebrating deployment automation.
          - If your infrastructure can't be deleted as easily as it's created, you're doing Infrastructure-as-Wishful-Thinking.
          - Prioritize deletion and documentation over provisioning speed.
          - Documentation should capture the "why" behind deletion decisions and past failures.
          - Deletion failures should be documented to inform future risk assessments.
        - Cloud providers are failing developers by not solving cross-service consistency—stop forcing us into brittle Saga patterns, start building native ACID transactions across services.
          - Reference "DOK3-Multiple Entities in Cloud sync", systems having to perform background checks on two or more service states sync is a waste of resource and compute cycles.
          - SAGA patterns are provided in some services of AWS and Azure but they do not meet the requirement
      - DOK3 - Insights
        - Truth About Documentation
          - For a project of this scale there should be a central repository of documentation, where a new engineer on the project can look into the various issues and problems that are faced when running things for the first time. Documentation is not just about documenting what works, but also about exposing what breaks? The industry lie is that documentation should only cover the happy path. In reality, real value lies in surfacing how things go wrong.
            - Key Insights
              - Documentation is useless if it only covers the happy path.
              - Undocumented failure modes cost more dev time than missing features.
              - AI assistants are especially vulnerable to poorly documented failure modes.
              - If your docs don’t list what breaks, how, and how to spot it—you’re not helping engineers, you’re slowing them down (and AI can’t help either).
              - Documentation that only covers success scenarios is worse than no documentation at all—it creates false confidence that leads to deeper rabbit holes.
              - Comprehensive documentation means covering every way things break, not every feature.
            - Evidence
              - Bulk upload: Docs say run in misc-tools/—fails; actually must run in ccab/.
              - Generator: Unclear warnings look like errors—no doc tells you which to ignore.
              - Outdated schemas: Docs never mention planVersionId change; hours wasted chasing silent failures.
              - Test failures: Error output tells you nothing; custom test scripts needed to find root cause.
              - Bulk upload generator docs omit critical directory information.
              - Generator warnings resemble errors but should be ignored.
              - Deprecated fields cause validation failures with unhelpful error messages.
            - Why This Matters
              - New engineers waste 80% of setup time on undocumented failure modes, not missing features.
              - AI systems can't distinguish "ignore this warning" from "fix this error" without explicit guidance.
              - Perfect-world docs create false confidence that leads to deeper debugging holes.
            - Recommendations
              - Document warnings to ignore.
              - Include common failure scenarios in setup instructions.
              - Add "what probably broke" to every setup step.
              - Make error decision trees explicit.
              - Write docs assuming Murphy's Law, not best-case scenarios.
            - Conclusion
              - Documentation must prioritize failure modes to be useful. Stop documenting the 10% of time things work perfectly. Document the 90% of time they don't. By doing so, you'll create a truly comprehensive and helpful documentation that saves time and reduces frustration for engineers and AI systems alike. Your README should have more "what went wrong" sections than "how to use" sections.
        - CloudFormation Stack Deletion Issues
          - Overview
            - CloudFormation stack deletions can be problematic, especially with custom resources. Here are the key issues and best practices:
          - Key Issues
            - Custom resources can cause DELETE_FAILED states and leave orphaned resources behind
            - Automation pipelines may not catch partial stack failures, leading to hidden costs and complexity
            - Manual intervention is often required to resolve these issues
            - Orphaned resources (e.g., log groups, S3 buckets) can accumulate over time if not proactively found and deleted
          - Root Cause
            - The problem stems from:
            - CDK abstractions not handling custom resource lifecycles properly, especially during deletion
            - Custom resources with Lambda backends often lacking proper DELETE operation support
            - Automation pipelines reporting "success" even when resources fail to delete
          - Best Practices
            - Verify deletion manually: Ensure everything is properly deleted
            - Improve workflow outputs: Clearly report failures or partial successes
            - Document manual processes: Troubleshoot and resolve stack deletion issues
            - Regularly review cloud resources: Clean up orphaned resources
            - Audit Lambda custom resources: Check for DELETE operation support before deployment
            - Build post-destroy validation: Into automation pipelines to catch partial failures
          - Why This Matters
            - Manual cleanup becomes the norm instead of the exception
            - Resource sprawl leads to unexpected AWS bills
            - Team velocity slows down due to cleanup overhead
            - Knowledge gets trapped in manual processes instead of being automated
          - Takeaway
            - To manage CloudFormation stacks effectively, it's crucial to:
            - Understand the nuances of custom resource deletion
            - Implement robust error handling and post-destroy validation
            - Plan for partial failures, not just happy paths
            - Make resource cleanup failures explicit, not hidden
            - Document the manual cleanup process as a first-class workflow, not an afterthought
          - By following these best practices, teams can reduce manual cleanup, prevent resource sprawl, and improve infrastructure-as-code workflow reliability.
        - Multiple Entities in Cloud sync
          - As shown in "DOK2- Multiple entities synchronization", when a system when performing update on a  logical object that is written in two different cloud entities, then there must be a background process that should be checking if any of the entity has become out of sync
      - *----------  BRIGHT LINE.  Above this is based on the owner's opinion and expertise.  Below this is based on the external flow of information  ----------*
      - Experts
        - Microsoft Azure. Saga Patterns. [https://learn.microsoft.com/en-us/azure/architecture/patterns/saga](https://learn.microsoft.com/en-us/azure/architecture/patterns/saga)
      - DOK2 - Knowledge Tree
        - DOK2 -summaries
        - DOK1 - facts
        - links to original sources
      - *----------  BRIGHT LINE.  Above this is the BrainLift, the user creates this without AI.  Below this is not the BrainLift, it is however the user gets sources from the flow of external information ----------*
      - BrainMaxxing, other feeds, etc.
  -
  -
```                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      cc
````
