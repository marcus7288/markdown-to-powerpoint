# Welcome to Pandoc-Compatible Slides

## A Modern Presentation Tool

---

## Single Column Slide

This is a regular slide with a single column of content.

- First bullet point
- Second bullet point
- Third bullet point

You can include **bold** and *italic* text, as well as `inline code`.

---

## Two-Column Slide (Pandoc Standard)

::: columns

::: column
### Left Column

- Point one
- Point two
- Point three

This uses Pandoc's standard `::: columns` syntax.
:::

::: column
### Right Column

- Another point
- More details
- Final thought

The parser handles both Pandoc and legacy formats!
:::

:::

---

## Two-Column with Code (Legacy Format)

### Configuration Example

```python
def hello_world():
    print("Hello, World!")
    return True
```

|COL|

### Output

```
Hello, World!
```

This slide uses the legacy `|COL|` separator, which still works for backward compatibility.

---

## Features List

### What This Tool Supports

1. **Pandoc-compatible syntax** for maximum portability
2. **Legacy syntax** for existing presentations
3. **Multiple themes** with professional styling
4. **Code blocks** with syntax awareness
5. **Images and tables** for rich content
6. **16:9 and 4:3** aspect ratios

---

## Code Example

Here's a more complex code block:

```javascript
function createPresentation(markdown) {
  const slides = splitSlides(markdown);
  const pres = new PptxGenJS();
  
  slides.forEach(slide => {
    pres.addSlide(slide);
  });
  
  return pres;
}
```

---

## Tables Work Too

| Feature | Pandoc | Legacy | Status |
|---------|--------|--------|--------|
| Slide breaks | ✓ | ✓ | Supported |
| Two columns | ✓ | ✓ | Supported |
| Code blocks | ✓ | ✓ | Supported |
| Tables | ✓ | ✓ | Supported |

---

## Blockquotes

> "The best presentations are simple, clear, and focused."
> 
> — Design Principle

Use blockquotes for emphasis or citations.

---

## Mixed Content Example

::: columns

::: column
### Text Content

You can mix different content types in columns:

- Bullets
- **Bold text**
- *Italic text*
- `Code snippets`

> And even blockquotes!
:::

::: column
### Numbered Lists

1. First item
2. Second item
3. Third item
4. Fourth item

Each column can have its own formatting and structure.
:::

:::

---

# Thank You!

## Questions?

Visit the GitHub repository for documentation and examples.
