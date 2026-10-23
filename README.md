# dotfiles

Personal dotfiles managed with [GNU Stow](https://www.gnu.org/software/stow/).

## Packages

| Package | Symlinks |
|---------|----------|
| `git`   | `~/.config/git/config`, `~/.config/git/ignore` |
| `kitty` | `~/.config/kitty/kitty.conf`, `~/.config/kitty/colors.conf` |
| `obsidian` | `~/Documents/local/.obsidian/themes/foyay/manifest.json`, `~/Documents/local/.obsidian/themes/foyay/theme.css` |

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
stow obsidian

# or stow everything at once
stow */
```

The `obsidian` package expects the vault at `~/Documents/local`. After stowing, pick foyay under Settings → Appearance → Themes. It has light and dark variants.

Stow creates symlinks from `~` into the package directories, so `dotfiles/kitty/.config/kitty/kitty.conf` becomes `~/.config/kitty/kitty.conf`.

`.stowrc` sets `--no-folding`, so stow creates real directories and links only individual files. Anything an app writes next to its config (caches, credentials, vault data) stays out of the repo. Stow only reads `.stowrc` from the current directory, so always run it from `~/dotfiles`.

To remove symlinks for a package: `stow -D <package>`

## Machine-specific git settings

`~/.gitconfig` is not in this repo. Git reads `~/.config/git/config` first and `~/.gitconfig` second, so a value in `~/.gitconfig` overrides the shared one. Use it for settings that differ per machine, such as a work email:

```ini
[user]
	email = you@work.example
```

## Updating

A `git pull` is enough to apply changes — symlinks point directly into the repo, so updates are live immediately. Only run `stow <package>` again if you add a new file that doesn't have a symlink yet. If you delete or rename a file, run `stow -R <package>` to clean up the stale symlink.
