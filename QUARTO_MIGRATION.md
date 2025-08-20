# Quarto Migration Guide

This document explains how to use the new Quarto-based workflow alongside the existing Pandoc/Make workflow.

## Prerequisites

To use the Quarto workflow, you need:

1. [Quarto CLI](https://quarto.org/docs/get-started/installation.html)
2. [Pandoc](http://pandoc.org/installing.html) (typically installed with Quarto)
3. [Tectonic](https://tectonic-typesetting.github.io/) or another LaTeX distribution for PDF output
4. [pandoc-crossref](https://github.com/lierdakil/pandoc-crossref) for cross-references in the thesis

## Quick Start

### Render All Projects
```bash
quarto render
```

### Render Individual Projects
```bash
# Article
quarto render article/

# Presentation  
quarto render presentation/

# Thesis
quarto render thesis/
```

### Render Specific Formats
```bash
# Article as PDF only
quarto render article/ --to pdf

# Presentation as HTML slides only
quarto render presentation/ --to revealjs

# Thesis as DOCX only
quarto render thesis/ --to docx
```

## Project Configuration

Each project directory now contains a `_quarto.yml` file that configures:

- Output formats (PDF, DOCX, HTML, etc.)
- Format-specific options (PDF engine, slide level, etc.)
- Filters and extensions
- File inclusion order (for multi-file projects like thesis)

### Article Project
- **Type**: Default project
- **Input**: `article.md`
- **Formats**: DOCX, PDF, LaTeX
- **Config**: `article/_quarto.yml`

### Presentation Project  
- **Type**: Default project
- **Input**: `presentation.md`
- **Formats**: RevealJS (HTML), PDF, PowerPoint, LaTeX
- **Config**: `presentation/_quarto.yml`

### Thesis Project
- **Type**: Book project
- **Input**: Multiple chapters (00.md, 00_Introduction.md, etc.)
- **Formats**: DOCX, EPUB, PDF, LaTeX
- **Config**: `thesis/_quarto.yml`
- **Special Features**: Custom filters, multiple bibliographies

## Migration Benefits

1. **Unified Build System**: Single command to render all formats
2. **Modern Tooling**: Quarto provides advanced features like cross-references, code execution, and interactive content
3. **Better Error Handling**: Clearer error messages and debugging
4. **Extensibility**: Easy to add new formats or customize existing ones
5. **IDE Integration**: Better support in RStudio, VS Code, and other editors

## Backward Compatibility

The original Pandoc/Make workflow is preserved:
- All original YAML configuration files remain
- Makefile continues to work
- GitHub Actions support both workflows

This allows for gradual migration and comparison between approaches.

## Testing the Migration

To verify everything works:

1. Install Quarto
2. Run `quarto render article/` 
3. Compare output with `make article`
4. Check that all expected files are generated
5. Verify content quality matches original output

## Common Issues and Solutions

### Missing pandoc-crossref
If you get errors about pandoc-crossref, install it:
```bash
# On macOS with Homebrew
brew install pandoc-crossref

# On Linux, download from GitHub releases
wget https://github.com/lierdakil/pandoc-crossref/releases/latest/download/pandoc-crossref-Linux.tar.xz
tar -xf pandoc-crossref-Linux.tar.xz
sudo mv pandoc-crossref /usr/local/bin/
```

### Lua Filter Errors
The thesis project uses custom Lua filters. Ensure they're in the correct path (`thesis/filters/`) and have proper permissions.

### LaTeX Errors
If you encounter LaTeX errors with PDF output:
1. Ensure Tectonic or another LaTeX distribution is installed
2. Check that all required LaTeX packages are available
3. Consider using `--pdf-engine=xelatex` as an alternative

## Next Steps

1. Test the Quarto workflow with your content
2. Customize `_quarto.yml` files as needed
3. Report any issues or improvements needed
4. Consider fully migrating once comfortable with the new workflow