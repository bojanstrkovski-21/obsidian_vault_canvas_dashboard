A. Build Prerequisites

1. Neovim 0.8 or newer
2. Nerd Fonts ( Dejavu, Droid, Fira Code,Fira Mono,Hack Nerd, Incosolata, 
Iosevska, JetBrainsMono Nerd Font, source-code-pro,Meslo,
Mononolki nerd, Notosans, Roboto Mono, Space Mono, 
Terminess nerd-Terminus, Ubuntu Font)
3. Rust + Tree-sitter CLI 
 3.1 Rust: curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
 3.2 Tree-sitter: cargo install tree-sitter-cli
4. Xclip - clipboaedtool
5. Ripgrep
6. lazygit: 
 6.1 Ubuntu/Debian
 LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | grep -Po '"tag_name": "v\K[^"]*')
 curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/latest/download/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
 tar xf lazygit.tar.gz lazygit
 sudo install lazygit /usr/local/bin
 6.2 Archlinux: sudo pacman -S lazygit
 6.3 Fedora/Rhel: 
     sudo dnf copr enable atim/lazygit -y
     sudo dnf install lazygit
 6.4 Void Linux: sudo xbps-install -S lazygit
 6.5 bottom: on rustp stable: cargo install bottom --locked
 6.6 Python: python.org

7. Perl
     wget https://www.cpan.org/src/5.0/perl-5.38.0.tar.gz
     tar -xzf perl-5.38.0.tar.gz
     cd perl-5.38.0
     ./Configure -des -Dprefix=$HOME/localperl
     make
     make test
     make install
 7.1 Perl neovim integration:
     install cpanminus installer first: curl -L https://cpanmin.us | perl - --sudo App::cpanminus
     install module for neovim: cpanm -n Neovim::Ext
8. Ruby: 
 8.1 Ubuntu/Debian
     sudo apt-get install ruby-full
 8.2 CentOS, Fedora, or RHEL
     sudo yum install ruby
 8.3 Arch linux
     sudo pacman -S ruby
 a. gem install neovim for neovim integration
9. Node: 
   a. Install nvm: curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   "source ~/.bashrc" source the shell
   nvm list-remote  for listing node versions 
   nvm install node  for installing latest nodej+npm
  9.1 for neovim integration insstall: npm install -g neovim
10. ncurses sudo apt-get install libncurses5-dev libncursesw5-dev

B. Install  Astronvim
bacup older: 
mv ~/.config/nvim ~/.config/nvim.bak
mv ~/.local/share/nvim ~/.local/share/nvim.bak
git clone --depth 1 https://github.com/AstroNvim/AstroNvim ~/.config/nvim
nvim
