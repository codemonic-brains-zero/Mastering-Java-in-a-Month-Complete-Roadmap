# Mastering Java in a Month

An interactive Java learning roadmap with chapter notes, JVM/JRE/JDK diagrams, and a Java playground.

## Live site

[Open the GitHub Pages site](https://codemonic-brains-zero.github.io/Mastering-Java-in-a-Month-Complete-Roadmap/)

## Repository structure

```text
.
+-- index.html
+-- roadmap/
|   +-- java-learning-roadmap.md
+-- mastering-java/
    +-- chapter-01-introduction-to-java/
    |   +-- chapter-01-introduction-to-java.html
    |   +-- chapter-01-introduction-to-java.md
    +-- chapter-02-variables-data-types-and-operators/
    |   +-- chapter-02-variables-data-types-and-operators.html
    |   +-- chapter-02-variables-data-types-and-operators.md
    +-- chapter-03-control-flow-and-arrays/
    |   +-- chapter-03-control-flow-and-arrays.html
    |   +-- chapter-03-control-flow-and-arrays.md
    +-- shared/
        +-- index.html
        +-- assets/
            +-- java-primitive-types.svg
            +-- operator-evaluation.svg
            +-- primitive-conversion.svg
            +-- variable-ownership.svg
            +-- loop-control-flow.svg
            +-- array-indexing.svg
            +-- array-reference-structure.svg
```

- [`roadmap/java-learning-roadmap.md`](roadmap/java-learning-roadmap.md) contains the complete Java syllabus.
- [`mastering-java/chapter-01-introduction-to-java/chapter-01-introduction-to-java.md`](mastering-java/chapter-01-introduction-to-java/chapter-01-introduction-to-java.md) contains the Chapter 1 lesson notes.
- [`mastering-java/chapter-02-variables-data-types-and-operators/chapter-02-variables-data-types-and-operators.md`](mastering-java/chapter-02-variables-data-types-and-operators/chapter-02-variables-data-types-and-operators.md) contains Chapter 2 lesson explanations, Java examples, takeaways, and its coverage check against the master roadmap.
- [`mastering-java/chapter-03-control-flow-and-arrays/chapter-03-control-flow-and-arrays.md`](mastering-java/chapter-03-control-flow-and-arrays/chapter-03-control-flow-and-arrays.md) contains Chapter 3 lesson explanations and Java examples.
- Each named chapter HTML page opens the shared UI in [`mastering-java/shared/index.html`](mastering-java/shared/index.html); lesson content stays in Markdown.
- Chapter 2 and Chapter 3 visual diagrams are SVG files in `mastering-java/shared/assets/`.

The root page redirects directly to Chapter 1's named HTML page. Chapter 1, Chapter 2, and Chapter 3 have Previous/Next navigation; later chapter pages will be added in subsequent steps.
