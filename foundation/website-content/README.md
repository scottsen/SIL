# SIF Website Content - Source of Truth

**Status**: Source location for SIF-specific website pages
**Synced To**: `/projects/sif-website/docs/pages/`
**Created**: 2025-12-12 (fusipu-1212)

---

## Purpose

This directory contains the **source of truth** for SIF Foundation website pages that are NOT shared with the SIL website.

These pages are specific to the Semantic Infrastructure Foundation (501(c)(3) nonprofit) and should be version controlled separately from the shared SIL documentation.

---

## Workflow

### To Update SIF Website Pages

1. **Edit source files here**:
   ```bash
   cd /home/scottsen/src/projects/SIL/foundation/website-content/pages
   vim about.md  # or funding.md, contact.md, etc.
   ```

2. **Commit to git**:
   ```bash
   cd /home/scottsen/src/projects/SIL
   git add foundation/website-content/
   git commit -m "docs: Update SIF about page"
   git push
   ```

3. **Copy to website repo**:
   ```bash
   cp -r foundation/website-content/pages/* \
      /home/scottsen/src/projects/sif-website/docs/pages/
   ```

4. **Deploy** (see WEBSITE_DEPLOYMENT_GUIDE.md in sunny-cyclone-1212 session):
   ```bash
   cd /home/scottsen/src/projects/sif-website
   ./scripts/generate-llms-full.sh
   git commit -am "sync: Update SIF pages from source"
   ./deploy/deploy-container.sh staging --fresh
   ```

---

## Files

- `pages/about.md` - Foundation about page with mission, history
- `pages/funding.md` - Funding model and financial transparency
- `pages/research.md` - Research programs and initiatives
- `pages/contact.md` - Contact information
- `pages/index.md` - Homepage content
- `pages/foundation/` - Foundation team pages

---

## Note

This approach implements **Decision 1, Option A** from DECISIONS_NEEDED.md (sunny-cyclone-1212):
- Version control for SIF pages (previously untracked)
- Consistent with SIL docs workflow
- Manual copy for now (can automate sync later if needed)

---

**See Also**:
- `/projects/SIL/docs/README_SOURCE_OF_TRUTH.md` - Shared SIL documentation
- sunny-cyclone-1212 session - Website deployment documentation
