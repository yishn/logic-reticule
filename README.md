# reticule

<img src="logo.png" width="100" height="100">

A new way to write and explore mathematical texts. This is a work in progress.

# Getting Started

## Installation

Make sure you have [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/) installed. To install reticule, run:

    npm install -g reticule

## Book Structure

To create a book, create a folder with the following text files:

    root
    ├ book.json
    └ toc.md

## Meta Information

`book.json` contains all meta-information regarding your book, such as the title and the author. `toc.md` contains the table of contents of your book. It defines all sections and links to the corresponding files.

`book.json` contains an JSON object with the following properties:

Property               | Description
-----------------------|----------------------------------------
`title` *(mandatory)*  | The book title. No markdown allowed.
`author` *(mandatory)* | The book author(s). Markdown allowed.
`accent`               | Defines an accent color in hex. Default: `#327CCB`
`lang`                 | Defines the book language. Affects CSS hyphenation. Default: `en`
`github`               | The link to a GitHub repository. If defined, every page has a 'GitHub' and an 'Edit page' link.
`disqus`               | The shortname of your Disqus website. Provides Disqus comment system integration if defined.
`localization`         | An object containing alternate strings. Translatable strings: `&para;`, `$\square$`, `Proof`, `Table of Contents`, `Index`, `GitHub`, `Edit page`, `Generated by reticule`

### Example

~~~json
{
    "title": "Étale Kohomologie",
    "author": "Yichuan Shen",
    "lang": "de",
    "localization": {
        "Proof": "Beweis",
        "Table of Contents": "Inhaltsverzeichnis",
        "Edit page": "Seite bearbeiten",
        "Generated by reticule": "Erstellt mit reticule",
        "$\\square$": "Q.E.D."
    }
}
~~~

## Book Sections

For each section create a folder with a `tags.md` file:

    root
    ├ section1
    │ └ tags.md
    ├ section2
    │ └ tags.md
    ├ section3
    │ └ tags.md
    │
    ├ book.json
    └ toc.md

Also, provide the book structure in `toc.md` as an unordered list:

~~~md
* [Section 1](section1/)
* [Section 2](section2/)
* Subsection
    * [Section 3](section3/)
~~~

Don't use the folder name `index` as it's reserved for the automatically generated index.

## Tags

Tags are the building blocks of a reticule. A tag consists of two parts: An assertion and an optional proof. To create a tag, choose a unique tag id, e.g. `0ABC` or `1ABC`, and append the following in a `tags.md` file:

~~~md
#0ABC

There are infinitely many primes.

#1ABC:Dirichlet's Theorem

Let `a, b` be coprime numbers. There are infinitely many primes
congruent `a` modulo `b`.
~~~

Only alphanumeric characters and the hyphen `-` are allowed in a tag id. You can name the tag by appending a colon and a name to the id. To provide a proof, add a horizontal line:

~~~md
#0ABC:Theorem

There are infinitely many primes.

---

Suppose there are only finite primes `p_1,\ldots,p_n`. Observe that
`p_1\cdot p_2\cdots p_n + 1` has a prime divisor `p`, distinct from
`p_1,\ldots,p_n`.
~~~

[Markdown](https://daringfireball.net/projects/markdown/) is used for formatting. Code spans and code blocks are converted into math environments and rendered by [MathJax](https://www.mathjax.org/) and [XyJax](http://sonoisa.github.io/xyjax/xyjax.html).

To link to other tags, use a markdown link and and the tag id as the source:

~~~md
#0ABC:Theorem

There are infinitely many primes.

---

Putting `a = 1` and `b = 2` in [~](#1ABC) yields infinitely many
odd primes.
~~~

## Creating Index

To add a keyword to the index, just append the keyword, wrapped in `~~`, anywhere in the tag:

~~~md
#1ABC:Dirichlet's Theorem

Let `a, b` be coprime numbers. There are infinitely many primes
congruent `a` modulo `b`. ~~Dirichlet's Theorem~~
~~~

You can add a context to a keyword by appending `|` and the context to the keyword:

~~~md
#1ABC:Dirichlet's Theorem

Let `a, b` be coprime numbers. There are infinitely many primes
congruent `a` modulo `b`. ~~Dirichlet's Theorem|Number Theory~~
~~~

## TeX Macros

You can define custom TeX macros that can be used throughout your book. Simply add a file named `macros.tex` with the user-defined macros to the root folder:

    root
    ├ book.json
    ├ toc.md
    └ macros.tex

## Compilation

To compile a reticule book into a website, navigate to your book directory and simply run:

    reticule
