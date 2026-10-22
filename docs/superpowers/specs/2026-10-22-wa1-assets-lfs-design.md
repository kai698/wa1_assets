# WA1 Assets LFS Design

## Intent

Move the existing WA1 mesh binaries out of normal Git blobs and into Git LFS, while documenting repository usage and ignoring local/generated files.

## Scope

- Add Git LFS attributes matching the asset formats used by kyber_assets, including uppercase .STL files.
- Add a conservative .gitignore for editor, OS, Python, and generated conversion artifacts.
- Add a Chinese README covering setup, fetch, verification, and contribution workflows.
- Rewrite the existing local main history so tracked mesh binaries are represented by LFS pointers; create a backup branch before rewriting.

## Non-goals

- Do not change URDF contents or mesh geometry.
- Do not push the rewritten history to origin automatically.

## Approach

Use git lfs migrate import --include='*.STL,*.stl' after committing the repository metadata. Preserve a local backup branch pointing at the pre-migration commit, then verify the new tree contains LFS pointers and that the working tree contains hydrated binary meshes.
