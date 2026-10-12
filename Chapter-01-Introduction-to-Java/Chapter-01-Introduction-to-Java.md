# Chapter 1: Introduction to Java

## 1. What is Java?
Java is a high-level, general-purpose, class-based programming language and platform. Java source code is compiled into bytecode, which a compatible Java Virtual Machine (JVM) executes.

~~~text
Main.java --javac--> Main.class (bytecode) --JVM--> program runs
~~~

## 2. History of Java
Java began at Sun Microsystems in the early 1990s as part of the Green Project, which explored software for consumer electronic devices. James Gosling was a key designer. Oak is the best-documented early name; the name was later changed to Java. Sun announced Java publicly in 1995, and Java 1.0 was released on 23 January 1996. Java did not invent the World Wide Web; web software became an important use for Java as the Web grew. Some secondary sources mention GreenTalk and .gt in early naming accounts, but accounts of that stage are not consistent.

## 3. Why Java was created
The project sought portability across different devices, reliability, security, and a productive programming environment. C and C++ already existed and remain useful; Java offered a different balance with bytecode, a managed runtime, garbage collection, and a broad standard library.

## 4. Features
- Object-oriented programming with classes, objects, encapsulation, inheritance, and polymorphism.
- Platform portability through bytecode and compatible JVMs.
- Automatic garbage collection for managed objects.
- Strong compile-time type checking and runtime checks.
- Built-in support for threads and concurrency APIs.
- Networking and extensive standard libraries.
- Runtime class loading and JIT optimization.
These features reduce some risks but do not make programs automatically bug-free, secure, or faster in every situation.

## 5. Applications
Java is used for backend services, enterprise systems, APIs, Android codebases, desktop applications, data processing, cloud services, developer tools, and some embedded environments. Java itself is not a database; Java programs can connect to databases using drivers and APIs.

## 6. Java editions
- Java SE: core language and standard libraries for general-purpose development.
- Jakarta EE: specifications and APIs for enterprise and server applications. It was formerly Java EE; many migrated APIs use the jakarta.* namespace.
- Java ME: technologies for certain constrained or embedded devices.
They serve different needs and are not interchangeable labels.

## 7. Java versions, release history, and what changed

Java version numbers tell you which language, library, JVM, and tooling features became available. Java 8, 11, 17, 21, and 25 are widely used LTS releases; LTS means a vendor offers a longer support window, not that every vendor has identical dates or terms. Since Java 9, feature releases have generally arrived every six months. A newer Java can run older bytecode in many cases, but compatibility is not automatic in every situation: removed APIs, changed defaults, dependencies, and build settings can matter.

### Major milestones

| Release | Date | Important additions or changes (highlights, not every change) |
|---|---|---|
| Java 1.0 | Jan 1996 | First public production release; core language/runtime and standard APIs. |
| Java 1.1 | Feb 1997 | Inner classes, JavaBeans-related support, JDBC and RMI APIs. |
| Java 2 / Java 1.2 | Dec 1998 | Collections framework, Swing, major standard-library and JVM improvements. |
| Java 5 (1.5) | Sep 2004 | Generics, annotations, enums, enhanced for-loop, autoboxing/unboxing, varargs, concurrency utilities. |
| Java 6 | Dec 2006 | Library/tooling improvements, scripting support, compiler APIs; no major new syntax headline. |
| Java 7 | Jul 2011 | try-with-resources, diamond operator `<>`, multi-catch, strings in `switch`, binary literals and numeric underscores, NIO.2. |
| Java 8 (LTS for many vendors) | Mar 2014 | Lambda expressions, method references, streams, functional interfaces, default methods, and the `java.time` date/time API. |
| Java 9 | Sep 2017 | Java Platform Module System (JPMS), JShell, collection factory methods, and improved process/API support. |
| Java 10 | Mar 2018 | Local-variable type inference with `var` (for eligible local variables; not a dynamic type). |
| Java 11 (LTS for many vendors) | Sep 2018 | Standardized HTTP Client API, single-file source launch, new String/file methods, and removal of some older Java EE/CORBA modules from the JDK. |
| Java 12–13 | 2019 | Switch expressions and text blocks appeared as preview features; previews were not yet final features. |
| Java 14 | Mar 2020 | Switch expressions became final; helpful NullPointerException messages; records appeared as preview. |
| Java 15 | Sep 2020 | Text blocks became final; sealed classes and records continued through preview stages. |
| Java 16 | Mar 2021 | Records became final; pattern matching for `instanceof` became final; `jpackage` became a standard tool. |
| Java 17 (LTS) | Sep 2021 | Sealed classes became final; strong encapsulation of JDK internals; pattern matching for switch remained preview. |
| Java 18 | Mar 2022 | UTF-8 became the default charset; simple web server tool; `@snippet` support for documentation. |
| Java 19–20 | 2022–2023 | Virtual threads, structured concurrency, and some pattern-matching work were preview/incubator features—not all final yet. |
| Java 21 (LTS) | Sep 2023 | Virtual threads, record patterns, pattern matching for switch, and sequenced collections became final; string templates were preview at this release. |
| Java 22–24 | 2024–2025 | Foreign Function & Memory API became final in Java 22; continued work on language previews, performance, garbage collection, and developer tools. Check each JEP/release notes for the exact status of a feature in a specific release. |
| Java 25 (LTS) | Sep 2025 | Current LTS generation as of this note; includes compact source files and instance main methods as final features, plus other language, library, runtime, and performance changes. Exact support periods depend on the vendor. |

**Important:** this is a learning timeline of selected headline changes, not a complete list of every API or bug fix. A feature marked *preview* or *incubator* was experimental and could require special flags; it should not be treated as a normal finalized language feature for that release.

### LTS versus non-LTS

- **LTS:** a vendor-supported long-term baseline that organizations often choose for production, such as Java 8, 11, 17, 21, or 25.
- **Non-LTS / interim feature release:** delivers newer features sooner, but typically has a shorter support window.
- Oracle's support policy and the policies of OpenJDK distributors such as Eclipse Temurin can differ. Always check the exact vendor, build, and support policy rather than assuming a universal end-of-support date.
- For a new learning project, use a currently supported JDK such as 25 LTS if your IDE and course setup support it. If a course or project specifically targets Java 17 or 21, use that version for consistency.

### Check the Java version installed on your computer

~~~bash
java -version
javac -version
~~~

- `java -version` reports the runtime/launcher version selected by your PATH.
- `javac -version` reports the compiler version selected by your PATH.
- They should normally come from the JDK you intend to use. On Windows, `where java` and `where javac` help identify which executable is being used.
- In Eclipse, also check **Window > Preferences > Java > Installed JREs** (the exact menu can vary by version) and the project's **Java Compiler** settings. The command-line JDK and Eclipse project compliance level can differ.

### Why version matters in practice

For example, records became a final feature in Java 16, and virtual threads became final in Java 21. Code using either feature will not compile on older language levels that do not support it. In Eclipse, a project set to Java 17 can reject newer syntax even if a newer JDK is installed. Set the project's JRE/JDK and compiler compliance level intentionally, and check library/deployment compatibility before upgrading.

## 8. Install and verify the JDK
For development, install a JDK, which includes the compiler and runtime components. Common distributions include Eclipse Temurin, Oracle JDK, and Amazon Corretto. On Windows, if a command is not found, locate the actual JDK installation and check whether its bin directory is on PATH, then open a new terminal. You have already installed Eclipse Temurin and verified both commands, so you can continue to the examples.

Useful Windows checks:

~~~bat
where java
where javac
~~~

On macOS or Linux, use which java and which javac.

## 9. IDE and command line
An IDE such as Eclipse combines a code editor, project/build tools, run controls, debugger, and console. The editor is where you write code; the compiler translates source; the launcher starts the program; the console displays output and diagnostics. Eclipse may compile automatically when you save, depending on settings.

In Eclipse: open the Java project, open or create a class under the source folder, write code, save, choose Run As > Java Application, and read the Console.

## 10. Structure of a Java program
Create a file named Main.java:

~~~java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
~~~

- public class Main declares a class named Main.
- The public top-level class name should match the filename, including capitalization.
- main is the entry-point method for this basic application.
- public controls access; static means the method can be called without creating a Main object; void means it returns no value.
- String[] args holds command-line arguments as strings.
- System.out.println prints text and moves to a new line.
- Java is case-sensitive, braces delimit blocks, and statements commonly end with semicolons.
- // starts a single-line comment; /* ... */ is a block comment.

## 11. First program: editor to output
Step 1: Write the Main.java code shown above in Eclipse or a text editor and save it.

Step 2: In a terminal opened in the folder containing Main.java, compile:

~~~bash
javac Main.java
~~~

Successful compilation normally produces no message and creates Main.class in the output folder.

Step 3: Run the class:

~~~bash
java Main
~~~

Expected output:

~~~text
Hello, Java!
~~~

Step 4: Change the editor code to:

~~~java
public class Main {
    public static void main(String[] args) {
        System.out.println("I am learning Java!");
    }
}
~~~

Save, compile again using javac Main.java, and run again using java Main. New output:

~~~text
I am learning Java!
~~~

If you change the source but do not rebuild, the class file may still contain the previous compiled version.

## 12. Compilation and execution
Compilation and execution are separate steps. javac Main.java compiles source code. java Main launches the compiled class; omit the .class extension. An IDE can automate these steps, but understanding them helps you diagnose problems.

Example with a deliberate error (missing semicolon):

~~~java
System.out.println("Hello, Java!")
~~~

The compiler reports a syntax error. Correct it to:

~~~java
System.out.println("Hello, Java!");
~~~

Save and compile again. Exact diagnostic wording depends on the JDK.

## 13. Bytecode
Bytecode is the intermediate instruction format normally stored in .class files. The JVM loads and verifies classes, then interprets bytecode and may JIT-compile frequently executed code into native machine instructions. Bytecode supports portability, but platform-specific paths, native libraries, and external dependencies can still affect portability.

## 14. JDK, JRE, JVM
- JVM: loads, verifies, and executes bytecode.
- JRE: conceptual runtime environment containing a JVM and runtime libraries; modern distributions do not always ship a separate general-purpose JRE download.
- JDK: development kit containing tools such as javac plus runtime components.
Memory aid: JDK for development, JRE as the runtime concept, JVM for executing bytecode.

## 15. .java and .class files
- Main.java contains human-readable source code.
- Main.class contains compiled bytecode.
After compiling, list files with dir on Windows or ls on macOS/Linux. Do not edit the .class file as if it were source; edit the .java file and recompile.

## 16. Compiler and launcher
~~~bash
javac Main.java
java Main
~~~

javac compiles the source file; java launches the class named Main. If javac is not found, check that a JDK is installed and its bin directory is discoverable. If the main class cannot be found, confirm you are in the correct directory and that Main.class exists.

## 17. Write Once, Run Anywhere
The same compiled bytecode can run on different platforms when each has a compatible JVM and the required libraries. This is the goal behind Java's WORA phrase, not a guarantee that every program is free of operating-system-specific assumptions.

## 18. Workflow
1. Understand the task.
2. Create a project or source file.
3. Write and save code.
4. Compile or build.
5. Read and fix errors.
6. Run the program.
7. Compare output with expectations.
8. Change code and repeat.
9. Test normal, boundary, and invalid inputs.

~~~text
Plan -> Edit -> Save -> Compile -> Fix errors
                           |
                           v
                    Run -> Check output
                           |
                           v
                    Modify and repeat
~~~

## 19. Common errors
- javac is not recognized: verify JDK installation and PATH; open a new terminal after changes.
- Public class/file mismatch: rename the file or class so names match.
- ';' expected: inspect the indicated line and nearby lines for a missing semicolon or syntax issue.
- Could not find or load main class: check current directory, classpath, compilation result, and class name.
- Main method not found: use public static void main(String[] args) for this example.
- Old output appears: save and rebuild, and ensure the correct class/project is running.
- Eclipse errors: inspect capitalization, braces, semicolons, selected JDK, and the Problems/Console views.

## 20. Quick revision
- Java started at Sun Microsystems; the Green Project explored consumer-device software.
- Oak is the best-documented early name; Java was announced in 1995 and Java 1.0 released in 1996.
- Source file: .java. Compiled bytecode file: .class.
- javac compiles; java launches; JVM executes bytecode.
- JDK supplies development tools; JRE is the runtime concept.
- Java's portability depends on compatible runtimes and dependencies.

## 21. Practice questions
1. Define Java.
2. What was the Green Project?
3. What early name is best documented in Java's history?
4. When was Java announced and when was Java 1.0 released?
5. Why was Java created when C and C++ already existed?
6. Explain five Java features.
7. Compare Java SE, Jakarta EE, and Java ME.
8. What does LTS mean?
9. Explain JDK, JRE, and JVM.
10. What is bytecode?
11. Differentiate .java and .class files.
12. What do javac and java do?
13. Why might output not change after editing source?
14. Create a program that prints your name.
15. Remove a semicolon, observe the compiler error, fix it, and compile again.
16. Run java -version and javac -version and record the versions.

## Further reading
- Oracle, A Brief History of Java: https://education.oracle.com/file/general/4955_BriefHistoryOfJava_7.pdf
- JVM Specification: https://docs.oracle.com/en/java/javase/26/docs/specs/jvms/jvms-1.html
- Oracle Java: https://www.oracle.com/java/
- Eclipse IDE: https://eclipseide.org/
- Eclipse Temurin: https://adoptium.net/

---
End of Chapter 1. All chapter notes and the guided code workflow are collected in this single Markdown file.
