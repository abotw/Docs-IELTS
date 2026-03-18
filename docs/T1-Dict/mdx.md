---
title: MDX
status: done
---

As a dictionary enthusiast, understanding **MDX** is extremely important if you use electronic dictionaries like **MDict** or build your own **digital dictionary library**.

This tutorial will introduce the **MDX dictionary format** from beginner to advanced level: history, structure, technical details, tools, and practical usage.

# 1. What Is MDX?

**MDX** is a proprietary dictionary file format used by the software **MDict**.

-   Full name: *MDict Dictionary Data File*
-   Extension: `.mdx`
-   Purpose: Store dictionary entries (words + definitions)
-   Companion file: `.mdd` (resource file)

In short:

| File   | Purpose                                       |
| ------ | --------------------------------------------- |
| `.mdx` | Text content (entries, definitions, HTML)     |
| `.mdd` | Multimedia resources (images, audio, CSS, JS) |

# 2. A Brief History of MDX

MDict was developed in China in the early 2000s and became extremely popular among advanced dictionary users because:

-   It supports HTML-based entries.
-   It allows custom CSS styling.
-   It supports JavaScript.
-   It can integrate audio pronunciation and images.

Over time, the MDX format became the *de facto* standard for high-quality third-party electronic dictionaries.

Today, MDX dictionaries are supported by:

-   MDict
-   GoldenDict
-   Eudic (欧路词典)
-   Various Android and iOS dictionary apps

# 3. Internal Structure of an MDX File

Although MDX is a binary format, conceptually it contains:

### 3.1 Header Section

Contains metadata such as:

-   Dictionary title
-   Description
-   Encoding (UTF-8, UTF-16)
-   Engine version
-   Creation tool

### 3.2 Keyword Index Section

This is the searchable word list.

Each entry contains:

-   Headword
-   Offset pointer
-   Length of entry content

Think of it as:

```
word → pointer → definition block
```

This design allows:

-   Fast lookup
-   Efficient random access
-   Good performance even with large dictionaries

### 3.3 Record Block Section

This contains the actual dictionary entries.

Entries are typically written in:

-   HTML
-   XHTML
-   CSS styling
-   Sometimes JavaScript

Example (conceptual):

```html
<div class="entry">
  <h1>example</h1>
  <p>noun</p>
  <p>a thing characteristic of its kind</p>
</div>
```

### 3.4 Compression

MDX files use compression for efficiency:

-   zlib compression
-   Record block compression
-   Key block compression

This keeps file sizes manageable even for large dictionaries like Oxford or Longman.

# 4. What Is MDD?

The `.mdd` file is the **resource file**.

It stores:

-   Images (PNG, JPG)
-   Audio (MP3)
-   CSS files
-   Fonts
-   JavaScript files

Example:

If a dictionary entry contains:

```html
<img src="images/apple.png">
<audio src="audio/apple.mp3">
```

Those files are stored inside `.mdd`.

Without the `.mdd`, the dictionary will still work — but images/audio will not load.

# 5. MDX Entry Writing Format (Source Level)

Before compiling into `.mdx`, dictionary content is usually written in **source text format**.

Typical source structure:

```
apple
<html>
definition content
</html>
</>

banana
<html>
definition content
</html>
</>
```

Rules:

-   Headword line
-   Definition block
-   End marker (`</>`)

This source file is then compiled into `.mdx`.

# 6. How MDX Is Created

To create MDX files, developers use:

-   **MDict Builder**
-   Command-line tools
-   Open-source tools like mdict-utils

General workflow:

```
Text source → Compiler → .mdx
Resources → Compiler → .mdd
```

Advanced creators:

-   Use CSS for beautiful layouts
-   Use JS for foldable definitions
-   Optimize fonts for mobile reading

# 7. Advantages of MDX Format

### 7.1 HTML-Based

Unlike many traditional dictionary formats, MDX supports full HTML rendering:

-   Tables
-   Colors
-   Fonts
-   Layout control
-   Clickable links

### 7.2 Highly Customizable

You can:

-   Modify CSS
-   Improve typography
-   Optimize layout for macOS/iPad (which you might appreciate if you like clean macOS-style design)

### 7.3 Efficient Indexing

The block index design makes:

-   Lookup extremely fast
-   Large dictionaries usable on mobile devices

# 8. Limitations of MDX

Despite its popularity, MDX has some limitations:

1.  Proprietary format
2.  Official documentation is limited
3.  Editing requires compilation
4.  Not fully open standard

Reverse engineering projects exist, but the format is not officially open.

# 9. MDX vs Other Dictionary Formats

| Format      | Open | HTML    | Multimedia | Popularity |
| ----------- | ---- | ------- | ---------- | ---------- |
| MDX         | ❌    | ✅       | ✅          | Very High  |
| StarDict    | ✅    | Limited | Limited    | Medium     |
| DSL (ABBYY) | Semi | Limited | Limited    | Medium     |

# 10. How Power Users Use MDX

Advanced users often:

-   Build custom English–Chinese dictionaries
-   Combine multiple dictionaries
-   Create pronunciation packs
-   Extract word lists for Anki
-   Customize CSS for better readability

Especially for IELTS preparation, many learners use MDX versions of:

-   Oxford
-   Longman
-   Collins

to improve vocabulary precision.

# 11. Technical Deep Dive (For Advanced Users)

Internally, MDX:

-   Uses big-endian integers
-   Uses block-based index
-   Applies compression to key blocks and record blocks separately
-   Stores offsets as 64-bit integers (newer versions)

Reverse-engineered specs are available in open-source projects.

If you're a CS student, you can treat MDX as:

>   A compressed indexed key–value database specialized for dictionary lookup.

# 12. Should You Learn MDX?

If you:

-   Love dictionaries
-   Care about typography
-   Want custom vocabulary systems
-   Prepare for IELTS seriously
-   Like technical tinkering

Then understanding MDX is extremely valuable.

# 13. Summary

MDX is:

-   A high-performance dictionary format
-   HTML-based
-   Resource-extensible (.mdd)
-   Widely supported
-   Powerful but semi-closed

It combines:

-   Database indexing
-   Compression techniques
-   Web technologies
-   Linguistic data organization

