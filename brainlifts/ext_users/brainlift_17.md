Plan and Design Tasks

Owner

Lokesh Singhania

Purpose

Background

Currently, Plan and Design does not have a particular expected output format leading to ambiguity especially for people doing it for the first time.

Current practice is to determine story points based on time spent.

Goals

Catch all non-trivial misalignments during the plan and design task, eliminating the rework done in subsequent implementation tasks owing to misalignments regarding the plan and design.

Define a repeatable output format that is comprehensive to eliminate misses that lead to ad hoc designs later and enable efficient and faster implementations that don't need to context switch to planning due to earlier misses.

Set expectations both for the doer and the QCer to reduce friction during the review process.

In Scope:

Document and define the output requirement of a plan and design task to minimize and/or eliminate the back-and-forth leading to inefficiency.

Suitable for me in my current project (Athena) for all repos (both frontend and backend).

Out of Scope

Epic Design Tasks: This Brain Lift focuses on Plan and Design tasks of stories, epics, etc. that have been already created and not for epic design tasks whose purpose is to define that stories or epics

Individual Tasks Planning Phase: Though, this may have some overlap with the planning phase within each task, this brain lift only focuses on scenarios when we create a separate task or ticket for the plan and design of a story or epic.

Team-wide practices: This may be used by others, but that is not the primary goal but a potential by-product.

Cross Project Practices: This is to define an output format that works for me in content of my current project. Though it is defined as generic, it is possible that a different output format may be more apt for a different project based on its needs.

DOK4 - SPOV

Plan and design output should update artifacts that are used in day to day job (e.g. code, postman collection, context pack, brainlift, etc) instead of a separate document that is created and used once.

Add complete models in the codebase for the input/output

Add/update endpoints.

Populate(or create) context packs based on the necessary context gathered as well as the decisions taken during the plan and design task.

Create class hierarchy and method stubs with defined input and output but with an empty implementation. The stubs could include comments about the implementation as well as calling other stubs.

This eliminates any later misalignment regarding not only the class hierarchy but also module/folder structure and naming.

Enables the upcoming implementation task to focus purely on the implementation and not misc concerns (naming, folder structure)

Plan and design need to go much further than the ticket description.

> This is presented as a spiky point of view though it may be general industry view because the plans and designs that I have encountered (including mine) have not been mentioning these.

Ticket descriptions focus on the product perspective, but each ticket must still anticipate core engineering needs — such as caching, retries, and error handling — to ensure robust implementations. These are not afterthoughts to fix once issues arise; they must be considered upfront.

Plan and design must prominently describe any spiky or potentially controversial decisions.

> This again may be common sense, but keeping it as a spiky point of view because it is worth repeating being one of the primary things that the plan and design exists to address.

For a new or a different pattern not followed in the rest of the codebase, create a brainlift. This facilitates the reuse of the different pattern for similar scenarios in future and also highlights the deviation from the current practices while also providing a structured format for its rationale.

For decisions that are smaller in impact or localized that doesn't justify a brainlift, context packs to be used instead.

Plan and design estimations must use pre defined competency step types instead of determining story points based on time spent.

> Spiky as different from the advice I received regarding plan and design estimations, story points.

Current competencies support plan and design related activities and there is no reason not to leverage them.

Anything repeatable for a plan and design task that is not covered in the existing competency to be proposed as a new competency, just like we do for our implementation. Custom Work to be used as a stop gap for immediate needs if required.

DOK3 - Insights

Having models in a document or in Jira output section can be translated directly into code with the help of AI with minimal effort.

This helps in clarifying and leaves no ambiguity regarding the model, bringing to notice any potential points of contention that may be missed when defining model at a high level in Plan and Design task

Having a defined consistent output improves not only efficiency but also quality.

Eliminates decision fatigue about what is to be the output.

Sets expectation both for the reviewer and doer about the expected output.

An formalized format will be be consistent by nature and sets the stage for incremental improvements over time. While an unformalized format would lead to inconsistency even for the same doer and does not help in improving the format over time, it may even regress.

Having concrete definitions (such as model, class hierarchy and API endpoints) forces us to take the necessary decisions and reduces the chance of something important being missed or something controversial being not noticed.

Updating/Creating context pack forces us to decide the module placement and naming beforehand which may be a potential point of disagreement and reveal a deeper and more important misalignment.

Using time-based story points for plan and design is an anti-pattern that can be easily avoided

Time-based story points instead of complexity-based step types incentivize(or at least do not disincentivize) inefficiency.

Using competency-based step types for estimations brings the advantages with it:

- Clarity of the work and effort that went into the plan and design instead of just the output, both for the reviewer & Doer.
- Modeling and focusing on the complexity/value of the effort instead of the time
- Habituate the doer to define the scope and identify the potential risky questions before they start working in earnest on the plan and design task.

Knowledge Tree

- Relevant Step Types for Plan and Design
  - [Competencies Sheet](https://docs.google.com/spreadsheets/d/1XS7MK01ycnAO6JG5ha3N-F1jv-cZfGmeyZhO_fov3bc/edit?gid=991923659#gid=991923659)
    - DOK1 - facts
      - **Manual Testing**: To check existing product functionality/edge cases.
      - **Research**: when we need to choose from alternatives and need research or POC's for the same.
      - **Documentation**: For updates to our standard documentations (for the given task) such as brainlifts, context packs, Postman collections, and debug events.
      - **Reverse Engineering**: When we need to dig into unfamiliar pieces of code, either in our project or related (e.g. Checking Time Back Platform implementation for understanding of Caliper events implementation in Athena).
      - **Clarifying Requirements**: For clarifications and discussions with product and/or dependent projects/team members (e.g. aligning on pattern within team for the new feature, enquiring about API from a downstream project team).
      - **Defining in-memory DTOs | Designing REST APIS | Designing GraphQL APIs**: For defining the API endpoints and contracts/models.
      - **Custom Work**: Fallback when no other step type covers the activity.
    - DOK2 - Multiple existing step types provide support for common activities during plan and design.
- Non Functional Concerns
  - ()
    - DOK 1 - Facts
      - Caching Strategy
        - Location: Backend/Frontend
        - Cache Key Pattern
        - Cache Duration
      - Retry Strategy:
        - Evaluating necessity for the API/case
        - Appropriate Max Retries
        - Backoff strategy
        - Location: Backend/Frontend
      - Error Handling
        - If to log log to Sentry/CloudWatch/etc
        - Categorization based on criticality
      - Consistency with existing implementation
        - Functional consistency with similar feature for a different use case/course
        - Code Consistency to ensure similar handling for similar features
        - Naming Consistency to ensure the previous names are no longer confusing after introduction of new features (e.g. earlier - only Unit tests, new: FRQ Unit Test -> old need to be renamed to MCQ Unit Test)
        - Documenting intentional variations across similar features.
      - Performance
    - DOK 2 - Summary: Multiple aspects which are not part of a typical ticket description need to be considered to ensure complete implementation.

Experts

- Expert 1
  - Description:
  - Relevance:
  - Locations: (blog, x, personal website, etc.)

Notes

Links

BL Coach:

Next

Structure and content of KT

Language of SPOV

Templatizing Pnd

- Steps
  - Use Cases
  - External APIs
  - Current Implementation
- Organize
  - By Use case or APIs.

Workflowy is not a suitable tool for plan and design

What is the right tool and format

Can workflowy support it

Do we make BLs for Pnd or not?
