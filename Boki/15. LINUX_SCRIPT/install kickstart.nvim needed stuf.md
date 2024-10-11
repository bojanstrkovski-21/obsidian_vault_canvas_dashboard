# install kickstart.nvim
dependencies: ripgrep,fd,xclip,git,curl

kickstart on Linux
git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
to install run in terminal: nvim --headless "+Lazy! sync" +qa
after that in terminal open nvim let it sync and close and open and start working. 

Run :checkhealth in neovim and install anything thats missing some stuf must be installed from source so read down this document and follow directions and enjoy.

# Install ripgrep
sudo apt install ripgrep

# Install xclip
sudo apt install xclip

# Install fd
URL: https://github.com/sharkdp/fd

# Install cpanminus from source
URL:https://metacpan.org/pod/App::cpanminus

System: curl -L https://cpanmin.us | perl - --sudo App::cpanminus
Local: curl -L https://cpanmin.us | perl - App::cpanminus

# Install Java with Apt on Debian
URL: https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-debian-11

install it with this two packages
sudo apt install default-jre
sudo apt install default-jdk

Arch
sudo pacman -S jre-openjdk
sudo pacman -S jdk-openjdk


# Install go on Debian
URL: https://phoenixnap.com/kb/debian-install-go

Download the tar.gz file from download page https://go.dev/dl/

Go to the downloaded directory and open in teminal and paste the command: 
sudo tar -C /usr/local -xzf go1.19.2.linux-amd64.tar.gz

open .bashrc with text editor and add at the end of file:
export PATH=$PATH:/usr/local/go/bin
then save the file and reopen terminal and type: go version for verifying the installation is succses.

# Install julia 
URL: https://www.linuxfordevices.com/tutorials/install-julia-on-linux

Download tar.gz file from link: 
https://julialang.org/downloads/#current_stable_release

go to the download directory and open in terminal and type: tar -C $Home//local/share/ -xvzf julia.tar.gz and press enter

in terminal go to the unziped directory and in the bin directory and type ./julia to test if works and press ctrl+d to exit from julia

to create the executable file in terminal type: sudo ln -s $HOME/.local/share/julia.version/bin/julia /usr/local/bin/julia and press enter and after that is done you cen run julia from anywhere just with typing julia.

# Install nvm and nodejs
URL: https://tecadmin.net/how-to-install-nvm-on-debian-12/

execute the curl command in terminal: 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash 

then source your .bashrc file by typing in terminal: source .bashrc

to install latest nodejs type in terminal: nvm install node 

it is recomended to run in terminal: npm install -g npm@latest  to update npm to the latest for better performance.



