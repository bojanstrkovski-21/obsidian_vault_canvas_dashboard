### Installation
Arch:    `sudo pacman -S fzf`
Debian: `sudo apt install fzf`
Fedora:  `sudo dnf install fzf`
Open-Suse:  `sudo zypper install fzf`
Void-Linux:   `sudo xbps-install -S fzf`
NixOS:  `nix-env -iA nixpkgs.fzf` or `declare it in configuration.nix nixpkgs.fzf`


from source:  
```shell
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

Setting up shell integration
Add the following line to your shell configuration file.

- bash
    
    ```shell
    # Set up fzf key bindings and fuzzy completion
    eval "$(fzf --bash)"
    ```
    

zsh

```shell
# Set up fzf key bindings and fuzzy completion
source <(fzf --zsh)
```

fish

```fish
# Set up fzf key bindings
fzf --fish | source
```

Source:
https://github.com/junegunn/fzf.git
