# dotfiles

Personal dotfiles managed with [GNU Stow](https://www.gnu.org/software/stow/).

## Packages

| Package | Symlinks |
|---------|----------|
| `git`   | `~/.gitconfig`, `~/.gitignore_global` |
| `kitty` | `~/.config/kitty/` |

## Setup on a new machine

```bash
# 1. Install stow
sudo apt install stow        # Debian/Ubuntu
sudo pacman -S stow          # Arch
brew install stow            # macOS

# 2. Clone the repo
git clone <repo-url> ~/dotfiles
cd ~/dotfiles

# 3. Stow individual packages
stow git
stow kitty

# or stow everything at once
stow */
```

Stow creates symlinks from `~` into the package directories, so `dotfiles/kitty/.config/kitty/kitty.conf` becomes `~/.config/kitty/kitty.conf`.

To remove symlinks for a package: `stow -D <package>`

## Updating

A `git pull` is enough to apply changes — symlinks point directly into the repo, so updates are live immediately. Only run `stow <package>` again if you add a new file that doesn't have a symlink yet.
