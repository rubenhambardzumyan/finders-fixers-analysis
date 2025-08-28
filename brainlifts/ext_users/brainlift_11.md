Defining In-Memory DTOs in TypeScript

Owner

- Eugene Dolgov (﻿Eugene Dolgov﻿)

Purpose

- To establish a consistent, reliable, and maintainable approach for defining in-memory Data Transfer Objects (DTOs). This framework ensures data integrity, type safety, and seamless communication between different parts of our systems.
- **Out of scope:** Data persistence models, database schemas, and client-side state management patterns.

DOK4 - SPOV

**The only acceptable way to define a DTO for cross-boundary communication **(backend to frontend,\*\* **with third-party APIs)** is with a Zod schema that enforces immutability.\*\* This single schema is the contract, providing the non-negotiable source of truth for runtime validation and static typing.

- **Correct Implementation:** The schema defines validation, immutability, and the type in one place.

```
// File: /models/user.models.ts
import { z } from 'zod';
import { UserRoleEnum } from '../constants/user.constants';

export const CreateUserInputSchema = z.object({
  email: z.string().email('A valid email address is required.'),
  firstName: z.string().min(1, 'First name cannot be empty.'),
  role: z.nativeEnum(UserRoleEnum).default(UserRoleEnum.VIEWER),
}).readonly(); // .readonly() is mandatory for immutability.

// The DTO type is inferred directly from the schema. No separate interface is needed.
export type CreateUserInput = z.infer<typeof CreateUserInputSchema>;
```

- **An untrusted input must be parsed into a validated DTO at the application boundary **— the earliest possible moment. Business logic must never operate on raw, unvalidated objects.
  - **Correct Implementation: **A handler or controller validates input before any other action.
  - ```
    import { CreateUserInputSchema, CreateUserInput } from '../models/user.models';
    ```

function handleCreateUserRequest(requestBody: unknown): RequestOutput {
  try {
    // 1. The raw `requestBody` is parsed into a trusted, immutable DTO.
    const trustedUserInput: CreateUserInput = CreateUserInputSchema.parse(requestBody);

// 2. From this point on, all logic uses the `trustedUserInput`.
    // The immutability is enforced by the type system.
    // trustedUserInput.firstName = "Fail"; // <-- TypeScript compilation error

createUser(trustedUserInput);
  } catch (error) {
    // 3. If validation fails, the request is rejected immediately.
    return { success: false, errors: error.errors };
  }
}

````
- **A DTO's sole purpose is data transfer. Embedding any business logic, calculations, or formatting within them is a critical anti-pattern** that violates separation of concerns and leads to tightly coupled, brittle systems.
  - **Incorrect Implementation (Anti-Pattern):**
  - ```
// This is NOT a DTO because it contains logic.
export type BadUserDTO = {
  readonly firstName: string;
  readonly lastName: string;
  // Business logic inside a data object is forbidden.
  getFullName: () => string;
};
````

- **Correct Implementation:** Logic is fully separated into a service layer.
- ```
  // The DTO is pure data, with no methods.
  export type User = {
    readonly firstName: string;
    readonly lastName: string;
  };
  ```

// The logic lives in a service, completely separate from the data structure.
class UserService {
  public getFullName(user: User): string {
    return `${user.firstName} ${user.lastName}`;
  }
}

````
- **Code organization for data structures is not a matter of preference**; it is a strict standard for project coherence. **DTOs live in `/models`** ** and enums live in `/constants`** **.**
  - **Correct Implementation:** The file tree must follow this precise structure.
  - ```
src/
├── constants/
│   └── user-role.constant.ts  # Enums are defined here
└── models/
    └── user.model.ts          # Zod schemas and DTO types are defined here
````

- **Enum Definition (/constants/user-role.constant.ts):**
- ```
  export enum UserRoleEnum {
    ADMIN = 'ADMIN',
    EDITOR = 'EDITOR',
    VIEWER = 'VIEWER',
  }
  ```

```
- **Immutability is non-negotiable.** A DTO, once created, must never be mutated. To modify it, you must create a new instance. This is the only way to prevent unpredictable side effects, simplify debugging, and build a reliable data flow.
- **The "one-size-fits-all" DTO is an anti-pattern. **The idea of a single, canonical UserDTO for all operations is fundamentally flawed. DTOs must be purpose-built for a single operation. A CreateUserInput DTO is different from a UserPublicProfileOutput DTO, which is different from an UpdateUserPassword DTO. This practice is our primary defense against both over-fetching data and, more critically, security vulnerabilities from mass assignment attacks. What you exclude from a DTO is as important as what you include.
- **Database entities must never cross service boundaries.** A DTO is the formal contract for communication between components; a database entity is an implementation detail of how a single service persists its state. Exposing entities outside the service that owns them creates a tight, brittle coupling that makes future changes to the data model nearly impossible without breaking consumers. Always map your internal entities to specific, public-facing DTOs at the boundary.

DOK3 – Insights

Comprehensive DTO validation at application boundaries serves as a form of executable documentation. Clear, detailed validation errors are more valuable to a consuming developer than separately maintained API documentation that is often stale or incomplete. The validation schema is the most current and ruthlessly accurate description of what the service expects.

- The concept of a single, canonical DTO for a resource (e.g., one User DTO) is a fallacy that leads to bloated and confusing data contracts. In reality, data context is paramount. A CreateUserInput DTO has different requirements (e.g., required password) than a UserOutput DTO (e.g., omitted password, included id and createdAt fields) or an UpdateUserEmail DTO. The proliferation of distinct, operation-specific DTOs is a sign of a healthy, well-defined API, not unnecessary complexity.
- A strictly defined DTO is one of the most effective, yet often overlooked, security controls in an application. By creating an explicit allow-list of fields for a given operation, DTO validation provides a robust defense against mass assignment vulnerabilities, where a malicious user might try to inject and update forbidden fields (e.g., setting isAdmin = true). What you exclude from a DTO schema is as important for security as what you include.
- The shape and complexity of DTOs exchanged between two services act as a "canary in the coal mine" for architectural health. If two services require large, deeply nested DTOs to communicate, it suggests their responsibilities are not clearly separated and they are too tightly coupled. The DTO is a diagnostic tool; its complexity is a direct measure of the coupling between the components it connects.
- The true cost of using primitive types (e.g., string) for core domain concepts (e.g., an email address or a product ID) is hidden. The cost is not paid by the DTO author, but by every single consumer who must re-implement validation and contextual understanding. Creating a specific, validated type (e.g., a Zod schema for EmailAddress) centralizes this logic, reducing system-wide cognitive load and preventing entire classes of bugs that arise from downstream misuse. This initial investment pays for itself by making the data contract itself more intelligent.
- Friction and bugs related to DTO evolution are often a symptom of treating the DTO as a shared implementation detail rather than a formal, versioned contract. When a backend team can change a DTO and instantly break a frontend client, it reveals a lack of an explicit agreement between the two. This highlights the need for treating DTOs with the same rigor as public API endpoints, including strategies for versioning and deprecation.

Experts

Chair of the C4Model, author

- **Name:** Simon Brown
- **Main views:** Advocates for thinking about software architecture in terms of "Code, Containers, Components and Classes" a clear hierarchy of abstractions. He emphasizes clear communication of architectural ideas through simple diagrams and a shared vocabulary.
- **Why follow: **His focus on clear boundaries and communication directly applies to DTOs, which are the contracts that define those boundaries. Applying his thinking helps ensure DTOs are designed at the right level of abstraction.
- Locations
  - Personal Blog: [https://simonbrown.je/](https://simonbrown.je/)
  - Twitter/X: [https://x.com/simonbrown](https://x.com/simonbrown)
- Author of "Clean Code" and "Clean Architecture"
  - **Name:** Robert C. Martin (Uncle Bob)
  - **Main views:** Argues that data structures should be simple and expose their data without behavior. He distinguishes sharply between simple data objects (like DTOs) and objects with rich behavior, advocating for a strong separation between them.
  - **Why follow:** His principles on clean architecture provide the foundational "why" behind keeping DTOs free of business logic. His work is the canonical source for understanding the separation of concerns, which is the core principle governing DTO design.
  - Locations
    - Personal Blog: [https://blog.cleancoder.com/](https://blog.cleancoder.com/)
    - Twitter/X: [https://x.com/unclebobmartin](https://x.com/unclebobmartin)
- Creator of Zod
  - **Name:** Colin McDonnell
  - **Main views:** Believes in the power of TypeScript-first development and the importance of a single source of truth for data validation and type safety.
  - **Why follow:** As the creator of our chosen tool for schema definition and validation, his insights and the library's evolution provide the most direct guidance on best practices for implementation. Following his work ensures we are using the tool as intended and are aware of new features that can simplify our work.
  - Locations
    - GitHub: [https://github.com/colinhacks](https://github.com/colinhacks)
    - Twitter/X: [https://x.com/colinhacks](https://x.com/colinhacks)

DOK2 - Knowledge Tree

The Data Transfer Object (DTO) Pattern

- Source: "Patterns of Enterprise Application Architecture" by Martin Fowler
- DOK1 - Facts
  - The DTO pattern is used to pass data with multiple attributes in a single method call.
  - A key motivation for the pattern is to reduce the number of remote calls between processes.
  - Martin Fowler identifies a DTO as a specific type of Data Holder object.
- DOK2 - Summary
  - The DTO pattern, as originally defined by Martin Fowler, solves the problem of inefficient communication between processes (like a client and a server) by bundling the data for a single interaction into one simple container object. This reduces network overhead and decouples architectural layers by creating a formal data contract between them.
- URL
  - [https://martinfowler.com/eaaCatalog/dataTransferObject.html](https://martinfowler.com/eaaCatalog/dataTransferObject.html)

Schema Declaration and Validation with Zod

- Source: Zod Official Documentation
- DOK1 - Facts
  - z.object({ ... }) is a function that creates a schema for an object's shape and its properties' types.
  - The .parse(data) method checks if the provided data conforms to the schema and throws a detailed error if it does not.
  - z.infer<typeof schema> is a TypeScript utility that extracts a static, compile-time type definition directly from a runtime schema.
  - The .readonly() method can be chained onto an object schema to make all properties in the inferred TypeScript type readonly, enforcing immutability at compile time.
- DOK2 - Summary
  - The Zod library provides specific functions (z.object, .parse) to define and enforce data structures at runtime. It also offers a mechanism (z.infer) to derive a compile-time TypeScript type from the exact same schema. This eliminates the common problem of manually synchronizing validation logic and type definitions, while also providing tools like .readonly() to enforce key architectural principles like immutability directly at the type level.
- URL
  - [https://zod.dev/](https://zod.dev/)
- Immutability in TypeScript
  - Source: TypeScript Handbook & MDN Web Docs
  - DOK1 - Facts
    - The readonly keyword in TypeScript can be applied to properties, preventing the compiler from allowing their reassignment after an object's initial creation.
    - Object.freeze() is a built-in JavaScript method that provides shallow runtime immutability by preventing the addition, deletion, or modification of an object's direct properties.
    - The spread syntax ({ ...original, property: newValue }) is the standard pattern for creating a modified copy of an object without mutating the original source object.
  - DOK2 - Summary
    - Immutability in TypeScript is a two-level concept: the readonly keyword provides essential compile-time safety to catch accidental modifications during development, while Object.freeze() can offer a layer of runtime protection. The core practice for working with immutable objects is to never change them directly; instead, you create a new version with the updated data, which leads to more predictable state management and fewer side-effect-related bugs.
  - URLs
    - [https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)
    - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
- Structural Typing in TypeScript
  - Source: TypeScript Handbook
  - DOK1 - Facts
    - TypeScript's type system is structural, not nominal.
    - Type compatibility is determined by an object's "shape"—the names and types of its properties—not by its explicit class or interface name.
    - If two types have the same structure, they are considered compatible and interchangeable.
    - This is often called "duck typing": if an object has all the properties of a Duck type, it can be treated as a Duck.
  - DOK2 - Summary
    - TypeScript uses a structural type system to determine if a value can be assigned to a variable of a given type. It only checks if the value has at least the properties required by the type definition, regardless of how or where that value was created. This core principle is what allows a plain JavaScript object to be compatible with a Zod-inferred DTO type, as long as it has the correct structure, enabling flexible yet type-safe code.
  - URL
    - [https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#structural-type-system](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#structural-type-system)
```
