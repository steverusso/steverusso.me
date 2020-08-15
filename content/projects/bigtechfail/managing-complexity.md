---
weight: 4
title: Managing Complexity Between HTML & CSS
draft: true
---

I made the decision early on for BigTech.fail that I [would not be using JavaScript](../early-architecture-decisions/) at all.
That essentially leaves HTML and CSS as "places" where complexity can be managed or mismanaged.

Before going further, it's important to note that for this article, as well as the actual project itself, there are no concerns whatsoever regarding CSS performance.

## Shifting the Balance

- made the decision to shift complexity towards CSS and away from HTML; this is based on:
  - it's easier to read 8 lines of CSS styling than 8 utility classes
  - the page layouts and partials (HTML) is where new contributors would (likely?) go first in order to get an idea of the project
  - the CSS is probably where they'd go next
  - CSS has tools like SCSS/SASS if things get crazy

## Minimizing the Use of Utility Classes

Utility classes are short CSS classes that apply one or two styling rules to an element, and it is typically easy to deduce which rules they apply from their short name.
For example, `d-flex` would be a utility class for applying the `display: flex !important;` rule.

```html
<div class="pos-relative d-flex align-center px-8"> . . . </div>
```
```css
.pos-relative { position: relative !important }
.d-flex { display: flex !important }
.align-center { align-items: center !important }
.px-8 { padding-left: 2rem !important; padding-right: 2rem !important }
```

```html
<div class="mydiv"> . . . </div>
```
```css
.mydiv {
  position: relative;
  display: flex;
  align-items: center;
  padding: 0 2rem;
}
```

## Pick a Tag to Mean _One_ Thing

- The "site" has a consistent user interface (consistent because each page has it) that can be broken down into components: navbar, footer
- Pick a tag to be one of those components, that's it. It isn't used in any other capacity anywhere else.

Consider the following code snippets for use as the top level elements in the site's top navigation bar:

```html
<div class="navbar"> ... </div>
<!-- vs -->
<nav> ... </nav>
```

The second code snippet is clearly simpler.
The element doesn't have any attributes, which results in less text.
That's less to keep track of when refactoring, less that new contributors have to read and process, etc.
Obviously less text shouldn't be the primary goal.
Less text can result in ambiguity.
However, in this situation, we have less text that's _even clearer_ because the tag name itself describes the purpose of the element.

- Closing tags easier to track when deeply nested instead of 50 divs.
- Offload complexity to CSS, keep the HTML simple
  - HTML is what a new contributor will go to first, and should easily give an accurate overview to someone looking for it.
  - Duplicate CSS is not complicated, but loading an HTML element up with 7 utility classes just to avoid duplicate CSS is.

Things I miss:
- obvi the timeline, although some exciting things in the works
- esc key to close drawers and dialogs
