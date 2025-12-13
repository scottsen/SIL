# SOURCE OF TRUTH - Edit Files Here

⚠️ **This directory contains the canonical documentation for the Semantic Infrastructure Lab**

## Critical Information

**EDIT HERE**: These files are the source of truth and are synced to website repositories

**DO NOT EDIT**:
- `/projects/sil-website/docs/` ← SYNCED (will be overwritten by sync-docs.sh)
- `/projects/sif-website/docs/canonical/` ← SYNCED (will be overwritten by sync-docs.sh)

## Workflow

When you update files in this directory:

```bash
# 1. Edit source files HERE
cd /home/scottsen/src/projects/SIL
vim docs/meta/FOUNDER_BACKGROUND.md

# 2. Commit changes HERE
git add docs/
git commit -m "docs: update founder background"
git push

# 3. Sync to website repos
cd /home/scottsen/src/projects/sil-website
./scripts/sync-docs.sh

# 4. Regenerate llms-full.txt
./scripts/generate-llms-full.sh

# 5. Deploy
./deploy/deploy-container.sh staging --fresh
```

## What Gets Synced

The following directories are synced to website repositories:

- `canonical/` → SIL & SIF websites
- `architecture/` → SIL & SIF websites
- `research/` → SIL & SIF websites
- `meta/` → SIL website
- `innovations/` → SIL & SIF websites
- `tools/` → SIL & SIF websites

## Documentation

See: `/home/scottsen/src/tia/sessions/sunny-cyclone-1212/WEBSITE_DEPLOYMENT_GUIDE.md`

## Last Updated

2025-12-12 (sunny-cyclone-1212)
