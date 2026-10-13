# Chapter 7: Exception Handling

Exceptions represent conditions that interrupt the ordinary flow of a program. Good error handling distinguishes programming mistakes from recoverable failures, preserves useful context, and releases resources reliably.

## 150. Errors versus exceptions

`Throwable` has two major branches: `Error` and `Exception`. Errors generally indicate serious JVM or system problems that applications should not try to recover from casually; exceptions represent conditions an application may handle or report.

```java
try {
    Integer.parseInt("not a number");
} catch (NumberFormatException exception) {
    System.out.println("Enter a whole number");
}
```

Do not catch `Error` to disguise failures such as resource exhaustion.

**Key takeaway:** Catch specific recoverable exceptions, not every throwable condition.

## 151. Compile-time errors versus runtime errors

Compile-time errors prevent source code from compiling, such as incompatible types or missing symbols. Runtime exceptions occur while a compiled program executes, such as invalid indexing or parsing input that is not numeric.

```java
int[] values = {10, 20};
System.out.println(values[2]); // compiles, but throws at runtime
```

Compiler diagnostics catch many issues early, but they cannot prove every runtime input is valid.

**Key takeaway:** Use compiler feedback first, then validate runtime data and behavior.

## 152. Exception hierarchy

`Throwable` is the root of the exception hierarchy. `Error` and `Exception` extend it; `RuntimeException` extends `Exception`. Checked exceptions are exceptions other than `RuntimeException` and its subclasses.

```java
try {
    java.nio.file.Files.readString(java.nio.file.Path.of("notes.txt"));
} catch (java.io.IOException exception) {
    System.err.println(exception.getMessage());
}
```

Catch at a level that can handle the condition or add meaningful context.

**Key takeaway:** Understand the hierarchy to choose precise catch and throws declarations.

## 153. Checked exceptions

Checked exceptions must be caught or declared in a method's `throws` clause. They make certain failure paths visible to callers at compile time.

```java
static String read(java.nio.file.Path path) throws java.io.IOException {
    return java.nio.file.Files.readString(path);
}
```

Propagate a checked exception when the caller can make a better recovery decision.

**Key takeaway:** Handle checked exceptions or explicitly pass responsibility to callers.

## 154. Unchecked exceptions

Unchecked exceptions are `RuntimeException` subclasses and do not need to be declared or caught. They often indicate invalid arguments, incorrect state, or programming errors.

```java
static int first(int[] values) {
    if (values == null || values.length == 0) {
        throw new IllegalArgumentException("values must not be empty");
    }
    return values[0];
}
```

Do not use unchecked exceptions as routine control flow.

**Key takeaway:** Validate preconditions and use unchecked exceptions for invalid use or state.

## 155. Built-in exceptions

The Java API defines exceptions such as `NullPointerException`, `IllegalArgumentException`, `IllegalStateException`, `IndexOutOfBoundsException`, and `IOException`. Prefer a built-in type when it accurately describes the failure.

```java
static void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("age must be non-negative");
    }
}
```

Include a clear message that helps explain what was invalid without leaking sensitive data.

**Key takeaway:** Use the most specific standard exception that matches the problem.

## 156. User-defined exceptions

A custom exception represents a domain-specific failure that callers may need to distinguish. Extend `Exception` for a checked exception or `RuntimeException` for an unchecked one.

```java
class InsufficientFundsException extends Exception {
    InsufficientFundsException(String message) {
        super(message);
    }
}
```

Add custom exception types only when they clarify the API or recovery behavior.

**Key takeaway:** Domain exceptions should communicate meaningful, actionable failure categories.

## 157. `try` and `catch`

A `try` block contains code that may fail; a matching `catch` handles an exception of the declared type or a subtype. If no handler matches, the exception propagates to the caller.

```java
try {
    int count = Integer.parseInt(input);
    System.out.println(count);
} catch (NumberFormatException exception) {
    System.err.println("Input must be a whole number");
}
```

Keep the protected region and catch behavior as narrow and specific as practical.

**Key takeaway:** Catch only failures you can handle or meaningfully translate.

## 158. Multiple catch blocks

A try statement may have multiple catch blocks to handle different exception types. Put more specific exception types before their supertypes because a broader catch would make later subtype catches unreachable.

```java
try {
    process(input);
} catch (NumberFormatException exception) {
    reportBadNumber(exception);
} catch (IllegalArgumentException exception) {
    reportInvalidValue(exception);
}
```

Avoid duplicating large handling blocks; extract a shared method if the behavior is truly the same.

**Key takeaway:** Order catches from specific to general and preserve distinctions that matter.

## 159. Multi-catch

Multi-catch handles several unrelated exception types with one catch block using `|`. The caught variable is implicitly final.

```java
try {
    loadConfiguration();
} catch (java.io.IOException | SecurityException exception) {
    reportConfigurationFailure(exception);
}
```

Use it when handling is identical; use separate catches when recovery differs.

**Key takeaway:** Combine exception types only when one response is appropriate for all of them.

## 160. `finally`

A `finally` block runs as control leaves a try statement in ordinary completion and exception cases. It is traditionally used for cleanup, but try-with-resources is safer for closing `AutoCloseable` resources.

```java
try {
    performOperation();
} finally {
    releaseTemporaryState();
}
```

Avoid returning from `finally`, since it can hide an exception or override an earlier return value.

**Key takeaway:** Keep `finally` cleanup simple and never suppress the original failure accidentally.

## 161. `throw`

The `throw` statement raises a particular exception object and stops normal execution of the current path until a handler is found.

```java
if (amount <= 0) {
    throw new IllegalArgumentException("amount must be positive");
}
```

Throw exceptions for exceptional conditions rather than expected alternatives.

**Key takeaway:** Throw a precise exception at the point where invalid state is detected.

## 162. `throws`

The `throws` clause declares exceptions that a method may propagate to its callers. Checked exceptions must be caught or declared; unchecked exceptions may also be documented when useful.

```java
static byte[] load(java.nio.file.Path path) throws java.io.IOException {
    return java.nio.file.Files.readAllBytes(path);
}
```

A declaration does not handle the failure; it communicates responsibility to callers.

**Key takeaway:** Use `throws` to make propagation part of the method contract.

## 163. Exception propagation

When a method does not catch an exception, it propagates up the call stack until a matching handler is found or the thread's uncaught-exception handler receives it.

```java
static String loadName(java.nio.file.Path path) throws java.io.IOException {
    return java.nio.file.Files.readString(path).strip();
}
```

Add context when rethrowing only if it helps diagnose the failure, and preserve the original cause.

**Key takeaway:** Handle errors at the layer that has enough information to respond correctly.

## 164. Nested try blocks

A try statement may appear inside another try or catch block when an inner operation needs a distinct recovery boundary. Each catch handles exceptions from its associated try, not arbitrary failures in unrelated code.

```java
try {
    String input = readInput();
    try {
        process(input);
    } catch (IllegalArgumentException exception) {
        reportInvalidInput(exception);
    }
} catch (java.io.IOException exception) {
    reportReadFailure(exception);
}
```

Deeply nested exception handling is often a sign to extract focused methods.

**Key takeaway:** Nest handlers only when the inner and outer failures require genuinely different responses.

## 165. Custom exception design

A well-designed custom exception has a name that identifies the domain failure and constructors that preserve helpful messages and causes. Avoid creating many nearly identical types without distinct handling needs.

```java
class ConfigurationException extends Exception {
    ConfigurationException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

Do not encode sensitive input in exception messages or expose implementation details unnecessarily.

**Key takeaway:** Design exception types around caller decisions and preserve causal information.

## 166. Try-with-resources

Try-with-resources automatically closes resources that implement `AutoCloseable` when the block exits, including when an exception is thrown. Resources are closed in reverse order of initialization.

```java
try (var reader = java.nio.file.Files.newBufferedReader(
        java.nio.file.Path.of("notes.txt"))) {
    System.out.println(reader.readLine());
}
```

Use it for files, streams, database resources, and other closeable objects.

**Key takeaway:** Prefer try-with-resources to manual close logic.

## 167. Suppressed exceptions

If the try-with-resources body throws and closing a resource also throws, the body exception remains primary and the close failure is recorded as a suppressed exception.

```java
try (var resource = createResource()) {
    use(resource);
} catch (Exception exception) {
    for (Throwable suppressed : exception.getSuppressed()) {
        System.err.println(suppressed.getMessage());
    }
}
```

Inspect suppressed exceptions when diagnosing cleanup failures.

**Key takeaway:** Automatic resource management preserves both the primary failure and close failures.

## 168. Best practices for exception handling

Catch specific types, keep handlers close to the layer that can recover, preserve causes when translating exceptions, and avoid empty catch blocks. Do not use exceptions for ordinary branching or log the same failure at every layer.

```java
try {
    saveRecord(record);
} catch (java.io.IOException exception) {
    throw new IllegalStateException("Could not save record", exception);
}
```

Validate inputs early, provide useful diagnostics, and release resources with try-with-resources.

**Key takeaway:** Handle failures deliberately: recover, translate with context, or let them propagate.
