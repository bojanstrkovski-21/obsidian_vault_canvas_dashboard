Neovim-preparation-required-stuf
========================

## I. Basic tools for installing everything

### 1. wget 
a. Debian: `sudo apt install wget` \
b. ArchLinux: `sudo pacman -S wget` \
c. Fedora: `sudo dnf install wget` \
d. OpenSuse: `sudo zypper install wget` \

### 2. curl
a. Debian: `sudo apt install curl` \
b. ArchLinux: `sudo pacman -S curl` \
c. Fedora: `sudo dnf install curl` \
d. OpenSuse: `sudo zypper install curl` 

### 3. git
a. Debian: `sudo apt install git` \
b. ArchLinux: `sudo pacman -S git` \
c. Fedora: `sudo dnf install git` \
d. OpenSuse: `sudo zypper install git`

### 4. ripgrep
a. Debian: `sudo apt install ripgrep` \
b. ArchLinux: `sudo pacman -S ripgrep ripgrep-all` \
c. Fedora: `sudo dnf install ripgrep` \
d. OpenSuse: `sudo zypper install ripgrep` \

URL: https://github.com/BurntSushi/ripgrep

### 5. make
a. Debian: `sudo apt install make` \
b. ArchLinux: `sudo pacman -S make` \
c. Fedora: `sudo dnf install make` \
d. OpenSuse: `sudo zypper install make`  

### 6. cmake
a. Debian: `sudo apt install cmake` \
b. ArchLinux: `sudo pacman -S cmake` \
c. Fedora: `sudo dnf install cmake` \
d. OpenSuse: `sudo zypper install cmake`

### 7. unzip
a. Debian: `sudo apt install unzip` \
b. ArchLinux: `sudo pacman -S unzip` \
c. Fedora: `sudo dnf install unzip` \
d. OpenSuse: `sudo zypper install unzip`\

### 8. fd
ArchLinux: `sudo pacman -S fd` \

URL: https://github.com/sharkdp/fd

### 9. FZF - fuzy finder
ArchLinux: `sudo pacman -S fzf` \

https://github.com/junegunn/fzf

## II. Rust language
`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
## III. Treesitter
`cargo install tree-sitter-cli`

## IV. Python

Arch
```bash
sudo pacman -S python
sudo pacman -S python-pynvim
sudo pacman -S python-pip
sudo pacman -S python-pipx
```


IF not arch

```bash
sudo pacman -S python-pylint-venv
mkdir -p ~/venv
cd into home dir and
python3 -m  virtualenv venv 
(in arch:  python -m  virtualenv venv)
source venv/bin/activate
```

## V. Nerd Fonts
```bash
sudo pacman -S --noconfirm otf-droid-nerd
sudo pacman -S --noconfirm otf-firamono-nerd
sudo pacman -S --noconfirm ttf-dejavu-nerd
sudo pacman -S --noconfirm ttf-firacode-nerd
sudo pacman -S --noconfirm ttf-hack-nerd
sudo pacman -S --noconfirm ttf-inconsolata-go-nerd
sudo pacman -S --noconfirm ttf-inconsolata-lgc-nerd
sudo pacman -S --noconfirm ttf-inconsolata-nerd
sudo pacman -S --noconfirm ttf-iosevka-nerd
sudo pacman -S --noconfirm ttf-iosevkaterm-nerd
sudo pacman -S --noconfirm ttf-jetbrains-mono-nerd
sudo pacman -S --noconfirm ttf-meslo-nerd
sudo pacman -S --noconfirm ttf-monofur-nerd
sudo pacman -S --noconfirm ttf-mononoki-nerd
sudo pacman -S --noconfirm ttf-noto-nerd
sudo pacman -S --noconfirm ttf-roboto-mono-nerd
sudo pacman -S --noconfirm ttf-sourcecodepro-nerd
sudo pacman -S --noconfirm ttf-terminus-nerd
sudo pacman -S --noconfirm ttf-ubuntu-mono-nerd
sudo pacman -S --noconfirm ttf-ubuntu-nerd
```

## VI. Perl and Cpanminus
### 1. Perl
a. ArchLinux: `sudo pacman -S perl`
b. Debian: 
```bash
tar -xzf perl-5.38.0.tar.gz
cd perl-5.38.0
./Configure -des -Dprefix=$HOME/localperl
make
make test
make install
```

### 2. Cpanminus for Perll neovim integration:
URL: https://metacpan.org/pod/App::cpanminus

a. Install SystemWide: `curl -L https://cpanmin.us | perl - --sudo App::cpanminus`
b. Install LocalUser: `curl -L https://cpanmin.us | perl - App::cpanminus`
c. Install neovim module: \
  SystemWide: `sudo cpanm -n Neovim::Ext` \
  LocarUser: `cpanm -n Neovim::Ext`

## VII. Java
URL: https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-debian-11
### 1. Debian
`sudo apt install default-jdk`
### 2. Arch
`sudo pacman -S jdk-openjdk`

## VIII. GO Language
### 1. Debian
URL: https://phoenixnap.com/kb/debian-install-go

Download the tar.gz file from download page https://go.dev/dl/

Go to the downloaded directory and open in teminal and paste the command: \
`sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz` \

open .bashrc with text editor and add at the end of file: \
`export PATH=$PATH:/usr/local/go/bin`
than save the .bashrc file and source .bashrc: `source ~/.bashrc`
or close and reopen terminal
for veficatiopn that go is installed in terminal type `go version`

## IX. Nvm and Nodejs
### 1. nvm install
URL: https://tecadmin.net/how-to-install-nvm-on-debian-12/
`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash`
`source ~/.bashrc`
### 2. install latest nodejs and npm
`nvm install node`
`npm install -g npm@latest `

## X. Ruby
1. Ubuntu/Debian

`sudo apt-get install ruby-full` \

2. CentOS, Fedora, or RHEL

`sudo yum install ruby` \
`sudo dnf install ruby` \

3. Arch linux

`sudo pacman -S ruby`

a. For neovim integration install: `gem install neovim`

## XI. Lua language and stuf
1. lua
a. Debian: `sudo apt install lua5.4`
b. ArchLinux: `sudo pacman -S lua`
2. luarocks
a. Debian: `sudo apt install luarocks`
b. ArchLinux: `sudo pacman -S luarocks`
3. luajit
a. Debian: `sudo apt install luajit`
b. ArchLinux: `sudo pacman -S luajit`
4. lua-check
a. Debian: `sudo apt install lua-check`
b. ArchLinux: `sudo pacman -S lua-check`

## XII. Julia
URL: https://www.linuxfordevices.com/tutorials/install-julia-on-linux

1. Download tar.gz file from link:
URL: https://julialang.org/downloads/#current_stable_release

2. Go to the download directory and open in terminal and type:
`tar -C $Home//local/share/ -xvzf julia.tar.gz`

3. for running julia from anywhere in terminal go to the unziped directory and in the bin directory ($HOME/.local/share/julia.version/bin/julia) and type:
`sudo ln -s $HOME/.local/share/julia.version/bin/julia /usr/local/bin/julia`