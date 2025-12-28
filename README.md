# Zotero Literature Note Template for Obsidian

An academic template for importing Zotero sources into Obsidian with full CSS control for web publishing via Quartz.

## Features

- **CSS-ready structure**: All elements wrapped in semantic classes for styling
- **Academic formatting**: `§ I`, `§ II` for highlights; `Abb. 1`, `Abb. 2` for figures
- **Obsidian-editable**: Clean rendering in Obsidian while maintaining full CSS control online
- **Multi-format support**: Books, articles, blog posts, etc.
- **Markdown callouts**: Uses Obsidian callouts for source citations and abstracts
- **Image handling**: Automatic Wikilink format for Quartz compatibility

## Template Structure

### Frontmatter
- `cssclasses: literature-note` - Enables targeted CSS styling
- `shortTitle` - Clean navigation labels (e.g., "Ahrens (2017)")
- Auto-generated metadata from Zotero (authors, year, citekey, etc.)

### Content Sections
1. **Title** (H2) with optional book cover
2. **Source citation** (Callout: `> [!book] Quelle`)
3. **Abstract** (Callout: `> [!abstract] Kurzfassung`)
4. **Annotations**:
   - Text highlights with Zotero colors (yellow, orange, red, green, blue, purple, magenta, gray)
   - Page references `(S. 42)`
   - Comments `Anm.: ...`
   - Images/screenshots with automatic figure captions

### CSS Classes

All annotation elements are wrapped in semantic divs for complete CSS control:

```html
<div class="annotation-highlight">
  <span class="section-marker"></span>
  <mark class="hltr-yellow">"Highlighted text"</mark>
  <span class="annotation-page">(S. 42)</span>
</div>

<div class="annotation-comment">
  <span class="comment-label">Anm.:</span> Your comment
</div>

![[image.png]]
<div class="annotation-figure-caption">
  <span class="figure-label"></span>
  <span class="figure-source">Seite 42</span>
</div>
```

## CSS Counter Examples

Use CSS counters for automatic numbering:

```scss
article.literature-note {
  counter-reset: section figure;

  .annotation-highlight {
    counter-increment: section;
    .section-marker::before {
      content: "§ " counter(section, upper-roman); // § I, § II, § III
    }
  }

  .annotation-figure-caption {
    counter-increment: figure;
    .figure-label::before {
      content: "Abb. " counter(figure); // Abb. 1, Abb. 2, Abb. 3
    }
  }
}
```

## Installation

### For Obsidian Zotero Integration Plugin

1. Install [Obsidian Zotero Integration](https://github.com/mgmeyers/obsidian-zotero-integration)
2. In Obsidian Settings → Zotero Integration → Import Formats
3. Create new format or edit existing
4. Copy content from `Zotero-Vorlage.md` into the template field
5. Save and use when importing from Zotero

### Template Language

This template uses **Nunjucks** (JavaScript templating), not Jinja2. Key differences:
- `namespace` is not supported → use separate counters
- Variables in loops are locally scoped
- Use `{%- -%}` for whitespace control carefully (can break Markdown parsing)

## Design Philosophy

- **Obsidian-first**: Template must render cleanly in Obsidian for editing
- **CSS-control-second**: All elements wrapped for complete online styling
- **No wrapper divs around images**: Obsidian doesn't render images inside custom divs
- **Minimal nesting**: Flat structure for better Markdown compatibility

## Best Practices

1. **Callouts**: Keep using Markdown callouts (`> [!book]`) - they work in both Obsidian and Quartz
2. **Images**: Use Wikilinks without path prefixes (`![[filename.png]]`)
3. **Blank lines**: Always leave blank lines between HTML divs and Markdown (especially before callouts)
4. **Whitespace control**: Avoid `{%- -%}` on `{% if %}` blocks that wrap large HTML structures

## Compatibility

- **Obsidian**: ✅ Clean rendering, full editability
- **Quartz v4**: ✅ Full CSS control via `cssclasses: literature-note`
- **Citations Plugin**: ✅ Works with Quartz Citations plugin
- **Better BibTeX**: ✅ Auto-exports to `bibliography.bib`

## Related Projects

- **Quartz**: https://quartz.jzhao.xyz/
- **Obsidian Zotero Integration**: https://github.com/mgmeyers/obsidian-zotero-integration
- **Better BibTeX for Zotero**: https://retorque.re/zotero-better-bibtex/

## License

MIT License - Feel free to adapt for your workflow!

## Credits

- Template design: Alem Šabić
- Built with: Obsidian, Zotero, Quartz
- Developed with assistance from Claude (Anthropic)

---

*Part of the [ale.ms](https://ale.ms) knowledge management system*
