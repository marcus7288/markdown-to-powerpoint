# Pandoc Compatibility Update

## Summary

The Markdown → PowerPoint converter now supports **Pandoc's standard syntax** for creating slides with two-column layouts, while maintaining backward compatibility with the original custom syntax.

## What Changed

### Two-Column Syntax

**NEW - Pandoc Standard (recommended):**
```markdown
::: columns

::: column
Left column content
:::

::: column
Right column content
:::

:::
```

**OLD - Legacy Format (still supported):**
```markdown
Left column content

|COL|

Right column content
```

### Why This Matters

1. **Portability**: Presentations written in Pandoc syntax can be converted using actual Pandoc CLI tools
2. **Standard Compliance**: Uses widely-adopted markdown extensions from Pandoc
3. **Interoperability**: Same markdown files can work with other Pandoc-based tools
4. **Backward Compatibility**: All existing presentations using `|COL|` continue to work

## Technical Implementation

### Parser Updates

The `isTwoCol()` and `splitCols()` functions now:
- Detect both `::: columns` (Pandoc) and `|COL|` (legacy) markers
- Parse Pandoc's nested `::: column` blocks
- Extract content from each column appropriately
- Fall back gracefully if syntax is malformed

### Code Changes

```javascript
// Before
function isTwoCol(chunk) { 
  return /^\|COL\|$/m.test(chunk); 
}

// After  
function isTwoCol(chunk) { 
  return /^:::\s*columns\s*$/m.test(chunk) || /^\|COL\|$/m.test(chunk);
}
```

The `splitCols()` function now includes Pandoc parsing logic that:
1. Detects `::: columns` wrapper
2. Splits on individual `::: column` markers
3. Extracts and trims content from each column
4. Falls back to legacy `|COL|` splitting if needed

## Files Included

1. **pandoc-to-pptx.html** - Updated converter with Pandoc support
2. **README.md** - Updated documentation with syntax examples
3. **pandoc-sample.md** - Sample presentation demonstrating both syntaxes

## Testing

The converter has been tested with:
- Pure Pandoc syntax (`::: columns`)
- Pure legacy syntax (`|COL|`)
- Mixed presentations using both syntaxes
- Edge cases (malformed syntax, empty columns)

## Migration Guide

### For New Presentations
Use Pandoc syntax for maximum compatibility:

```markdown
# My Presentation

---

## Two Column Slide

::: columns

::: column
Content here
:::

::: column
More content
:::

:::
```

### For Existing Presentations
No changes needed! Your existing `|COL|` markers continue to work exactly as before.

### Converting Legacy to Pandoc
Simple find-and-replace pattern:

1. Find each section that looks like:
   ```
   Content A
   
   |COL|
   
   Content B
   ```

2. Replace with:
   ```
   ::: columns
   
   ::: column
   Content A
   :::
   
   ::: column
   Content B
   :::
   
   :::
   ```

## Additional Notes

- The `---` slide separator was already Pandoc-standard
- Level 1 headers (`#`) create title slides (existing behavior)
- Level 2 headers (`##`) create content slide titles (existing behavior)
- All other markdown features (bullets, code, tables, images) unchanged

## References

- [Pandoc Manual - Slide Shows](https://pandoc.org/MANUAL.html#slide-shows)
- [Pandoc Manual - Fenced Divs](https://pandoc.org/MANUAL.html#divs-and-spans)
- [PptxGenJS Documentation](https://gitbrent.github.io/PptxGenJS/)
