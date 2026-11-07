# spec-kit explore

A read-only spec-kit command that surveys a project and reports:

- codebase condition (stack, architecture, risks)
- readiness of the latest feature (tasks and checklists checked against the actual code)
- recent changes (git history and uncommitted work)

## Install

```bash
specify extension add --dev /path/to/speckit-extensions/explore
```

## Usage

```
/speckit-explore-explore
/speckit-explore-explore pay extra attention to the modules API
```

The optional argument is a focus hint; that area is read in depth and gets its own section in the report.
