# Contributing to SIL

## Repository Architecture

SIL uses a two-repo model:

| Repo | Purpose | Visibility |
|------|---------|------------|
| **SIL** | Canonical documentation source of truth | Public |
| **sil-website** | Website application that serves docs | Public |

```
SIL/docs/  ───(sync-docs.sh)───►  sil-website/docs/ (gitignored)
                                         │
                                         ▼
                                   Website serves
```

## Where to Edit Documentation

**Always edit in `SIL/docs/`** — this is the source of truth.

Never edit directly in `sil-website/docs/` — those files are gitignored and will be overwritten on next sync.

### Workflow

1. Edit docs in `SIL/docs/`
2. Commit and push to SIL repo
3. Run `sil-website/scripts/sync-docs.sh` to copy to website
4. Deploy website (if needed)

## Private vs Public Content

### Public (SIL repo)
- All documentation in `docs/`
- Project index in `projects/`
- README, LICENSE, CITATION

### Private (NOT in this repo)
- Internal strategy and planning
- Personnel notes
- Pitch materials
- Investor frameworks

**The `internal/` directory is gitignored.** If you need to work on internal content, use TIA's private workspace (`tia/projects/SIL/internal/`).

## Directory Structure

```
SIL/
├── docs/
│   ├── canonical/       # Core philosophy, architecture, principles
│   ├── innovations/     # GenesisGraph, reveal, morphogen, etc.
│   ├── research/        # Papers, standards, research notes
│   ├── meta/            # FAQ, founder background, acknowledgments
│   ├── tools/           # Tool documentation
│   ├── architecture/    # Architecture guides
│   └── vision/          # Long-term vision docs
├── projects/            # Project index
├── README.md
├── LICENSE
└── CITATION.cff
```

## Commit Guidelines

- Use conventional commits: `feat:`, `fix:`, `docs:`, `security:`
- For documentation: `docs(area): description`
- For security fixes: `security: description`

## Questions?

Open an issue or see the [FAQ](docs/meta/FAQ.md).
