# External Asset Package Strategy

This project should use a lightweight public GitHub repository plus external Unity asset packages.

## Target architecture

### GitHub repository

Keep these in Git:

- source code
- `Packages/`
- `ProjectSettings/`
- small text configs
- package manifests and import instructions
- placeholder assets needed for an open-source fallback build
- documentation

Avoid putting large production assets in Git or Git LFS as the long-term default.

### External asset packages

Put approved redistributable binary content in downloadable `.unitypackage` files:

- public demo scenes
- models
- textures
- materials
- animation clips
- audio
- fonts
- baked lighting or navigation data
- large prefabs and effect resources

Users should download the required packages, then import them into the checked-out Unity project.

### User-supplied dependencies

Do not redistribute assets that are paid, license-restricted, or copyright-unclear. For these, provide installation instructions only:

- commercial Asset Store packages
- vendor SDKs
- copyrighted IP assets
- third-party packs without clear redistribution rights

## Recommended package split

Do not build one monolithic package for the whole project. Split packages by update cadence and legal status:

| Package | Contents | Notes |
| --- | --- | --- |
| `SubspaceHunter.PublicDemo.Scenes.unitypackage` | Public demo scenes and their scene-local data | Keep separate so scene edits do not force users to redownload all art assets. |
| `SubspaceHunter.PublicDemo.Gameplay.unitypackage` | Public gameplay prefabs, small configs, project-owned interaction assets | Should only contain redistributable project-owned content. |
| `SubspaceHunter.PublicDemo.Environments.unitypackage` | Approved environment meshes, textures, materials, skyboxes | Split again if this grows too large. |
| `SubspaceHunter.PublicDemo.Characters.unitypackage` | Approved original character assets only | Do not include copyrighted or third-party characters unless redistribution rights are clear. |
| `SubspaceHunter.PublicDemo.Audio.unitypackage` | Approved original or redistributable audio | Keep separate because audio is large and license-sensitive. |
| `SubspaceHunter.PublicDemo.Fonts.unitypackage` | Approved fonts or rebuilt fallback SDF assets | Prefer small fallback fonts for the public build. |

If a package grows beyond roughly 1-2 GB or changes frequently, split it further.

## Import order

Recommended user flow:

1. Clone the GitHub repository.
2. Open the project with Unity `2021.3.45f1`.
3. Install documented SDKs and third-party packages that must come from their official sources.
4. Import external public asset packages in this order:
   1. `Gameplay`
   2. `Environments`
   3. `Characters`
   4. `Audio`
   5. `Fonts`
   6. `Scenes`
5. Reopen Unity if the package import changes scripts, shaders, or project-wide assets.
6. Open `Assets/PublicDemo/PublicScenes/进入游戏.unity` or another documented entry scene.

## Packaging rules

- Export packages from Unity, not by manually zipping folders.
- Preserve original folder paths and `.meta` files so GUID references remain valid.
- Do not move assets before exporting unless the move is intentional and verified in Unity.
- Every package must contain only assets with confirmed redistribution rights.
- Keep a package manifest that records:
  - package filename
  - version
  - release date
  - Unity version
  - included root folders
  - dependency packages
  - license status
  - download URL
  - SHA-256 hash
- When one asset depends on another, either place both in the same package or document the dependency and import order.
- Prefer stable package names plus semantic versions, for example:

  ```text
  SubspaceHunter.PublicDemo.Scenes.v0.1.0.unitypackage
  ```

## Versioning

Use two version tracks:

- Git tags for code releases, such as `v0.1.0`
- matching asset package versions, such as `PublicDemo.Scenes v0.1.0`

The repository should document which asset package versions match each Git tag.

## Current transition state

The repository currently contains `Assets/PublicDemo/PublicScenes/` through Git LFS because those scenes are important project content. That is acceptable as a temporary bridge, but the long-term target is to move large demo scenes into external asset packages together with their approved dependencies, then keep only lightweight placeholders or import instructions in GitHub.

See `docs/PUBLIC_DEMO_DEPENDENCIES.zh-CN.md` for the current dependency audit.

## Next engineering steps

1. Classify every PublicDemo dependency root as:
   - public package
   - official/user-installed dependency
   - private-only
   - replacement required
2. Build the first candidate package set from redistributable assets only.
3. Test the packages by importing them into a clean clone.
4. Add a machine-readable package manifest once the package list stabilizes.
5. After package import is proven, decide whether to remove the LFS-hosted PublicDemo scenes from the repository history and public branch.
