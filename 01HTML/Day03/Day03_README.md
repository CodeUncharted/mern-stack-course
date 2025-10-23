# HTML Day 03

## Table of Contents
- [File Path System](#file-path-system)
- [HTML Boilerplate Code](#html-boilerplate-code)
- [Multipage Website](#multipage-website)
- [Semantic HTML Elements](#semantic-html-elements)

---

## File Path System

### The Fundamental Truth

A website is not one single file. It's a collection of different files (HTML, CSS, JavaScript, images, videos, fonts) that all need to work together. These files are organized into folders, just like documents on your computer.

### The Core Problem

If your `index.html` file needs to display an image named `logo.png`, how does the HTML file tell the browser where to find `logo.png`?

You can't just say `src="logo.png"` and expect it to work every time. The browser needs an exact, unambiguous address to locate the file. A **file path** is that address.

---

### A) Relative File Paths

A relative file path gives directions to a file **starting from the location of the file you are currently in**. You will use this 99% of the time for linking your own files together.

**Example Folder Structure:**

```
my-website/
├── index.html
├── about.html
├── images/
│   ├── logo.png
│   └── hero.jpg
└── pages/
    ├── contact.html
    └── terms.html
```

#### Scenario 1: Linking to a file in the SAME folder

You are in `index.html` and want to link to `about.html`. They are neighbors in the same folder.

```html
<!-- This code is inside index.html -->
<a href="about.html">About Us</a>
```

#### Scenario 2: Linking to a file in a SUB-FOLDER (Going Down)

You are in `index.html` and want to display `logo.png`. You need to go **into** the images folder.

```html
<!-- This code is inside index.html -->
<img src="images/logo.png" alt="My Website Logo">
```

#### Scenario 3: Linking to a file in a PARENT FOLDER (Going Up)

You are in `contact.html` (inside `pages/`) and want to display `logo.png` (inside `images/`). You must first go **up** one level to `my-website/`, then **down** into `images/`.

```html
<!-- This code is inside pages/contact.html -->
<img src="../images/logo.png" alt="My Website Logo">
```

- `../` takes you from `pages/` up to `my-website/`
- `images/logo.png` then takes you down into the images folder

---

### B) Absolute File Paths

An absolute file path gives the **full, complete URL** to a resource on the web. It starts with `http://` or `https://`.

**When to use it:**
You ONLY use absolute paths when linking to a resource that is **NOT on your own website**.

- Linking to another website
- Using a font from Google Fonts
- Using an image from an image-hosting service

**Example:**

```html
<!-- Linking to an external website -->
<a href="https://www.google.com">Search on Google</a>

<!-- Using an image hosted on another server -->
<img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/Html5_logo_and_wordmark.svg" alt="HTML5 Logo">
```

### Why NOT use absolute paths for your own files?

A beginner might be tempted to copy the full path from their computer:

```html
src="C:/Users/Arjun/Desktop/my-website/images/logo.png"
```

**This is a major mistake.** This address only works on YOUR computer. When you upload your website to a server, that path becomes meaningless and the image will be broken.

### Security: The Browser Sandbox

A web browser is a **secure prison** (sandbox) for the code it runs. Code running inside the sandbox is NOT allowed to freely access the host computer's file system.

If this security rule didn't exist, a malicious website could potentially read your private files, photos, documents—anything on your computer.

Relative paths will always work because they describe the location of files **relative to each other**, no matter what computer or server they are on.

---

### Summary / Rules of Thumb

1. **For Your Own Files (Internal Links):** ALWAYS use Relative Paths
   - `filename.html` (Same folder)
   - `folder/filename.html` (Go down)
   - `../filename.html` (Go up)

2. **For Other Websites' Files (External Links):** ALWAYS use Absolute Paths
   - `https://www.example.com/page.html`

---

### Absolute Paths: Windows vs macOS/Linux

#### Windows

- **Starting Point:** Drive letter followed by colon and backslash (e.g., `C:\`)
- **Directory Separator:** Backslash `\`
- **Structure:** `Drive:\Folder\SubFolder\file.txt`

**Example:**
```
C:\Users\JohnDoe\Documents\report.docx
```

#### macOS / Linux

- **Starting Point:** Single forward slash `/` (represents the root)
- **Directory Separator:** Forward slash `/`
- **Structure:** `/Folder/SubFolder/file.txt`

**Example:**
```
/Users/johndoe/Documents/report.docx
```

#### Comparison Table

| Feature | Windows | macOS / Linux |
|---------|---------|---------------|
| Starting Point | Drive Letter (C:\) | Single forward slash (/) |
| Directory Separator | Backslash (\\) | Forward Slash (/) |
| Example | C:\Users\JohnDoe\Documents\report.docx | /Users/johndoe/Documents/report.docx |

---

## HTML Boilerplate Code

### The Fundamental Truth

A web browser needs **specific, predictable instructions** to do its job. It cannot guess your intentions.

### The Core Problem

We need to give the browser essential "setup information" **before** it starts rendering our visible content. This setup needs to answer:

- "What version of HTML am I reading?"
- "What character encoding should I use?"
- "What should the title of the browser tab be?"
- "How should this page behave on mobile vs desktop?"

### The Solution: The Boilerplate

A **boilerplate** is a standard, universal starting template. It's the blueprint you need before you start building.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

---

### Breaking Down Each Line

#### 1. `<!DOCTYPE html>`

**The Problem:** Browsers need to know which set of HTML rules to use.

**The Solution:** This Document Type Declaration tells the browser to use the latest, standard-compliant mode (HTML5). It prevents "quirks mode" (an old mode for non-standard pages).

**Must always be the first thing in your file.**

---

#### 2. `<html lang="en">...</html>`

**The Problem:** How do search engines and screen readers know what language the content is in?

**The Solution:** The `lang="en"` attribute declares English as the primary language. This is crucial for accessibility and SEO.

- Change to `"es"` for Spanish
- Change to `"hi"` for Hindi
- etc.

---

#### 3. `<head>...</head>`

**The Problem:** We need a place for "behind-the-scenes" information.

**The Solution:** The `<head>` section contains metadata. Nothing inside `<head>` is displayed in the browser window.

---

#### 4. `<meta charset="UTF-8">`

**The Problem:** Computers need a character set to map numbers to letters. Wrong encoding = garbled text.

**The Solution:** UTF-8 is the universal standard that can represent almost any character from any language in the world.

**Essential to prevent text-encoding issues.**

---

#### 5. `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

**The Problem:** Websites can be viewed on tiny phone screens or giant monitors. Without this, mobile browsers render pages as if on desktop—resulting in tiny, unreadable pages.

**The Solution:** This is the cornerstone of **responsive design**.

- `width=device-width`: Makes page width equal to screen width
- `initial-scale=1.0`: Sets initial zoom to 100%

**Tells the browser to optimize for mobile screens.**

---

#### 6. `<title>...</title>`

**The Problem:** How do users identify your page among 20 tabs?

**The Solution:** Sets the text in the browser tab, bookmarks, and search results. Critical for usability and SEO.

---

#### 7. `<body>...</body>`

**The Problem:** Where do we put visible content?

**The Solution:** Contains everything users see: headings, paragraphs, images, links, etc.

---

### Why Websites Work Without Boilerplate

Browsers are **extremely forgiving**. When you omit the boilerplate:

1. **No `<!DOCTYPE html>`?** → Browser enters "Quirks Mode" (unpredictable rendering)
2. **No `<html>` or `<body>` tags?** → Browser implicitly generates them
3. **No `<meta charset="UTF-8">`?** → Browser guesses encoding (can break special characters)
4. **No `<title>`?** → Browser uses filename as title

### Why Use Boilerplate Anyway?

For simple pages, it looks the same. But for professional, reliable websites:

1. **Unpredictable Rendering:** CSS works differently across browsers in quirks mode
2. **Broken Characters:** Special characters (€, —, ') can break without UTF-8
3. **Bad Mobile Experience:** Sites are unusable on phones without viewport meta tag
4. **Poor SEO and Accessibility:** Search engines and screen readers rely on boilerplate tags

**The boilerplate is the proper engineering foundation for your website.**

---

## Multipage Website

### The Fundamental Truth

Complex information is naturally broken into distinct topics. A book has chapters, a store has departments, a website has pages.

### The Core Problem

How do we create distinct pages AND allow users to navigate between them seamlessly?

### The Solution

1. **Consistent Structure:** All pages share common header and footer
2. **Linking System:** Navigation menu with `<a>` tags on every page

---

## Semantic HTML Elements

### 1. The `<div>` (The Generic Box)

**The Problem:** How do we group elements together as a single unit?

**The Solution:** A generic, meaningless container for grouping.

```html
<div>
    <img src="avatar.png">
    <h2>Arjun Kumar</h2>
    <p>Loves to code and teach HTML.</p>
</div>
```

Now you can style or control them as one unit with CSS.

---

### 2. `class` and `id` (Labels for Boxes)

**The Problem:** How do we identify and target specific boxes?

**The Solution:** Two types of labels (attributes):

#### `id` - Unique Identifier

- For ONE specific element on the entire page
- Must be unique
- Perfect for major sections (navigation, search form)
- Like a Social Security Number or Aadhaar Number

#### `class` - Reusable Classifier

- Can be applied to MULTIPLE elements
- Groups elements with similar style/function
- Like a Job Title (many people can be "Engineer")

**Example:**

```html
<!-- One unique main header -->
<div id="main-header">...</div>

<!-- Multiple profile cards with same class -->
<div class="profile-card">...</div>
<div class="profile-card">...</div>

<!-- One special card with both id and class -->
<div id="featured-profile" class="profile-card">...</div>
```

**CSS Targeting:**

```css
#main-header { ... }        /* Targets the ONE unique element */
.profile-card { ... }        /* Targets ALL THREE cards */
#featured-profile { ... }    /* Targets only the special card */
```

---

### 3. The `<span>` (Inline Highlighter)

**The Problem:** How do we style a piece of content WITHIN a line of text without breaking the line?

**The Solution:** An inline container that doesn't create line breaks.

```html
<p>This is very <span class="highlight">important</span> information.</p>
```

**Analogy:** Like using a highlighter pen in a book—you mark a few words without ripping out the page.

---

### 4. Semantic Layout Elements

These are special `<div>`s with built-in meaning:

#### `<header>`
Box for introductory content at the top. Contains logo, navigation, main heading.

#### `<footer>`
Box for closing content at the bottom. Contains copyright, contact info, secondary links.

#### `<main>`
Defines the **main, unique content** of that specific page. Should NOT contain repeated elements (header/footer). **Only ONE `<main>` per page.**

---

## Summary

1. Use **relative paths** for your own files, **absolute paths** for external resources
2. Always start HTML files with the **boilerplate**
3. Use `<div>` to group elements, `class` for multiple elements, `id` for unique elements
4. Use `<span>` for inline styling
5. Use semantic elements (`<header>`, `<footer>`, `<main>`) for better structure

---

**Happy Coding! 🚀**