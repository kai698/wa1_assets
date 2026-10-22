# WA1 Assets LFS Implementation Plan

> For agentic workers: REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

Goal: Configure wa1_assets for Git LFS, document repository usage, and migrate existing STL history to LFS.

Architecture: Add repository metadata files, commit them, create a backup branch, then rewrite local main with git lfs migrate import for STL paths. Do not push automatically.

Tech Stack: Git, Git LFS, Markdown.

Spec: docs/superpowers/specs/2026-10-22-wa1-assets-lfs-design.md

## Global Constraints

- Preserve mesh contents and URDF paths.
- Match kyber_assets LFS patterns, including .STL.
- Do not push rewritten history.

## Review Focus

- Uppercase .STL files must match LFS attributes.
- Existing history must have no normal Git blobs for migrated STL files.
- The checked-out meshes must remain hydrated binary files after migration.
- README commands must distinguish pointer files from hydrated files.

### Task 1: Repository metadata

Files: .gitattributes, .gitignore, README.md

- [x] Add LFS patterns, ignore rules, and usage documentation.
- [x] Verify attributes and documentation references.
- [x] Commit metadata.

### Task 2: History migration

Files: Git history only

- [x] Create a backup branch at the pre-migration commit.
- [x] Run git lfs migrate import --include='*.STL,*.stl' on local main.
- [x] Verify current-tree pointers, hydrated files, and migrated history.

### Task 3: Final verification

- [x] Run repository status and LFS verification commands.
- [x] Confirm no push was performed and report the backup branch.
