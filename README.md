# AUR Package for Mumble Client (`mumble-9m2pju-git`)

This repository contains the packaging specification files (`PKGBUILD` and `.SRCINFO`) to build and package the **Mumble Client** directly from the official [Mumble GitHub repository](https://github.com/mumble-voip/mumble) for Arch Linux and Arch-based distributions (e.g. Manjaro, EndeavourOS, Garuda).

---

## 📁 Package Files

- [`PKGBUILD`](file:///home/x/mumble-9m2pju-bin/PKGBUILD): Arch Linux package build script.
- [`.SRCINFO`](file:///home/x/mumble-9m2pju-bin/.SRCINFO): Package metadata for the Arch User Repository (AUR).

---

## 🛠️ Build and Install Locally

To build and install this package locally on an Arch Linux system:

```bash
# 1. Install base-devel and git if not already present
sudo pacman -S --needed base-devel git

# 2. Build and install the package
makepkg -si
```

---

## 🚀 How to Publish to the AUR

If you wish to submit/maintain this package on the Arch User Repository (AUR):

1. **Register an AUR Account**:
   Create an account at [aur.archlinux.org](https://aur.archlinux.org/) and add your SSH key in account settings.

2. **Clone the AUR repository for your package**:
   ```bash
   git clone ssh://aur@aur.archlinux.org/mumble-9m2pju-git.git
   cd mumble-9m2pju-git
   ```

3. **Copy `PKGBUILD` and update `.SRCINFO`**:
   ```bash
   # Generate fresh .SRCINFO from PKGBUILD
   makepkg --printsrcinfo > .SRCINFO
   ```

4. **Commit and Push to AUR**:
   ```bash
   git add PKGBUILD .SRCINFO
   git commit -m "Initial commit for mumble-9m2pju-git"
   git push origin master
   ```

---

## ⚙️ Key Packaging Options

- **Client Only**: Configured with `-Dclient=ON -Dserver=OFF` to compile only the user-facing client.
- **Qt6 & Modern Stack**: Uses Qt6, Opus, Protobuf, and Ninja build system.
- **Git Submodules**: `git submodule update --init --recursive` is run in `prepare()` to fetch internal submodules like `minhook`, `spdlog`, and `rnnoise`.
