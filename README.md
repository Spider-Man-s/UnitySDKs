# Unity SDK Package Repository

A centralized repository for hosting and distributing multiple Unity packages through GitHub.

Each SDK is stored in its own folder and can be installed independently using Unity Package Manager (UPM) via Git URLs.

## Repository Structure

```text
UnitySDKs/
├── README.md
└── Packages/
    ├── SDK1/
    │   ├── package.json
    │   ├── Runtime/
    │   └── ...
    │
    ├── SDK2/
    │   ├── package.json
    │   ├── Runtime/
    │   └── ...
    │
    ├── SDK3/
    │   ├── package.json
    │   └── ...
    │
    └── ...
```

**Important:** Each SDK folder must contain its own `package.json` at its root.

## Adding a New SDK

1. Obtain or extract the Unity package.
2. Create a new folder inside `Packages/`.
3. Copy the package contents into that folder.
4. Make sure `package.json` is directly inside the new folder.
5. Commit and push the changes to GitHub.

Example:

```text
Packages/
└── MyNewSDK/
    ├── package.json
    ├── Runtime/
    ├── Editor/
    └── ...
```

## Installing Packages in Unity

Packages can be installed directly from GitHub using Unity Package Manager.

### Method 1: Package Manager

1. Open Unity.
2. Navigate to Window → Package Manager.
3. Click the `+` button.
4. Select **Install package from git URL...**
5. Enter the package Git URL.

Example:

```text
https://github.com/USERNAME/UnitySDKs.git?path=/Packages/MyNewSDK
```

### Method 2: manifest.json

You can also install packages by editing your Unity project's:

```text
Packages/manifest.json
```

Add the desired packages under `dependencies`:

```json
{
  "dependencies": {
    "com.company.sdk1": "https://github.com/USERNAME/UnitySDKs.git?path=/Packages/SDK1#main",
    "com.company.sdk2": "https://github.com/USERNAME/UnitySDKs.git?path=/Packages/SDK2#main",
    "com.company.sdk3": "https://github.com/USERNAME/UnitySDKs.git?path=/Packages/SDK3#main"
  }
}
```

Replace:

- `USERNAME` with your GitHub username.
- `UnitySDKs` with your repository name.
- `SDK1`, `SDK2`, etc. with the actual folder names.
- Package identifiers with the corresponding `name` values from each `package.json`.

## Understanding Git URLs

The URL format is:

```text
https://github.com/USERNAME/REPOSITORY.git?path=/FOLDER/PACKAGE#BRANCH
```

| Component    | Description                     |
| ------------ | ------------------------------- |
| `USERNAME`   | GitHub username or organization |
| `REPOSITORY` | Repository name                 |
| `path`       | Folder containing package.json  |
| `BRANCH`     | Git branch (e.g. main)          |

Example:

```text
https://github.com/USERNAME/UnitySDKs.git?path=/Packages/MyNewSDK#main
```

All packages can share the same repository and branch.

## Updating Packages

When a package is updated:

1. Replace or modify its files locally.
2. Commit the changes.
3. Push to GitHub.

```bash
git add .
git commit -m "Update MyNewSDK"
git push origin main
```

Unity can then retrieve the updated package. You may need to refresh or resolve packages in Package Manager.

## Versioning

For stable package versions, Git tags are recommended.

Example:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Install a specific version using:

```text
https://github.com/USERNAME/UnitySDKs.git?path=/Packages/MyNewSDK#v1.0.0
```

This allows projects to remain pinned to a specific SDK version.

## Important Notes

- Every package must have a valid `package.json`.
- The package identifier must be unique.
- The package folder must contain the `package.json` directly, not inside another nested folder.
- Git must be installed and available in your system PATH.
- Unity Git dependencies require the repository to be accessible to the installing machine.
- Private repositories require GitHub authentication.
- Git URL dependencies install extracted Unity packages, not `.tgz` archives directly. For `.tgz` files, extract them first if you want to use the `?path=` approach.

---

**Goal:** One GitHub repository, one branch, multiple independently installable Unity SDK packages.
