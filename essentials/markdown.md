---
title: Markdown Syntax Guide
theme: dark
icon: hash
---

# Markdown Syntax Guide

Learn how to write beautiful documentation using Markdown in DevScribe.

## Basic Formatting

### Text Formatting

- **Bold text** using `**bold text**`
- *Italic text* using `*italic text*`
- `Inline code` using backticks
- ~~Strikethrough~~ using `~~strikethrough~~`

### Headers

```markdown
# H1 Header
## H2 Header  
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header
```

## Lists

### Unordered Lists

```markdown
- Item 1
- Item 2
  - Nested item
  - Another nested item
- Item 3
```

### Ordered Lists

```markdown
1. First item
2. Second item
3. Third item
```

## Links and Images

### Links
```markdown
[Link text](https://example.com)
[Link with title](https://example.com "Link title")
```

### Images
```markdown
![Alt text](image.jpg)
![Alt text](image.jpg "Image title")
```

## Code Blocks

### Inline Code
Use single backticks for `inline code`.

### Code Blocks
Use triple backticks with language specification:

````markdown
```javascript
function hello() {
  console.log("Hello, world!");
}
```
````

## DevScribe Components

DevScribe supports special components:

### Callouts

```markdown
{% callout title="Note" %}
This is a callout with custom content.
{% /callout %}
```

{% callout title="Example" %}
This is how a callout looks when rendered.
{% /callout %}

### Cards

```markdown
{% card description="Card description" %}
Card content goes here
{% /card %}
```

## Tables

```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Row 1    | Data     | More data|
| Row 2    | Data     | More data|
```

## Blockquotes

```markdown
> This is a blockquote
> It can span multiple lines
```

> This is how a blockquote appears when rendered. 