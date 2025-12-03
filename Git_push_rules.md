# Git Push Debugging Rules

## Pre-Push Checklist

Before pushing changes to this Jekyll website, verify:

### 1. Bibliography (papers.bib)
- All BibTeX entries must have valid syntax (matching braces `{}`)
- Required fields: `title`, `author`, `year`
- Optional but recommended: `bibtex_show={true}`, `preview={image.png}`
- For selected papers on homepage: add `selected={true}`
- Preview images must exist in `assets/img/publication_preview/`

### 2. News Announcements (_news/)
- Front matter must include: `layout: post`, `date`, `inline: true/false`
- Date format: `YYYY-MM-DD HH:MM:SS-TIMEZONE` (e.g., `2025-11-06 12:00:00-0500`)
- Links should use HTML `<a href="...">` tags for inline announcements

### 3. Pages (_pages/)
- Front matter YAML must be valid (check colons, indentation)
- Boolean values: `true`/`false` (not quoted)
- Liquid templates must have matching `{% %}` tags

### 4. Config (_config.yml)
- YAML syntax must be valid
- Multi-line strings use `>` or `|`
- Check indentation (2 spaces)

### 5. Assets
- PDF files must be copied to `assets/pdf/`
- Images must be in appropriate `assets/img/` subdirectories
- File names should not contain spaces

## Common Errors

### Broken Links Check Failure
The `check-links-on-site` workflow may fail if:
- Links to external sites are dead
- Internal links reference non-existent pages
- arXiv/DOI links are malformed

**This is a non-blocking warning** - the site still deploys even if this check fails.

### Jekyll Build Errors
Check for:
- Invalid YAML in front matter
- Unclosed Liquid tags
- Missing include files
- Invalid BibTeX syntax

## Debugging Steps

1. Check GitHub Actions: `https://github.com/Jinyeop3110/Jinyeop3110.github.io/actions`
2. Look at the "Deploy site" workflow, not "Check for broken links"
3. If deploy fails, check the build logs for specific error messages
4. Common fixes:
   - Validate YAML: https://www.yamllint.com/
   - Validate BibTeX: https://biblatex-check.herokuapp.com/
   - Check Liquid syntax in templates

## GitHub Actions Workflows

| Workflow | Purpose | Blocking? |
|----------|---------|-----------|
| Deploy site | Builds and deploys Jekyll site | Yes |
| Prettier code formatter | Checks code formatting | No |
| Check for broken links | Validates internal/external links | No |
| Axe | Accessibility testing | No |
| Lighthouse | Performance testing | No |

## Quick Commands

```bash
# Check git status before pushing
git status

# View recent commits
git log --oneline -5

# Check GitHub Actions status (requires gh CLI)
gh run list --limit 5

# View specific run logs
gh run view <run-id> --log
```
