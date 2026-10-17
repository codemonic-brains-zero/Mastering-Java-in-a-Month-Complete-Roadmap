# Chapter 2: Variables, Data Types, and Operators

Variables give names to values, data types describe which values a variable can hold, and operators let a program work with those values. Together, these ideas are the building blocks for calculations, decisions, and input in Java.

## 17. Variables

A variable is a named place in a program that refers to a value. Every Java variable has a declared type, a name, and a scope that determines where its name can be used. A variable's value may change when the variable is not `final`.

**Example:**

```java
int score = 85;
score = 92;
System.out.println(score); // 92
```

`score` is an `int` variable. Reassigning it changes the value used by later statements; it does not change the variable's type.

**Key takeaway:** A variable has a type and a name; assignment updates its value.

## 18. Variable declaration and initialization

Declaration introduces a variable and its type. Initialization gives it its first value. These can happen on the same line or separately. A local variable must be definitely assigned before Java lets the program read it.

**Example:**

```java
int quantity;          // declaration
quantity = 3;           // initialization
int price = 12;         // declaration and initialization together
int total = quantity * price;
```

Fields are different: Java supplies default values to fields (`0`, `false`, or `null`, depending on type). Do not rely on defaults for local variables; assign them explicitly.

**Key takeaway:** Initialize local variables before reading them.

## 19. Dynamic initialization

An initializer does not have to be a literal. It can be an expression calculated from other values when the statement runs. This is often called dynamic initialization in introductory Java courses.

**Example:**

```java
int width = 8;
int height = 5;
int area = width * height;
int nextArea = area + width;
System.out.println(nextArea); // 48
```

The expressions use values available at that point in the program. If an input or an earlier variable changes, a later calculation can produce a different result.

**Key takeaway:** An initializer can be a calculation, a method result, or another expression—not just a fixed literal.

## 20. Scope and lifetime of variables

**Scope** is the region of source code in which a variable name is accessible. **Lifetime** is how long that variable's value exists during program execution. These ideas are related but not identical: a name can go out of scope while an object it referred to remains reachable elsewhere.

**Example:**

```java
int outer = 10;
if (outer > 0) {
    int inner = 4;
    System.out.println(outer + inner); // both names are in scope
}
// inner is out of scope here
```

The braces define a block. `outer` is declared in the surrounding block, so the inner block can use it. `inner` is declared inside the `if` block, so code after that block cannot use its name.

**Key takeaway:** A variable is usable only within its scope; its lifetime describes runtime existence.

## 21. Local, instance, and static variables

Java variables are commonly described by where they are declared:

- **Local variables** are declared inside a method, constructor, or block. Their scope is limited to that region, and they must be initialized before use.
- **Instance fields** are declared in a class outside its methods, without `static`. Each object has its own field values. Fields receive default values if no initializer is supplied.
- **Static fields** are declared with `static`. They belong to the class and are shared by its instances.

**Example:**

```java
class Counter {
    static int created; // shared by the class
    int value;          // separate for each object

    Counter(int start) {
        value = start;
        created++;
    }

    void printNext() {
        int next = value + 1; // local variable
        System.out.println(next);
    }
}
```

`value` belongs to one `Counter` object; `created` is shared. `next` exists only while `printNext` executes. Static fields are often used for class-wide constants or genuinely shared state; mutable shared state needs careful coordination in concurrent programs.

**Key takeaway:** Choose a variable's location based on who should own and access its value.

![Diagram showing a local variable in a method, an instance field on each object, and one static field shared by the class.](../shared/assets/variable-ownership.svg)

## 22. Constants and the `final` keyword

The `final` modifier prevents a variable from being assigned again after it has been initialized. A `static final` field is commonly used for a constant shared by a class. By convention, constant names use uppercase words separated by underscores.

**Example:**

```java
class Circle {
    static final double PI = 3.141592653589793;

    double area(double radius) {
        final double squaredRadius = radius * radius;
        return PI * squaredRadius;
    }
}
```

A `final` reference cannot be made to refer to a different object, but the referenced object's contents may still change if that object is mutable.

```java
final StringBuilder name = new StringBuilder("Java");
name.append(" SE"); // allowed: the object changes
// name = new StringBuilder("Other"); // not allowed: reassignment
```

**Key takeaway:** `final` prevents reassignment; it does not automatically make a referenced object immutable.

## 23. Primitive data types

Java defines eight primitive types. The size and range below are the language-level sizes/ranges normally taught for these types. The default values apply to **fields and array elements**, not to local variables inside methods (local variables must be assigned before use).

| Primitive type | Size | Range / possible values | Default value for fields and array elements | Example |
|---|---:|---|---|---|
| `byte` | 1 byte (8 bits) | -128 to 127 | `0` | `byte level = 7;` |
| `short` | 2 bytes (16 bits) | -32,768 to 32,767 | `0` | `short year = 2026;` |
| `int` | 4 bytes (32 bits) | -2,147,483,648 to 2,147,483,647 | `0` | `int count = 42;` |
| `long` | 8 bytes (64 bits) | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | `0L` | `long distance = 5_000_000_000L;` |
| `float` | 4 bytes (32-bit IEEE 754) | Approx. ±1.4 × 10⁻⁴⁵ to ±3.4028235 × 10³⁸ for nonzero finite values; about 6–7 decimal digits of precision | `0.0f` | `float ratio = 0.75f;` |
| `double` | 8 bytes (64-bit IEEE 754) | Approx. ±4.9 × 10⁻³²⁴ to ±1.7976931348623157 × 10³⁰⁸ for nonzero finite values; about 15–16 decimal digits of precision | `0.0d` (usually written `0.0`) | `double average = 82.5;` |
| `char` | 2 bytes (16-bit UTF-16 code unit) | `'\\u0000'` (0) to `'\\uffff'` (65,535) | `'\\u0000'` | `char initial = 'J';` |
| `boolean` | No precisely specified storage size in the Java language | `true` or `false` | `false` | `boolean ready = true;` |

**Important notes:**
- The floating-point ranges above describe approximate IEEE 754 values. `float` and `double` also support positive/negative zero, infinities, and `NaN`; they are not exact decimal types.
- Java does not define a portable byte size for `boolean` storage. Its only language-level values are `true` and `false`.
- A `char` holds one UTF-16 code unit, not necessarily one complete visible Unicode character.
- The default value for a reference-type field or array element is `null`.
- **Local variables have no automatically usable default value.** The compiler requires a local variable to be definitely assigned before it is read.

**Example — field defaults versus local variables:**
```java
class Defaults {
    int count;           // default: 0
    boolean active;      // default: false
    String name;         // default: null
    char letter;         // default: '\\u0000'

    void show() {
        int localCount;
        // System.out.println(localCount); // compile-time error: not initialized
        localCount = 0;
        System.out.println(localCount);
    }
}
```


Integer types are signed. `int` is the usual choice for whole-number calculations; use `long` when the possible range exceeds `int`. `float` and `double` represent approximate binary floating-point values, so they are not suitable for every exact-decimal use. `char` is not a general-purpose Unicode grapheme type: some visible characters require more than one UTF-16 code unit.

```java
int count = 4;
long largeCount = 4_000_000_000L;
double temperature = 21.5;
boolean passed = count > 0;
```

**Key takeaway:** Choose a primitive type for its range and meaning, and remember that floating-point values are approximate.

![Diagram grouping Java's eight primitive types into integral, floating-point, character, and boolean categories.](../shared/assets/java-primitive-types.svg)

## 24. Reference data types

A reference variable holds a reference to an object or the special value `null`; it does not contain the object's entire data. Classes, arrays, interfaces, and enums are reference types. Multiple variables can refer to the same object.

**Example:**

```java
String first = new String("Java");
String second = first;
second = second.toUpperCase();

System.out.println(first);  // Java
System.out.println(second); // JAVA
```

Strings are immutable, so `toUpperCase()` creates a result rather than changing the original string. With a mutable object, changes through one reference can be observed through another reference to that same object. Dereferencing `null` causes a `NullPointerException`.

```java
String name = null;
// System.out.println(name.length()); // throws NullPointerException
```

**Key takeaway:** Primitive variables hold primitive values; reference variables refer to objects and may also be `null`.

## 25. Literals

A literal is a value written directly in source code. Java supports integer, floating-point, character, string, boolean, and null literals.

**Example:**

```java
int million = 1_000_000;       // integer literal with digit separators
long population = 8_000_000_000L;
double fraction = 0.125;
float scale = 1.5F;
char newline = '\n';
String message = "Hello, Java";
boolean enabled = true;
String missing = null;
```

Digit separators (`_`) improve readability and do not change a number's value. Integer literals are `int` by default unless written with `L`; decimal literals are `double` by default unless written with `F`. A `char` literal uses single quotes and represents one UTF-16 code unit, while a `String` uses double quotes.

**Key takeaway:** Literal spelling affects its type; add `L` or `F` when the intended numeric type requires it.

## 26. Type conversion

Type conversion changes a value from one type to another. A conversion may be automatic when Java defines a safe widening conversion, or explicit when information could be lost. Converting a reference type uses different rules from converting primitives; this chapter focuses on primitive numeric conversions.

**Example:**

```java
int whole = 7;
double approximate = whole;       // int widens to double
double measurement = 7.9;
int truncated = (int) measurement; // explicit narrowing: 7
```

The cast truncates the fractional part; it does not round to the nearest integer. Narrowing an out-of-range value can also produce a surprising result. Conversion to `boolean` is not allowed in Java.

![Flow diagram contrasting widening primitive conversion with explicit narrowing and possible information loss.](../shared/assets/primitive-conversion.svg)

**Key takeaway:** Before converting, ask whether the target type can represent the source value without losing information.

## 27. Implicit type casting

An implicit conversion happens automatically when a value is assigned or passed to a compatible wider type. For example, an `int` can be widened to a `long` or `double` without a cast. Widening from an integer to a floating-point type can still lose precision for sufficiently large values.

**Example:**

```java
int items = 12;
long totalItems = items; // widening: no cast needed

float approximate = items; // int can widen to float
double precise = approximate; // float can widen to double
```

Java does not implicitly narrow a value in an assignment:

```java
double reading = 4.8;
// int count = reading; // compile-time error: narrowing requires an explicit cast
```

**Key takeaway:** Widening conversions usually need no cast, but a wider destination does not guarantee perfect precision for every numeric type.

## 28. Explicit type casting

An explicit cast tells Java to convert a value even when the conversion may discard information. The programmer is responsible for checking whether the result is meaningful.

**Example:**

```java
double price = 19.99;
int wholeDollars = (int) price; // 19; fractional part is discarded

int codePoint = 65;
char letter = (char) codePoint;
System.out.println(letter); // A
```

Casting does not round `19.99` to `20`. For an out-of-range integer conversion, high-order bits can be discarded; for a floating-point value outside the integer range, the result is limited by Java's conversion rules. Check or validate ranges before narrowing when the input may vary.

```java
long count = 2_000_000_000L;
if (count <= Integer.MAX_VALUE && count >= Integer.MIN_VALUE) {
    int safeCount = (int) count;
    System.out.println(safeCount);
}
```

**Key takeaway:** A cast permits a conversion; it does not make a lossy conversion safe.

## 29. Type promotion

Java promotes small integral operands such as `byte`, `short`, and `char` to `int` for most arithmetic operations. If an expression combines different numeric types, the operands are generally promoted to a common wider type before the operation. The expression's result type can therefore differ from the variables used to calculate it.

**Example:**

```java
byte left = 10;
byte right = 20;
int sum = left + right; // operands are promoted to int
// byte smallSum = left + right; // compile-time error without a cast
byte smallSum = (byte) (left + right);
```

Integer arithmetic can overflow before assignment to a wider destination:

```java
int a = 1_500_000_000;
int b = 1_500_000_000;
long wrong = a + b;          // addition overflows as int first
long correct = (long) a + b; // promote before addition
```

**Key takeaway:** Check the type of the whole expression, not only the type of the destination variable.

## 30. Operators

An operator performs an operation on one or more operands. Java groups operators by purpose: arithmetic, comparison, logical, assignment, unary, bitwise, and shift operators. Some operators require numeric operands, while logical operators require boolean values.

**Example:**

```java
int remaining = 10 - 3;        // arithmetic
boolean enough = remaining >= 5; // comparison
boolean canContinue = enough && true; // logical
```

An expression combines values, variables, method calls, and operators. Parentheses make the intended grouping clearer; use them when they improve readability even if precedence already determines the same result.

**Key takeaway:** Know each operator's operand types and result type before combining operators in an expression.

### Special operators often asked about in interviews

#### The conditional (ternary) operator: `? :`

The conditional operator is called *ternary* because it takes three operands. It evaluates a boolean condition and produces one of two values. Use it for a short choice; prefer `if/else` when the logic becomes difficult to read.

**Syntax:** `condition ? valueIfTrue : valueIfFalse`

**Example:**
```java
int marks = 75;
String result = (marks >= 40) ? "Pass" : "Fail";
System.out.println(result); // Pass
```

#### The `new` operator

The `new` operator creates an object or array. For an object, it requests allocation from the runtime, invokes a constructor, and produces a reference to the created object.

**Example:**
```java
class Dog {
    String breed = "Labrador";
}
class Main {
    public static void main(String[] args) {
        Dog pet = new Dog();
        System.out.println(pet.breed); // Labrador
    }
}
```

#### The `instanceof` operator

`instanceof` tests whether a non-null object reference is compatible with a specified reference type. It returns a boolean and is often used before a downcast. It returns `false` for `null`.

**Example:**
```java
class Animal {}
class Dog extends Animal {}
class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;
            System.out.println(dog.getClass().getSimpleName()); // Dog
        }
    }
}
```

**Special-operator summary**

| Operator | Purpose | Result | Example |
|---|---|---|---|
| `? :` | Choose one of two expressions | A value determined by the branches | `marks >= 40 ? "Pass" : "Fail"` |
| `new` | Create an object or array | Reference to the created object/array | `new Dog()` |
| `instanceof` | Test reference-type compatibility | `boolean` | `animal instanceof Dog` |

## 31. Arithmetic operators

The arithmetic operators are `+`, `-`, `*`, `/`, and `%`. Integer division discards the fractional part toward zero. The remainder operator `%` gives the remainder after division and can be useful for divisibility checks.

**Example:**

```java
int quotient = 17 / 5;  // 3
int remainder = 17 % 5; // 2
double precise = 17.0 / 5; // 3.4

boolean isEven = 18 % 2 == 0;
```

Integer division by zero throws `ArithmeticException`. Floating-point division by zero follows floating-point rules and may produce infinity or `NaN` instead. Integer arithmetic can overflow without throwing an exception.

**Key takeaway:** Use a floating-point operand when fractional division is intended, and check integer divisors before dividing.

## 32. Relational operators

Relational operators compare numeric values: `<`, `<=`, `>`, and `>=`. Equality operators `==` and `!=` also compare primitive values. A comparison expression evaluates to a boolean.

**Example:**

```java
int age = 20;
boolean adult = age >= 18;
boolean sameNumber = 5 == 5; // true
```

For reference variables, `==` checks whether both references identify the same object, not whether two objects have equal contents. Use `.equals()` for logical equality when the class defines it appropriately.

```java
String first = new String("Java");
String second = new String("Java");
System.out.println(first == second);      // false: different objects
System.out.println(first.equals(second)); // true: equal text
```

**Key takeaway:** Use `==` for primitive values and reference identity; use `.equals()` when comparing object contents.

## 33. Logical operators

Logical operators combine or invert boolean expressions. `&&` means AND, `||` means OR, and `!` means NOT. The conditional operators `&&` and `||` short-circuit: Java skips the right operand when the left operand already determines the result.

**Example:**

```java
int[] values = {4, 8, 12};
int index = 1;
boolean validAndPositive =
        index >= 0 && index < values.length && values[index] > 0;
```

The bounds checks run before `values[index]` because `&&` evaluates left to right and stops when a condition is false. This prevents an invalid array access in this expression. The non-short-circuit boolean operators `&` and `|` evaluate both operands; use them with booleans only when that behavior is intentional.

**Key takeaway:** Short-circuit logic is useful for safe guards and clear compound conditions.

## 34. Assignment operators

The basic assignment operator `=` stores the right-hand value in the variable on the left. Compound assignments such as `+=`, `-=`, `*=`, and `/=` combine an operation with assignment.

**Example:**

```java
int points = 10;
points += 5; // same effect as points = points + 5
points *= 2; // same effect as points = points * 2
System.out.println(points); // 30
```

Compound assignment includes an implicit conversion back to the left-hand type, unlike the expanded expression:

```java
short value = 10;
value += 2; // allowed; compound assignment converts the result back to short
// value = value + 2; // compile-time error: the expression is int
```

**Key takeaway:** Assignment changes a variable; it is not the same as equality comparison (`==`).

## 35. Unary operators

Unary operators act on one operand. Common examples are unary plus (`+`), negation (`-`), logical complement (`!`), increment (`++`), decrement (`--`), and bitwise complement (`~`).

**Example:**

```java
int count = 4;
int before = count++; // use 4, then increment count to 5
int now = ++count;    // increment count to 6, then use 6
boolean active = true;
boolean inactive = !active;
```

Prefix and postfix increment both change the variable; they differ in which value the expression produces. Avoid embedding `++` inside long expressions, where evaluation order is difficult to see.

**Key takeaway:** Prefer a separate increment statement when it makes the order of updates easier to understand.

## 36. Bitwise operators

Bitwise operators work on individual bits of integral values. `&` ANDs corresponding bits, `|` ORs them, `^` XORs them, and `~` flips the bits of one operand. They are useful for masks, flags, and low-level data work.

**Example:**

```java
int READ = 1;   // binary ...0001
int WRITE = 2;  // binary ...0010
int permissions = READ | WRITE;

boolean canWrite = (permissions & WRITE) != 0;
permissions = permissions & ~WRITE; // clear the WRITE bit
```

Unlike `&&` and `||`, bitwise `&` and `|` evaluate both operands. For boolean operands that can matter; for integer operands they operate on bits.

**Key takeaway:** Use bitwise operators for explicit bit manipulation; use logical operators for ordinary boolean conditions.

## 37. Shift operators

Shift operators move the bits of an integral value. `<<` shifts left, `>>` shifts right while preserving the sign bit, and `>>>` shifts right while filling with zero bits. Java masks the shift distance to the width of the promoted left operand.

**Example:**

```java
int flags = 1;
int secondBit = flags << 1; // 2
int half = 16 >> 1;         // 8
int lowBits = -1 >>> 1;     // shifts in zeros on the left
```

For non-negative numbers within range, left shift by one often has the same effect as multiplying by two. Shifting does not prevent integer overflow, and a shift is not always a clearer or safer replacement for multiplication or division.

**Key takeaway:** Use shifts when the operation is genuinely about bits; choose `>>` or `>>>` based on the desired sign behavior.

## 38. Ternary operator

The conditional (ternary) operator `condition ? valueIfTrue : valueIfFalse` chooses one of two expressions and produces a value. Its condition must be boolean.

**Example:**

```java
int temperature = 28;
String message = temperature >= 30 ? "Hot" : "Comfortable";
System.out.println(message);
```

Use it for a short, straightforward choice. For multiple branches or expressions with side effects, an `if`/`else` statement is usually easier to read. Both result expressions must be compatible with the type Java determines for the whole conditional expression.

**Key takeaway:** A ternary expression is a compact value-producing choice, not a replacement for every `if`/`else`.

## 39. Operator precedence and associativity

Precedence determines which operators are grouped first; associativity determines grouping when operators share the same precedence. For example, multiplication has higher precedence than addition, and arithmetic operators of the same level generally group from left to right.

**Example:**

```java
int result = 2 + 3 * 4;     // 14
int grouped = (2 + 3) * 4;  // 20
int subtraction = 20 - 5 - 3; // (20 - 5) - 3 = 12
```

Parentheses make intent explicit and prevent mistakes when boolean, arithmetic, and comparison operators are combined. Do not rely on memorizing the entire precedence table when a pair of parentheses makes the code clearer.

**Key takeaway:** Use parentheses to communicate the grouping you intend, especially in complex expressions.

![Diagram showing the evaluation order of a mixed arithmetic expression and how parentheses change the grouping.](../shared/assets/operator-evaluation.svg)

## 40. Command-line arguments

Java passes command-line arguments to `main` in the `String[] args` array. Each argument is text, even when it looks like a number; convert it before doing numeric operations. The first argument is at index `0`.

**Example:**

```java
public class AddArguments {
    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("Usage: java AddArguments <first> <second>");
            return;
        }

        int first = Integer.parseInt(args[0]);
        int second = Integer.parseInt(args[1]);
        System.out.println(first + second);
    }
}
```

Run it with `java AddArguments 12 30` after compiling; the output is `42`. `Integer.parseInt` throws `NumberFormatException` if an argument is not a valid integer, so robust command-line programs should handle invalid input and explain the expected format.

**Key takeaway:** Check `args.length` before indexing and parse text into the type your calculation needs.

## 41. User input using `Scanner`

`Scanner` can read tokens and lines from an input source such as `System.in`. It provides methods such as `nextInt()`, `nextDouble()`, and `nextLine()`.

**Example:**

```java
import java.util.Scanner;

class ReadAge {
    public static void main(String[] args) {
        try (Scanner input = new Scanner(System.in)) {
            System.out.print("Age: ");
            int age = input.nextInt();
            System.out.println("Next year: " + (age + 1));
        }
    }
}
```

Token-reading methods stop at a delimiter (whitespace by default). A common surprise occurs when `nextInt()` is followed by `nextLine()`: the line method may consume the rest of the current line, including its pending newline. Consume that remainder first if you then need a full line. `Scanner` can also throw `InputMismatchException` when input does not match the requested type.

**Key takeaway:** Choose token or line input deliberately, validate user input, and close a `Scanner` for `System.in` only when the program is finished reading from standard input.

## 42. User input using `BufferedReader`

`BufferedReader` reads text efficiently, usually one line at a time. `readLine()` returns a `String` or `null` at end-of-input; parsing is a separate step. It is useful when line-based input is desired or many lines need to be read.

**Example:**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

class ReadQuantity {
    public static void main(String[] args) throws IOException {
        BufferedReader input =
                new BufferedReader(new InputStreamReader(System.in));
        System.out.print("Quantity: ");
        String line = input.readLine();
        int quantity = Integer.parseInt(line);
        System.out.println("Double: " + (quantity * 2));
    }
}
```

`Integer.parseInt` throws `NumberFormatException` when the line is not an integer. `readLine()` can throw `IOException`, which the example declares with `throws IOException`; another design is to catch and report the error. For more involved applications, specify a character encoding explicitly when constructing a reader.

**Key takeaway:** `BufferedReader` gives you text; parse and validate that text before using it as a number.

## Interview questions and answers

### 1. Does Java have global variables? If not, why?

Java does not allow a variable declaration at the top level outside a type. Use an instance field for per-object state, or a `static` field for class-level state. Prefer constants or explicitly passed dependencies over mutable global-like state because shared mutable data can make programs harder to test and reason about.

**Example:**
```java
class Settings {
    static final int MAX_USERS = 100;
}
```

### 2. What is the difference between a local variable, an instance variable, and a static variable?

A local variable is declared inside a method or block and must be initialized before it is read. An instance variable belongs to each object. A static variable belongs to the class and is shared by its instances.

**Example:**
```java
class Counter {
    static int totalCounters;
    int value;

    Counter(int value) {
        this.value = value;
        totalCounters++;
    }

    void printNext() {
        int next = value + 1;
        System.out.println(next);
    }
}
```

### 3. Why does a local variable not receive a default value?

Java requires local variables to be definitely assigned before use. This catches a class of mistakes at compile time. Fields and array elements do receive defaults, such as `0`, `false`, and `null`.

**Example:** `int number; System.out.println(number);` does not compile until `number` is assigned a value.

### 4. Why is `String` a reference type instead of a primitive type?

`String` is a class with behavior and methods, such as `length()`, `substring()`, and `equals()`. A `String` variable holds a reference to a String object (or `null`), while primitive types hold primitive values.

**Example:**
```java
String language = "Java";
System.out.println(language.length()); // 4
```

### 5. What is the difference between `=` and `==`?

`=` assigns a value to a variable. `==` compares primitive values, or checks whether two references point to the same object. Use `.equals()` to compare object contents when the class defines meaningful equality.

**Example:**
```java
int score = 10;
System.out.println(score == 10); // true
```

### 6. What is the difference between `&&` and `&`?

For boolean expressions, `&&` short-circuits: if the left side is false, Java does not evaluate the right side. `&` evaluates both boolean operands. With integral operands, `&` performs bitwise AND.

**Example:**
```java
int[] numbers = {10};
int index = 2;
if (index >= 0 && index < numbers.length) {
    System.out.println(numbers[index]);
} // the array access is skipped when the bounds check fails
```

### 7. What is the difference between pre-increment and post-increment?

Both `++x` and `x++` increase `x` by one. Prefix increment produces the updated value; postfix increment produces the old value as the expression result.

**Example:**
```java
int x = 5;
int old = x++;       // old = 5, x = 6
int updated = ++x;   // x = 7, updated = 7
```

## Practical exercises

Complete these tasks in Eclipse or from the command line. Each task should be a small, runnable Java program unless it asks for an explanation.

1. Declare one variable of each primitive type and print its value.
2. Create a class with fields of all eight primitive types. Print their default values, then explain why the same approach does not work for uninitialized local variables.
3. Write a program that reads two integers and prints their sum, difference, product, quotient, and remainder. Decide how to handle a divisor of zero.
4. Convert a `double` value such as `19.99` to an `int`. Explain why the result is truncated rather than rounded.
5. Check whether a number is within the range 1 through 100 using relational and logical operators.
6. Use a ternary operator to print whether a student passed a test with a pass mark of 40. Rewrite it with `if`/`else` and compare readability.
7. Demonstrate prefix and postfix increment with separate variables and predict the output before running the program.
8. Use bitwise OR to combine two flags, bitwise AND to check a flag, and bitwise complement to clear a flag.
9. Calculate `2 + 3 * 4` and `(2 + 3) * 4`. Explain how precedence and parentheses change the result.
10. Create a `Counter` class with an instance field and a static field. Make two objects and demonstrate which value is shared.
11. Write a program that accepts two command-line arguments, converts them to integers, and prints their sum. Handle missing or invalid arguments.
12. Build a small bill calculator that stores item price, quantity, subtotal, tax percentage, and final total using appropriate data types.

## Chapter 2 coverage check

All 26 topics listed for Chapter 2 in the master roadmap are covered above. Several related details are included alongside their parent topics so the chapter stays aligned with the approved outline: integer overflow during promotion, floating-point approximation, `String` equality, `null`, input validation, and the `Scanner.nextInt()`/`nextLine()` boundary.

The roadmap does not currently list a dedicated section for enums, local-variable type inference (`var`), or exact decimal arithmetic with `BigDecimal`. These are useful follow-up topics, but are left out of this chapter until they are added to the syllabus.

## Operator reference tables

These tables collect the operators covered above for quick revision.

### Arithmetic operators

| Operator | Name | Description | Example (`int a = 10, b = 3`) | Result |
|---|---|---|---|---:|
| `+` | Addition | Adds values; can also concatenate strings | `a + b` | `13` |
| `-` | Subtraction | Subtracts the right operand from the left | `a - b` | `7` |
| `*` | Multiplication | Multiplies values | `a * b` | `30` |
| `/` | Division | Integer operands produce an integer quotient | `a / b` | `3` |
| `%` | Remainder | Returns the remainder after division | `a % b` | `1` |

### Relational operators

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `10 == 10` | `true` |
| `!=` | Not equal to | `10 != 3` | `true` |
| `>` | Greater than | `10 > 3` | `true` |
| `<` | Less than | `10 < 3` | `false` |
| `>=` | Greater than or equal to | `10 >= 10` | `true` |
| `<=` | Less than or equal to | `3 <= 10` | `true` |

### Logical operators

| Operator | Name | Meaning | Example | Result |
|---|---|---|---|---|
| `&&` | Logical AND | Both conditions must be true | `(5 > 3 && 8 > 5)` | `true` |
| `||` | Logical OR | At least one condition is true | `(5 > 3 || 8 < 5)` | `true` |
| `!` | Logical NOT | Reverses a boolean value | `!(5 > 3)` | `false` |

### Assignment operators

| Operator | Meaning | Example | Equivalent form |
|---|---|---|---|
| `=` | Assign | `a = 10` | `a = 10` |
| `+=` | Add and assign | `a += 5` | `a = a + 5` |
| `-=` | Subtract and assign | `a -= 5` | `a = a - 5` |
| `*=` | Multiply and assign | `a *= 5` | `a = a * 5` |
| `/=` | Divide and assign | `a /= 5` | `a = a / 5` |
| `%=` | Remainder and assign | `a %= 5` | `a = a % 5` |

### Unary operators

| Operator | Name | Example | Notes |
|---|---|---|---|
| `++x` | Prefix increment | `int y = ++x;` | Increments first, then yields the new value |
| `x++` | Postfix increment | `int y = x++;` | Yields the old value, then increments |
| `--x` / `x--` | Decrement | `x--;` | Decreases by one |
| `!` | Logical NOT | `!ready` | Inverts a boolean |
| `-` | Unary minus | `-x` | Negates a numeric value |
| `~` | Bitwise complement | `~mask` | Flips each bit of an integral value |

### Bitwise and shift operators

| Operator | Name | What it does |
|---|---|---|
| `&` | Bitwise AND | Result bit is 1 when both corresponding bits are 1 |
| `|` | Bitwise OR | Result bit is 1 when either corresponding bit is 1 |
| `^` | Bitwise XOR | Result bit is 1 when corresponding bits differ |
| `~` | Bitwise complement | Flips every bit |
| `<<` | Left shift | Shifts bits left, filling low bits with zero |
| `>>` | Signed right shift | Shifts right while preserving the sign bit |
| `>>>` | Unsigned right shift | Shifts right while filling high bits with zero |

**Shift examples:** `5 << 1` produces `10`; `16 >> 2` produces `4`; `-1 >>> 1` produces `2147483647` for an `int`.

### Common operator precedence (highest to lowest for these groups)

1. Postfix: `x++`, `x--`
2. Unary: `++x`, `--x`, `+`, `-`, `!`, `~`
3. Multiplicative: `*`, `/`, `%`
4. Additive: `+`, `-`
5. Shift: `<<`, `>>`, `>>>`
6. Relational and type test: `<`, `<=`, `>`, `>=`, `instanceof`
7. Equality: `==`, `!=`
8. Bitwise AND, XOR, OR: `&`, `^`, `|`
9. Logical AND, OR: `&&`, `||`
10. Conditional: `? :`
11. Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `%=`

Use parentheses when they make the intended grouping clearer.

