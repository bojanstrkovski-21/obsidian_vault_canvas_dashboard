A.  Install build prerequisites on your system
Build prerequisites
General requirements (see #1469):
1. Clang or GCC version 4.9+
1. CMake version 3.10+, built with TLS/SSL support
   Optional: Get the latest CMake from an installer or the Python package (pip install cmake)

Platform-specific requirements are listed below.

I. Ubuntu / Debian
sudo apt-get install ninja-build gettext cmake unzip curl

II. CentOS / RHEL / Fedora
sudo dnf -y install ninja-build cmake gcc make unzip gettext curl

III. Arch Linux
sudo pacman -S base-devel cmake unzip ninja curl

IV. openSUSE
sudo zypper install ninja cmake gcc-c++ gettext-tools curl

V. Void Linux
xbps-install base-devel cmake curl git

VI. NixOS / Nix
1. Starting from NixOS 18.03, the Neovim binary resides in the neovim-unwrapped Nix package 
(the neovim package being just a wrapper to setup runtime options like Ruby/Python support):
cd path/to/neovim/src
2. Drop into nix-shell to pull in the Neovim dependencies:
nix-shell '<nixpkgs>' -A neovim-unwrapped
3. Configure and build 
rm -rf build && cmakeConfigurePhase
buildPhase
4. Tests are not available by default, because of some unfixed failures.
You can enable them via adding this package in your overlay:
  neovim-dev = (super.pkgs.neovim-unwrapped.override  {
    doCheck=true;
  }).overrideAttrs(oa:{
    cmakeBuildType="debug";

    nativeBuildInputs = oa.nativeBuildInputs ++ [ self.pkgs.valgrind ];
    shellHook = ''
      export NVIM_PYTHON_LOG_LEVEL=DEBUG
      export NVIM_LOG_FILE=/tmp/log
      export VALGRIND_LOG="$PWD/valgrind.log"
    '';
  });
and replacing neovim-unwrapped with neovim-dev:
nix-shell '<nixpkgs>' -A neovim-dev
5. Neovim contains a Nix flake in the contrib folder, with 3 packages:

    neovim to run the nightly
    neovim-debug to run the package with debug symbols
    neovim-developer to get all the tools to develop on neovim

Thus you can run Neovim nightly with:
nix run github:neovim/neovim?dir=contrib. Similarly to develop on Neovim: nix develop github:neovim/neovim?dir=contrib#neovim-developer.

B. Build Neovim:
1. git clone https://github.com/neovim/neovim
2. cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo
3. run "git checkout stable" If you want the stable release.
4. If you want to install to a custom location, set CMAKE_INSTALL_PREFIX. See also Installing Neovim.
   (On BSD, use gmake instead of make.
   (To build on Windows, see the Building on Windows section. MSVC (Visual Studio) is recommended.
5. On Debian/Ubuntu, instead of installing files directly with sudo make install, 
you can run "cd build && cpack -G DEB && sudo dpkg -i nvim-linux64.deb"  to build DEB-package and install it. 
This should help ensuring the clean removal of installed files.
Or Default install with "sudo make install" in Default install location "/usr/local"

Notes:
    From the repository's root directory, running make will download and build all the needed dependencies and put the nvim executable in build/bin.
    Third-party dependencies (libuv, LuaJIT, etc.) are downloaded automatically to .deps/. See the FAQ if you have issues.
    After building, you can run the nvim executable without installing it by running VIMRUNTIME=runtime ./build/bin/nvim.
    If you plan to develop Neovim, install Ninja for faster builds. It will automatically be used.
    Install ccache for faster rebuilds of Neovim. It's used by default. To disable it, use CCACHE_DISABLE=true make.
