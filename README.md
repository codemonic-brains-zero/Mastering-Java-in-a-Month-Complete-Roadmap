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
    |   +-- index.html (folder redirect)
    |   +-- chapter-01-introduction-to-java.html
    |   +-- chapter-01-introduction-to-java.md
    +-- chapter-02-variables-data-types-and-operators/
    |   +-- chapter-02-variables-data-types-and-operators.html
    |   +-- chapter-02-variables-data-types-and-operators.md
    +-- shared/
        +-- index.html
        +-- assets/
            +-- java-primitive-types.svg
            +-- operator-evaluation.svg
            +-- primitive-conversion.svg
            +-- variable-ownership.svg
```

- [`roadmap/java-learning-roadmap.md`](roadmap/java-learning-roadmap.md) contains the complete Java syllabus.
- [`mastering-java/chapter-01-introduction-to-java/chapter-01-introduction-to-java.md`](mastering-java/chapter-01-introduction-to-java/chapter-01-introduction-to-java.md) contains the Chapter 1 lesson notes.
- [`mastering-java/chapter-02-variables-data-types-and-operators/chapter-02-variables-data-types-and-operators.md`](mastering-java/chapter-02-variables-data-types-and-operators/chapter-02-variables-data-types-and-operators.md) contains Chapter 2 lesson explanations, Java examples, takeaways, and its coverage check against the master roadmap.
- Each named chapter HTML page opens the shared UI in [`mastering-java/shared/index.html`](mastering-java/shared/index.html); lesson content stays in Markdown. Chapter 1 also keeps a small `index.html` redirect so the root page can continue to open the first chapter.
- Chapter 2's visual diagrams are SVG files in `mastering-java/shared/assets/`.

The root page redirects to Chapter 1. The prototype includes Chapter 1 and Chapter 2 pages with Previous/Next navigation; later chapter pages will be added in subsequent steps.
