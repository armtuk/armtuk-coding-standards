# Formatting

Consider the follwogin when formatting code:

- **Code Story** - does the code portray a clear story of what it's doing if read from top to bottom. Can a semi-technical user look at the code and generate a mental model that correctly model the outline of the functionality?
- **Extraneous Code Comments** - Code comments should be avoided. Code comments may only be used when they clarify a section of code that is otherwise opaque.
- **Information order** - A code file like a good story should run from start, through plot development, to finish. The most significant parts and highest abstractions of a code file must come at the beginning. Minor details are saved until last. The file therefore follows the prinicple placing the most abstract methods at the top, with simple helper methods at the bottom.
- **Horizontal Information Density** - A modern code editor has the capability to display 140 or more characters on a line, do not split a single code statement onto multiple lines unless it produces better comprehension. A logging statement is an example of a single code statement should generally be on a single line. It doesn't provide significant additional comprehension to the reader, only to the log output of the program.
- **Conditionals** - if you have a conditional block that has more than a single line, prefer to decompose it into a helper function.
- **Exception handling**
  - Exceptions should only be used to convey unexpected failure. Expected failures must be expressed as an encapsulated return value. Failure modes are part of normal program operation, and therefore should use normal flow mechanisms.
    - Java Example using algebraic data types: 
    ```java
     abstract class MyFunctionReturnValue<T> {
        abstract T value;
        abstract boolean isSuccess();
     }

     class MyFunctionReturnValueSuccess<T> extends MyFunctionReturnValue<T> {
        public final T value;

        public MyFunctionReturnValueSuccess(T t) {
            this.value = t;
        }

        public boolean isSuccess() {return true;}
     }

     class MyFunctionReturnValueFailure extzends MyFunctionReturnValue {
        public boolean isSuccess() {return false;}
     }
    ``` 
    - TypeScript example using iterface:
    ```typescript
    interface MyFunctionReturnValueSuccess<T> {
        isSuccess: true
        value: T
    }

    interface MyFunctionReturnValueFailure<T> {
        isSuccess: false
        value: T
    }

    type MyFunctionReturnValue<T> = MyFunctionReturnValueSuccess<T> | MyFunctionReturnValueFailure<T>
    ```
  - Where the code for exception handler is the same as another place in the codebase, this exception handle must be decomposed into a helper function.
  - In languages like Java, always prefer to use Runtime Exceptions.
  - When an exception is used, define a specific custom exception class to convey a specific meaning.
    - This exception class should encapsulate the state at the time when the exception was thrown.

Knowledge density can be significantly improved by maximizing both horizontal and vertical space. Humans are incredibly adept at adapting to read various different formats, and whilst many like code that is formatted to appear "pretty", this doesn't necessarily improve knowledge density. This also often means that the code becomes very much more verbose, which, in a language like Java is already a bad problem. If what we value is comprehension, we should take comprehension over prettiness where prettiness itself does not confer comprehension. Wrapping each argument/parameter onto a new line is a classic example of something that does nothing to improve code readability, but looks "organized". This generates much more vertical length and decreases the information density of a single page of code greatly reducing the speed at which a developer may understand what is in a class file. There are times when a little extra vertical space aids in readability in much the same way a new paragraph does in sentence structure. This additional space to delineate sections is preferred as it allows for a logical grouping of functionality and improves grouping in the brain. Having said that, this practice will likely be minimized simply by the application of appropriate decomposition which will cause logically grouped pieces of code to be decomposed into their own functions when the Single Responsibility Principle is applied to its natural conclusion.

The below example is an example.

### ✅ Prefer to place multliple arguments on as few lines as reasonable. Only wrap arguments when they exceed 140 characters.

```java
private void checkFraudDocumentWithFilterSpec(String orderId, String workflowId,
    String realm, String requestType, OrderingProxy orderingProxyFilterSpec, FraudDocument fd) {
...
}
```

### Java - Overly Complex Functional Chaining
Prefer to chain multiple functional operations within a single line as follows:

```java
return criteria.treatment(labName)
    .map(InlineLogger.info(log, x -> String.format("lab criteria %s for lab %s returned path %s", criteria, labName, x)))
    .orElseGet(() -> {
         log.warn(String.format("Query %s returned null for lab %s", criteria, labName));
         return Lab.WEBLAB_TREATMENT_PATH;
    });
```

```TypeScript
return criteria.treatment(labName)
    .map(InlineLogger.info(log, x => `lab criteria ${criteria} for lab ${labName} returned path ${x}`))
    .orElseGet(() => {
         log.warn(`Query ${criteria} returned null for lab ${labName}`);
         return Lab.LAB_TREATMENT_PATH;
    });
```

## ✅ Better Formatting Examples

### TypeScript - Functional Style with Good Density
```typescript
// Good: Compact functional style
const processUserData = (users: User[]) => 
  users
    .filter(user => user.isActive)
    .map(user => ({ ...user, processedAt: new Date() }))
    .reduce((acc, user) => ({ ...acc, [user.id]: user }), {});

// Good: Clear method signatures
function validatePayment(amount: number, currency: string, paymentMethod: PaymentMethod, metadata: PaymentMetadata): ValidationResult {
  // Implementation
}

// Good: Logical grouping with appropriate spacing
class UserService {
  // Public methods first (highest abstraction)
  async createUser(userData: CreateUserRequest): Promise<User> {
    const validatedData = this.validateUserData(userData);
    const user = await this.userRepository.create(validatedData);
    await this.notifyUserCreated(user);
    return user;
  }

  async updateUser(id: string, updates: UpdateUserRequest): Promise<User> {
    // Implementation
  }

  // Private helper methods last (lowest abstraction)
  private validateUserData(data: CreateUserRequest): ValidatedUserData {
    // Implementation
  }

  private async notifyUserCreated(user: User): Promise<void> {
    // Implementation
  }
}
```

### TypeScript - Conditional Decomposition

#### ✅ Better: Decomposed into focused functions
```TypeScript
function processOrder(order: Order): ProcessResult {
  if (canProcessOrder(order)) {
    return executeOrderProcessing(order);
  } else {
    return createProcessingError(order);
  }
}

function canProcessOrder(order: Order): boolean {
  return order.status === 'pending' && 
         order.paymentStatus === 'paid' && 
         order.inventoryAvailable;
}

function executeOrderProcessing(order: Order): ProcessResult {
  // Focused implementation
  return { success: true, orderId: order.id };
}

function createProcessingError(order: Order): ProcessResult {
  // Focused error handling
  return { success: false, error: 'Order cannot be processed' };
}
```

## Key Principles

1. **Maximize Knowledge Density** - Use horizontal space effectively while maintaining readability.
2. **Prioritize Comprehension Over Prettiness** - Choose functional clarity over visual organization.
3. **Logical Information Order** - Most abstract concepts first, implementation details last.
4. **Decompose Complex Conditionals** - Extract complex logic into well-named functions.
5. **Minimize Vertical Waste** - Avoid unnecessary line breaks that don't improve understanding.
6. **Use Functional Composition** - Leverage method chaining for better density and clarity.
