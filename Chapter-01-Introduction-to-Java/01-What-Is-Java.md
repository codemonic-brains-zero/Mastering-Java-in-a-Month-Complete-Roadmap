# Chapter 1: Introduction to Java

## Topic 1 — What Is Java?

### 1. Definition

**Java is a high-level, general-purpose, class-based, object-oriented programming language.** It is designed so that compiled Java programs can run on different operating systems when a compatible Java Virtual Machine (JVM) is available.

In simple words, Java lets us write instructions for a computer using a readable programming language. Java tools compile the source code into **bytecode**, and a JVM runs that bytecode.

### 2. A simple mental model

```text
Java source code (.java)
        |
        | javac compiler
        v
Java bytecode (.class)
        |
        | JVM
        v
Program runs on the computer
```

- **Source code** is the Java code written by a programmer.
- **Compiler (`javac`)** checks and translates Java source code into bytecode.
- **Bytecode** is the intermediate instruction format stored in a `.class` file.
- **JVM (Java Virtual Machine)** executes bytecode. Different operating systems can have their own compatible JVM implementations.

This is the idea behind Java's famous principle: **“Write Once, Run Anywhere”**—although a program can still depend on operating-system features or external libraries.

### 3. Our first tiny example

Create a file named `Main.java` and type:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

**Expected output**

```text
Hello, Java!
```

### 4. Understand the code

- `public class Main` declares a class named `Main`. In Java, code is organized around classes.
- `public static void main(String[] args)` declares the main method, which the Java launcher uses as the entry point for this simple application.
- `System.out.println(...)` prints the supplied text and then moves to a new line.
- `"Hello, Java!"` is a string literal: text enclosed in double quotation marks.
- The semicolon `;` ends the statement.

### 5. Run it in Eclipse

1. Open your Java project in Eclipse.
2. In the **Package Explorer**, right-click the source folder (usually `src`).
3. Select **New → Class**.
4. Enter `Main` as the class name and, if shown, tick the option to create `public static void main(String[] args)`.
5. Click **Finish**. Add the `System.out.println("Hello, Java!");` statement inside the main method.
6. Save the file, then click the green **Run** button.
7. Check the **Console** view for `Hello, Java!`.

If you already created and ran a first Java program during setup, you can use that program to review these parts rather than creating a duplicate class.

### 6. Key takeaways

- Java is a programming language; the JVM is the runtime engine that executes Java bytecode.
- Java source files usually use the `.java` extension.
- Compiled Java bytecode is stored in `.class` files.
- The `javac` compiler produces bytecode, and the JVM executes it.
- `main` is the entry point for this basic Java application.

### 7. Check your understanding

Try answering these before moving to the next topic:

1. What is Java used for?
2. What is the difference between a `.java` file and a `.class` file?
3. What does the JVM do?
4. Which statement prints `Hello, Java!`?
5. In your own words, what does “Write Once, Run Anywhere” mean?

**Next topic:** The origin and history of Java.
