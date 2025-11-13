# Working with Typst: A Guide for Manus Agents

**Author:** Manus AI
**Date:** 2025-11-13

## 1. Introduction to Typst

Typst is a modern, markup-based typesetting system designed to be a powerful alternative to LaTeX while offering a much simpler and more intuitive user experience [1]. It excels in producing scientific and technical documents, combining the ease of lightweight markup languages like Markdown with a sophisticated scripting language for complex layouts and automation. Its key features include a clean syntax, rapid compilation speeds, and a consistent, function-based approach to commands, making it an increasingly popular choice for academic papers, reports, and presentations.

This document serves as a comprehensive guide for Manus agents on how to effectively work with Typst, from installation and basic syntax to advanced features like package management and navigating its ecosystem.

## 2. Installing the Typst Compiler

While Typst offers a web app for online editing, installing the command-line interface (CLI) compiler is essential for local development and integration with other tools. The following steps detail how to install the Typst compiler within the Manus sandbox environment.

First, you must ensure that the `xz-utils` package is installed to handle the compressed archive. Then, you can download the latest pre-compiled binary from the official Typst GitHub releases, extract it, and move the executable to a directory within the system's `PATH`.

The entire process can be executed with a single shell command:

```bash
sudo apt-get update -qq && sudo apt-get install -y xz-utils && \
wget -qO- https://github.com/typst/typst/releases/latest/download/typst-x86_64-unknown-linux-musl.tar.xz | tar -xJ && \
sudo mv typst-x86_64-unknown-linux-musl/typst /usr/local/bin/
```

After running this command, you can verify the installation by checking the version:

```bash
typst --version
```

This command should return the installed Typst version, confirming that the compiler is ready to use.

## 3. Typst Syntax Fundamentals

Typst's syntax is designed for readability and ease of use. It operates in three distinct modes: **Markup**, **Math**, and **Code**.

*   **Markup Mode:** This is the default mode for writing text and applying basic formatting. It uses simple, intuitive syntax similar to Markdown.
*   **Math Mode:** Enclosed in dollar signs (`$`), this mode is for typesetting mathematical formulas.
*   **Code Mode:** Prefixed with a hash symbol (`#`), this mode unlocks Typst's powerful scripting capabilities, allowing for variables, functions, and programmatic control.

### Common Markup and Formatting

The following table summarizes some of the most common syntax elements used in Typst's markup mode.

| Element | Syntax | Description |
| :--- | :--- | :--- |
| **Emphasis** | `*strong*` or `_emphasis_` | For bold and italic text. |
| **Headings** | `= Level 1`, `== Level 2` | Headings are created with one or more equals signs. |
| **Lists** | `- Bullet`, `+ Numbered` | Simple syntax for creating bulleted and numbered lists. |
| **Links** | `https://typst.app` | URLs are automatically converted into clickable links. |
| **Labels & References** | `<label-name>` and `@label-name` | Create a label and reference it elsewhere in the document. |
| **Raw Text** | `` `verbatim` `` | Renders content without applying any formatting. |
| **Comments** | `// Line` or `/* Block */` | For adding notes that won't appear in the output. |

## 4. Navigating the Typst Documentation

The official Typst documentation is an excellent and comprehensive resource [1]. It is well-structured and divided into several key sections to help users find information quickly.

*   **[Tutorial](https://typst.app/docs/tutorial/):** A step-by-step, beginner-friendly guide that walks through the process of creating a document from scratch. This is the best starting point for new users.
*   **[Reference](https://typst.app/docs/reference/):** A detailed reference that covers every aspect of Typst, including all syntax, concepts, functions, and types. When you need to know how a specific function works, this is the place to look.
*   **[Guides](https://typst.app/docs/guides/):** This section contains practical guides for specific use cases, such as the invaluable **[Guide for LaTeX Users](https://typst.app/docs/guides/for-latex-users/)**, which helps users transition from LaTeX to Typst [2].

Effectively using the documentation involves starting with the Tutorial to grasp the basics, and then using the Reference and Guides for more specific questions and advanced topics. The search functionality within the documentation is also highly effective.

## 5. Key Differences from LaTeX

For those familiar with LaTeX, understanding the key differences in philosophy and syntax can accelerate the learning process. Typst is designed to be more consistent and less verbose.

### Math Notation

While the core concepts are similar, math notation has some important distinctions.

> In Typst, delimiters will scale automatically for their expressions, just as if `\left` and `\right` commands were implicitly inserted in LaTeX. You can customize delimiter behaviour using the `lr` function. To prevent a pair of delimiters from scaling, you can escape them with backslashes. [2]

| Feature | Typst | LaTeX |
| :--- | :--- | :--- |
| **Display Math** | `$ x = y $` (with spaces) | `$$...$$` or `\[...\]` or `equation` environment |
| **Fractions** | `(a+b)/c` | `\frac{a+b}{c}` |
| **Delimiters** | `(`, `[`, `{` auto-scale | `\left(`, `\right)` for scaling |
| **Functions** | `sqrt(x)`, `log(x)` | `\sqrt{x}`, `\log(x)` |
| **Text in Math** | `"if"` | `\text{if}` |
| **Symbol Variants** | `arrow.r.long` (dot notation) | Different command names (e.g., `\rightarrow`, `\longrightarrow`) |

### Commands and Packages

In LaTeX, functionality is added through packages with commands that often have inconsistent syntax. In Typst, functionality is exposed through **functions** that are called with a consistent syntax (`#function(arguments)`). Packages are managed through a central repository, the **Typst Universe**, and are imported on-demand without manual installation.

## 6. The Typst Universe: Packages and Templates

The **[Typst Universe](https://typst.app/universe/)** is the official online repository for community-created packages and templates [3]. It allows you to easily extend Typst's core functionality.

### Finding and Using Packages

You can browse the Universe by category or use the search bar to find packages for specific needs, such as drawing diagrams (`cetz`), creating presentations (`touying`), or formatting bibliographies.

To use a package, you import it directly into your document using the `#import` rule. Typst's package manager will automatically download it on first use and cache it for offline access. The import syntax specifies the namespace (`@preview` for community packages), the package name, and the version.

For example, to import the `cetz` package for drawing and use its `canvas` function, you would write:

```typst
#import "@preview/cetz:0.3.4": canvas

#canvas({
  // Drawing instructions go here
})
```

You can also import specific functions or import all of a package's exports using `*`.

```typst
// Import specific functions
#import "@preview/cetz:0.3.4": canvas, draw

// Import all functions
#import "@preview/cetz:0.3.4": *
```

This streamlined approach to package management is a significant advantage over traditional LaTeX workflows.

---

## References

[1] Typst Documentation. (n.d.). Retrieved from https://typst.app/docs/

[2] Guide for LaTeX Users. (n.d.). Typst Documentation. Retrieved from https://typst.app/docs/guides/for-latex-users/

[3] Typst Universe. (n.d.). Retrieved from https://typst.app/universe/
