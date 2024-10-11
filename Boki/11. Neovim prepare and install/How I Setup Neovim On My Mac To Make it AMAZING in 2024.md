---
created: 2024-04-06T22:13:05 (UTC +02:00)
tags: []
source: https://www.josean.com/posts/how-to-setup-neovim-2024
author: 
---

# How I Setup Neovim On My Mac To Make it AMAZING in 2024

> ## Excerpt
> Use this guide along with my youtube video to setup Neovim & make it amazing in 2024

---
You can find the source code for my config [here](https://github.com/josean-dev/dev-environment-files).

## Open a terminal window

Open a terminal window on your mac. You will need a true color terminal for the colorscheme to work properly.

I’m using _iTerm2_

## Install Homebrew

Run the following command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

If necessary, when prompted, enter your password here and press enter. If you haven’t installed the XCode Command Line Tools, when prompted, press enter and homebrew will install this as well.

## Add To Path (Only Apple Silicon Macbooks)

After installing, add it to the path. This step shouldn’t be necessary on Intel macs.

Run the following two commands to do so:

```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' &gt;&gt; ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

## Install iTerm2 If Necessary

If you don’t have a true color terminal, install iTerm2 with homebrew:

```
brew install --cask iterm2
```

Then switch to this terminal.

## Install A Nerd Font

I use Meslo Nerd Font. To install it do:

```
brew tap homebrew/cask-fonts
```

And then do:

```
brew install font-meslo-lg-nerd-font
```

Then open iTerm2 settings with `CMD+,` and under **Profiles > Text** change the font to **MesloLGS Nerd Font Mono**

## Install Neovim

Run:

## Install Ripgrep

Run:

## Install Node

Run:

## Setup Initial File Structure

Your config will be located in `~/.config/nvim`.

Let’s setup the initial file structure with the following commands:

Make the nvim config directory.

_`-p` is used to also create parent directories if they don’t already exist_

Move to this directory:

Create main `init.lua` file:

Create `lua/josean/core` directories:

_Any time I use “josean” you can replace this with your name_

Create plugins directory (will have all of the plugin configs/specs):

```
mkdir -p lua/josean/plugins
```

Create `lazy.lua` file (will be used to setup/configure lazy.nvim plugin manager):

```
touch lua/josean/lazy.lua
```

## Setup core options

Make sure you’re in `~/.config/nvim` and open the config:

Navigate to the core folder and press `%` to create a file and call it: “options.lua”

In this file add:

```
vim.cmd("let g:netrw_liststyle = 3")
```

Open the explorer with `:Explore` and navigate to the main `init.lua` file.

Add the following to load the basic options on startup:

```
require("josean.core.options")
```

Close Neovim with `:w` and reopen it with `nvim .`

Go back to “options.lua” and add the following to setup the rest of the options:

```
local opt = vim.opt -- for conciseness

-- line numbers
opt.relativenumber = true -- show relative line numbers
opt.number = true -- shows absolute line number on cursor line (when relative number is on)

-- tabs &amp; indentation
opt.tabstop = 2 -- 2 spaces for tabs (prettier default)
opt.shiftwidth = 2 -- 2 spaces for indent width
opt.expandtab = true -- expand tab to spaces
opt.autoindent = true -- copy indent from current line when starting new one

-- line wrapping
opt.wrap = false -- disable line wrapping

-- search settings
opt.ignorecase = true -- ignore case when searching
opt.smartcase = true -- if you include mixed case in your search, assumes you want case-sensitive

-- cursor line
opt.cursorline = true -- highlight the current cursor line

-- appearance

-- turn on termguicolors for nightfly colorscheme to work
-- (have to use iterm2 or any other true color terminal)
opt.termguicolors = true
opt.background = "dark" -- colorschemes that can be light or dark will be made dark
opt.signcolumn = "yes" -- show sign column so that text doesn't shift

-- backspace
opt.backspace = "indent,eol,start" -- allow backspace on indent, end of line or insert mode start position

-- clipboard
opt.clipboard:append("unnamedplus") -- use system clipboard as default register

-- split windows
opt.splitright = true -- split vertical window to the right
opt.splitbelow = true -- split horizontal window to the bottom

-- turn off swapfile
opt.swapfile = false
```

Do `:e lua/josean/core/init.lua`

Add the following:

```
require("josean.core.options")
```

Open the explorer with `:Explore` and go to the main init.lua file and change the require to:

## Setup core keymaps

Do `:e lua/josean/core/keymaps.lua`

And add the following to this file:

```
-- set leader key to space
vim.g.mapleader = " "

local keymap = vim.keymap -- for conciseness

---------------------
-- General Keymaps -------------------

-- use jk to exit insert mode
keymap.set("i", "jk", "&lt;ESC&gt;", { desc = "Exit insert mode with jk" })

-- clear search highlights
keymap.set("n", "&lt;leader&gt;nh", ":nohl&lt;CR&gt;", { desc = "Clear search highlights" })

-- delete single character without copying into register
-- keymap.set("n", "x", '"_x')

-- increment/decrement numbers
keymap.set("n", "&lt;leader&gt;+", "&lt;C-a&gt;", { desc = "Increment number" }) -- increment
keymap.set("n", "&lt;leader&gt;-", "&lt;C-x&gt;", { desc = "Decrement number" }) -- decrement

-- window management
keymap.set("n", "&lt;leader&gt;sv", "&lt;C-w&gt;v", { desc = "Split window vertically" }) -- split window vertically
keymap.set("n", "&lt;leader&gt;sh", "&lt;C-w&gt;s", { desc = "Split window horizontally" }) -- split window horizontally
keymap.set("n", "&lt;leader&gt;se", "&lt;C-w&gt;=", { desc = "Make splits equal size" }) -- make split windows equal width &amp; height
keymap.set("n", "&lt;leader&gt;sx", "&lt;cmd&gt;close&lt;CR&gt;", { desc = "Close current split" }) -- close current split window

keymap.set("n", "&lt;leader&gt;to", "&lt;cmd&gt;tabnew&lt;CR&gt;", { desc = "Open new tab" }) -- open new tab
keymap.set("n", "&lt;leader&gt;tx", "&lt;cmd&gt;tabclose&lt;CR&gt;", { desc = "Close current tab" }) -- close current tab
keymap.set("n", "&lt;leader&gt;tn", "&lt;cmd&gt;tabn&lt;CR&gt;", { desc = "Go to next tab" }) --  go to next tab
keymap.set("n", "&lt;leader&gt;tp", "&lt;cmd&gt;tabp&lt;CR&gt;", { desc = "Go to previous tab" }) --  go to previous tab
keymap.set("n", "&lt;leader&gt;tf", "&lt;cmd&gt;tabnew %&lt;CR&gt;", { desc = "Open current buffer in new tab" }) --  move current buffer to new tab
```

Open the explorer with `:Explore`, open `lua/josean/core/init.lua` and add the following:

```
require("josean.core.options")
require("josean.core.keymaps")
```

Exit with `:q` and reenter Neovim with `nvim .`

## Setup lazy.nvim

Go to “lazy.lua” and add the following to bootstrap lazy.nvim

```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)
```

Then configure lazy.nvim with the following:

```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup("josean.plugins")
```

_If you’re using your name instead of “josean”, change that to your name here as well_

Then open the explorer with `:Explore` and navigate to main `init.lua` file.

Add the following to it:

```
require("josean.core")
require("josean.lazy")
```

Exit with `:q` and reenter Neovim with `nvim`

**You can see the lazy.nvim UI now with `:Lazy` and you can close the UI with `q`**

## Install plenary & vim-tmux-navigator

Do `:e lua/josean/plugins/init.lua`

Add the following to install **plenary** and **vim-tmux-navigator**:

```
return {
  "nvim-lua/plenary.nvim", -- lua functions that many plugins use
  "christoomey/vim-tmux-navigator", -- tmux &amp; split window navigation
}
```

After adding this, save the file and you can install manually by doing `:Lazy`, then typing `I`.

After install, close the UI with `q` and you can manually load a plugin with `:Lazy reload vim-tmux-navigator` for example.

Otherwise, you can also exit with `:q` and reenter Neovim with `nvim .` and it’ll happen automatically.

## Install & configure tokyonight colorscheme

Do `:e lua/josean/plugins/colorscheme.lua`

In this file add the following:

```
return {
  {
    "folke/tokyonight.nvim",
    priority = 1000, -- make sure to load this before all the other start plugins
    config = function()
      local bg = "#011628"
      local bg_dark = "#011423"
      local bg_highlight = "#143652"
      local bg_search = "#0A64AC"
      local bg_visual = "#275378"
      local fg = "#CBE0F0"
      local fg_dark = "#B4D0E9"
      local fg_gutter = "#627E97"
      local border = "#547998"

      require("tokyonight").setup({
        style = "night",
        on_colors = function(colors)
          colors.bg = bg
          colors.bg_dark = bg_dark
          colors.bg_float = bg_dark
          colors.bg_highlight = bg_highlight
          colors.bg_popup = bg_dark
          colors.bg_search = bg_search
          colors.bg_sidebar = bg_dark
          colors.bg_statusline = bg_dark
          colors.bg_visual = bg_visual
          colors.border = border
          colors.fg = fg
          colors.fg_dark = fg_dark
          colors.fg_float = fg
          colors.fg_gutter = fg_gutter
          colors.fg_sidebar = fg_dark
        end,
      })
      -- load the colorscheme here
      vim.cmd([[colorscheme tokyonight]])
    end,
  },
}
```

This will setup **tokyonight** as the colorscheme and modify some of its colors according to my preference.

Exit with `:q` and reenter Neovim with `nvim .`

## Setup nvim-tree file explorer

Do `:e lua/josean/plugins/nvim-tree.lua`

Add the following to this file:

```
return {
  "nvim-tree/nvim-tree.lua",
  dependencies = "nvim-tree/nvim-web-devicons",
  config = function()
    local nvimtree = require("nvim-tree")

    -- recommended settings from nvim-tree documentation
    vim.g.loaded_netrw = 1
    vim.g.loaded_netrwPlugin = 1

    nvimtree.setup({
      view = {
        width = 35,
        relativenumber = true,
      },
      -- change folder arrow icons
      renderer = {
        indent_markers = {
          enable = true,
        },
        icons = {
          glyphs = {
            folder = {
              arrow_closed = "", -- arrow when folder is closed
              arrow_open = "", -- arrow when folder is open
            },
          },
        },
      },
      -- disable window_picker for
      -- explorer to work well with
      -- window splits
      actions = {
        open_file = {
          window_picker = {
            enable = false,
          },
        },
      },
      filters = {
        custom = { ".DS_Store" },
      },
      git = {
        ignore = false,
      },
    })

    -- set keymaps
    local keymap = vim.keymap -- for conciseness

    keymap.set("n", "&lt;leader&gt;ee", "&lt;cmd&gt;NvimTreeToggle&lt;CR&gt;", { desc = "Toggle file explorer" }) -- toggle file explorer
    keymap.set("n", "&lt;leader&gt;ef", "&lt;cmd&gt;NvimTreeFindFileToggle&lt;CR&gt;", { desc = "Toggle file explorer on current file" }) -- toggle file explorer on current file
    keymap.set("n", "&lt;leader&gt;ec", "&lt;cmd&gt;NvimTreeCollapse&lt;CR&gt;", { desc = "Collapse file explorer" }) -- collapse file explorer
    keymap.set("n", "&lt;leader&gt;er", "&lt;cmd&gt;NvimTreeRefresh&lt;CR&gt;", { desc = "Refresh file explorer" }) -- refresh file explorer
  end
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup which-key

Which-key is great for seeing what keymaps you can use.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `which-key.lua`

Add this to the file:

```
return {
  "folke/which-key.nvim",
  event = "VeryLazy",
  init = function()
    vim.o.timeout = true
    vim.o.timeoutlen = 500
  end,
  opts = {
    -- your configuration comes here
    -- or leave it empty to use the default settings
    -- refer to the configuration section below
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup telescope fuzzy finder

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `telescope.lua`

Add this to the file:

```
return {
  "nvim-telescope/telescope.nvim",
  branch = "0.1.x",
  dependencies = {
    "nvim-lua/plenary.nvim",
    { "nvim-telescope/telescope-fzf-native.nvim", build = "make" },
    "nvim-tree/nvim-web-devicons",
  },
  config = function()
    local telescope = require("telescope")
    local actions = require("telescope.actions")

    telescope.setup({
      defaults = {
        path_display = { "smart" },
        mappings = {
          i = {
            ["&lt;C-k&gt;"] = actions.move_selection_previous, -- move to prev result
            ["&lt;C-j&gt;"] = actions.move_selection_next, -- move to next result
            ["&lt;C-q&gt;"] = actions.send_selected_to_qflist + actions.open_qflist,
          },
        },
      },
    })

    telescope.load_extension("fzf")

    -- set keymaps
    local keymap = vim.keymap -- for conciseness

    keymap.set("n", "&lt;leader&gt;ff", "&lt;cmd&gt;Telescope find_files&lt;cr&gt;", { desc = "Fuzzy find files in cwd" })
    keymap.set("n", "&lt;leader&gt;fr", "&lt;cmd&gt;Telescope oldfiles&lt;cr&gt;", { desc = "Fuzzy find recent files" })
    keymap.set("n", "&lt;leader&gt;fs", "&lt;cmd&gt;Telescope live_grep&lt;cr&gt;", { desc = "Find string in cwd" })
    keymap.set("n", "&lt;leader&gt;fc", "&lt;cmd&gt;Telescope grep_string&lt;cr&gt;", { desc = "Find string under cursor in cwd" })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup a greeter

We’re gonna setup a greeter for Neovim startup with alpha-nvim

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `alpha.lua`

Add the following code:

```
return {
  "goolord/alpha-nvim",
  event = "VimEnter",
  config = function()
    local alpha = require("alpha")
    local dashboard = require("alpha.themes.dashboard")

    -- Set header
    dashboard.section.header.val = {
      "                                                     ",
      "  ███╗   ██╗███████╗ ██████╗ ██╗   ██╗██╗███╗   ███╗ ",
      "  ████╗  ██║██╔════╝██╔═══██╗██║   ██║██║████╗ ████║ ",
      "  ██╔██╗ ██║█████╗  ██║   ██║██║   ██║██║██╔████╔██║ ",
      "  ██║╚██╗██║██╔══╝  ██║   ██║╚██╗ ██╔╝██║██║╚██╔╝██║ ",
      "  ██║ ╚████║███████╗╚██████╔╝ ╚████╔╝ ██║██║ ╚═╝ ██║ ",
      "  ╚═╝  ╚═══╝╚══════╝ ╚═════╝   ╚═══╝  ╚═╝╚═╝     ╚═╝ ",
      "                                                     ",
    }

    -- Set menu
    dashboard.section.buttons.val = {
      dashboard.button("e", "  &gt; New File", "&lt;cmd&gt;ene&lt;CR&gt;"),
      dashboard.button("SPC ee", "  &gt; Toggle file explorer", "&lt;cmd&gt;NvimTreeToggle&lt;CR&gt;"),
      dashboard.button("SPC ff", "󰱼 &gt; Find File", "&lt;cmd&gt;Telescope find_files&lt;CR&gt;"),
      dashboard.button("SPC fs", "  &gt; Find Word", "&lt;cmd&gt;Telescope live_grep&lt;CR&gt;"),
      dashboard.button("SPC wr", "󰁯  &gt; Restore Session For Current Directory", "&lt;cmd&gt;SessionRestore&lt;CR&gt;"),
      dashboard.button("q", " &gt; Quit NVIM", "&lt;cmd&gt;qa&lt;CR&gt;"),
    }

    -- Send config to alpha
    alpha.setup(dashboard.opts)

    -- Disable folding on alpha buffer
    vim.cmd([[autocmd FileType alpha setlocal nofoldenable]])
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup automated session manager

Automatic session management is great for auto saving sessions before exiting Neovim and getting back to work when you come back.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `auto-session.lua`

Add the following to this file:

```
return {
  "rmagatti/auto-session",
  config = function()
    local auto_session = require("auto-session")

    auto_session.setup({
      auto_restore_enabled = false,
      auto_session_suppress_dirs = { "~/", "~/Dev/", "~/Downloads", "~/Documents", "~/Desktop/" },
    })

    local keymap = vim.keymap

    keymap.set("n", "&lt;leader&gt;wr", "&lt;cmd&gt;SessionRestore&lt;CR&gt;", { desc = "Restore session for cwd" }) -- restore last workspace session for current directory
    keymap.set("n", "&lt;leader&gt;ws", "&lt;cmd&gt;SessionSave&lt;CR&gt;", { desc = "Save session for auto session root dir" }) -- save workspace session for current working directory
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim .`

When working in a project, you can now close everything with `:qa` and when you open Neovim again in this directory you can use `<leader>wr` to restore your workspace/session.

## Disable lazy.nvim change\_detection notification

Let’s disable the lazy.nvim change\_detection notification which I find a bit annoying.

Navigate to `lazy.lua` and modify the code like so:

```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup("josean.plugins", {
  change_detection = {
    notify = false,
  },
})
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup bufferline for better looking tabs

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `bufferline.lua`

Add the following code:

```
return {
  "akinsho/bufferline.nvim",
  dependencies = { "nvim-tree/nvim-web-devicons" },
  version = "*",
  opts = {
    options = {
      mode = "tabs",
      separator_style = "slant",
    },
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup lualine for a better statusline

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `lualine.lua`

Add the following code:

```
return {
  "nvim-lualine/lualine.nvim",
  dependencies = { "nvim-tree/nvim-web-devicons" },
  config = function()
    local lualine = require("lualine")
    local lazy_status = require("lazy.status") -- to configure lazy pending updates count

    local colors = {
      blue = "#65D1FF",
      green = "#3EFFDC",
      violet = "#FF61EF",
      yellow = "#FFDA7B",
      red = "#FF4A4A",
      fg = "#c3ccdc",
      bg = "#112638",
      inactive_bg = "#2c3043",
    }

    local my_lualine_theme = {
      normal = {
        a = { bg = colors.blue, fg = colors.bg, gui = "bold" },
        b = { bg = colors.bg, fg = colors.fg },
        c = { bg = colors.bg, fg = colors.fg },
      },
      insert = {
        a = { bg = colors.green, fg = colors.bg, gui = "bold" },
        b = { bg = colors.bg, fg = colors.fg },
        c = { bg = colors.bg, fg = colors.fg },
      },
      visual = {
        a = { bg = colors.violet, fg = colors.bg, gui = "bold" },
        b = { bg = colors.bg, fg = colors.fg },
        c = { bg = colors.bg, fg = colors.fg },
      },
      command = {
        a = { bg = colors.yellow, fg = colors.bg, gui = "bold" },
        b = { bg = colors.bg, fg = colors.fg },
        c = { bg = colors.bg, fg = colors.fg },
      },
      replace = {
        a = { bg = colors.red, fg = colors.bg, gui = "bold" },
        b = { bg = colors.bg, fg = colors.fg },
        c = { bg = colors.bg, fg = colors.fg },
      },
      inactive = {
        a = { bg = colors.inactive_bg, fg = colors.semilightgray, gui = "bold" },
        b = { bg = colors.inactive_bg, fg = colors.semilightgray },
        c = { bg = colors.inactive_bg, fg = colors.semilightgray },
      },
    }

    -- configure lualine with modified theme
    lualine.setup({
      options = {
        theme = my_lualine_theme,
      },
      sections = {
        lualine_x = {
          {
            lazy_status.updates,
            cond = lazy_status.has_updates,
            color = { fg = "#ff9e64" },
          },
          { "encoding" },
          { "fileformat" },
          { "filetype" },
        },
      },
    })
  end,
}
```

So that lualine can show pending plugin updates through lazy.nvim, open “lazy.lua” and modify it like so:

```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup("josean.plugins", {
  checker = {
    enabled = true,
    notify = false,
  },
  change_detection = {
    notify = false,
  },
})
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup dressing.nvim

Dressing.nvim improves the ui for `vim.ui.select` and `vim.ui.input`

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `dressing.lua`

Add the following code:

```
return {
  "stevearc/dressing.nvim",
  event = "VeryLazy",
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup vim-maximizer

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `vim-maximizer.lua`

Add the following code:

```
return {
  "szw/vim-maximizer",
  keys = {
    { "&lt;leader&gt;sm", "&lt;cmd&gt;MaximizerToggle&lt;CR&gt;", desc = "Maximize/minimize a split" },
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup treesitter

Treesitter is an awesome Neovim feature that provides better syntax highlighting, indentation, autotagging, incremental selection and many other cool features.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `treesitter.lua`

Add the following code:

```
return {
  "nvim-treesitter/nvim-treesitter",
  event = { "BufReadPre", "BufNewFile" },
  build = ":TSUpdate",
  dependencies = {
    "windwp/nvim-ts-autotag",
  },
  config = function()
    -- import nvim-treesitter plugin
    local treesitter = require("nvim-treesitter.configs")

    -- configure treesitter
    treesitter.setup({ -- enable syntax highlighting
      highlight = {
        enable = true,
      },
      -- enable indentation
      indent = { enable = true },
      -- enable autotagging (w/ nvim-ts-autotag plugin)
      autotag = {
        enable = true,
      },
      -- ensure these language parsers are installed
      ensure_installed = {
        "json",
        "javascript",
        "typescript",
        "tsx",
        "yaml",
        "html",
        "css",
        "prisma",
        "markdown",
        "markdown_inline",
        "svelte",
        "graphql",
        "bash",
        "lua",
        "vim",
        "dockerfile",
        "gitignore",
        "query",
        "vimdoc",
        "c",
      },
      incremental_selection = {
        enable = true,
        keymaps = {
          init_selection = "&lt;C-space&gt;",
          node_incremental = "&lt;C-space&gt;",
          scope_incremental = false,
          node_decremental = "&lt;bs&gt;",
        },
      },
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup indent guides

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `indent-blankline.lua`

Add the following code:

```
return {
  "lukas-reineke/indent-blankline.nvim",
  event = { "BufReadPre", "BufNewFile" },
  main = "ibl",
  opts = {
    indent = { char = "┊" },
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup autocompletion

We’re going to setup completion with “nvim-cmp” to get suggestions as we type.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `nvim-cmp.lua`

Add the following code:

```
return {
  "hrsh7th/nvim-cmp",
  event = "InsertEnter",
  dependencies = {
    "hrsh7th/cmp-buffer", -- source for text in buffer
    "hrsh7th/cmp-path", -- source for file system paths
    {
      "L3MON4D3/LuaSnip",
      -- follow latest release.
      version = "v2.*", -- Replace &lt;CurrentMajor&gt; by the latest released major (first number of latest release)
      -- install jsregexp (optional!).
      build = "make install_jsregexp",
    },
    "saadparwaiz1/cmp_luasnip", -- for autocompletion
    "rafamadriz/friendly-snippets", -- useful snippets
    "onsails/lspkind.nvim", -- vs-code like pictograms
  },
  config = function()
    local cmp = require("cmp")

    local luasnip = require("luasnip")

    local lspkind = require("lspkind")

    -- loads vscode style snippets from installed plugins (e.g. friendly-snippets)
    require("luasnip.loaders.from_vscode").lazy_load()

    cmp.setup({
      completion = {
        completeopt = "menu,menuone,preview,noselect",
      },
      snippet = { -- configure how nvim-cmp interacts with snippet engine
        expand = function(args)
          luasnip.lsp_expand(args.body)
        end,
      },
      mapping = cmp.mapping.preset.insert({
        ["&lt;C-k&gt;"] = cmp.mapping.select_prev_item(), -- previous suggestion
        ["&lt;C-j&gt;"] = cmp.mapping.select_next_item(), -- next suggestion
        ["&lt;C-b&gt;"] = cmp.mapping.scroll_docs(-4),
        ["&lt;C-f&gt;"] = cmp.mapping.scroll_docs(4),
        ["&lt;C-Space&gt;"] = cmp.mapping.complete(), -- show completion suggestions
        ["&lt;C-e&gt;"] = cmp.mapping.abort(), -- close completion window
        ["&lt;CR&gt;"] = cmp.mapping.confirm({ select = false }),
      }),
      -- sources for autocompletion
      sources = cmp.config.sources({
        { name = "luasnip" }, -- snippets
        { name = "buffer" }, -- text within current buffer
        { name = "path" }, -- file system paths
      }),

      -- configure lspkind for vs-code like pictograms in completion menu
      formatting = {
        format = lspkind.cmp_format({
          maxwidth = 50,
          ellipsis_char = "...",
        }),
      },
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup auto closing pairs

This plugin will help us auto close surrounding characters like parens, brackets, curly braces, quotes, single quotes and tags

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `autopairs.lua`

Add the following code:

```
return {
  "windwp/nvim-autopairs",
  event = { "InsertEnter" },
  dependencies = {
    "hrsh7th/nvim-cmp",
  },
  config = function()
    -- import nvim-autopairs
    local autopairs = require("nvim-autopairs")

    -- configure autopairs
    autopairs.setup({
      check_ts = true, -- enable treesitter
      ts_config = {
        lua = { "string" }, -- don't add pairs in lua string treesitter nodes
        javascript = { "template_string" }, -- don't add pairs in javscript template_string treesitter nodes
        java = false, -- don't check treesitter on java
      },
    })

    -- import nvim-autopairs completion functionality
    local cmp_autopairs = require("nvim-autopairs.completion.cmp")

    -- import nvim-cmp plugin (completions plugin)
    local cmp = require("cmp")

    -- make autopairs and completion work together
    cmp.event:on("confirm_done", cmp_autopairs.on_confirm_done())
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup commenting plugin

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `comment.lua`

Add the following code:

```
return {
  "numToStr/Comment.nvim",
  event = { "BufReadPre", "BufNewFile" },
  dependencies = {
    "JoosepAlviste/nvim-ts-context-commentstring",
  },
  config = function()
    -- import comment plugin safely
    local comment = require("Comment")

    local ts_context_commentstring = require("ts_context_commentstring.integrations.comment_nvim")

    -- enable comment
    comment.setup({
      -- for commenting tsx, jsx, svelte, html files
      pre_hook = ts_context_commentstring.create_pre_hook(),
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup todo comments

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `todo-comments.lua`

Add the following code:

```
return {
  "folke/todo-comments.nvim",
  event = { "BufReadPre", "BufNewFile" },
  dependencies = { "nvim-lua/plenary.nvim" },
  config = function()
    local todo_comments = require("todo-comments")

    -- set keymaps
    local keymap = vim.keymap -- for conciseness

    keymap.set("n", "]t", function()
      todo_comments.jump_next()
    end, { desc = "Next todo comment" })

    keymap.set("n", "[t", function()
      todo_comments.jump_prev()
    end, { desc = "Previous todo comment" })

    todo_comments.setup()
  end,
}
```

Look for `telescope.lua` with telescope with `<leader>ff`

Open this file and add the following to be able to look for todos with telescope:

```
return {
  "nvim-telescope/telescope.nvim",
  branch = "0.1.x",
  dependencies = {
    "nvim-lua/plenary.nvim",
    { "nvim-telescope/telescope-fzf-native.nvim", build = "make" },
    "nvim-tree/nvim-web-devicons",
    "folke/todo-comments.nvim",
  },
  config = function()
    local telescope = require("telescope")
    local actions = require("telescope.actions")

    telescope.setup({
      defaults = {
        path_display = { "smart" },
        mappings = {
          i = {
            ["&lt;C-k&gt;"] = actions.move_selection_previous, -- move to prev result
            ["&lt;C-j&gt;"] = actions.move_selection_next, -- move to next result
            ["&lt;C-q&gt;"] = actions.send_selected_to_qflist + actions.open_qflist,
          },
        },
      },
    })

    telescope.load_extension("fzf")

    -- set keymaps
    local keymap = vim.keymap -- for conciseness

    keymap.set("n", "&lt;leader&gt;ff", "&lt;cmd&gt;Telescope find_files&lt;cr&gt;", { desc = "Fuzzy find files in cwd" })
    keymap.set("n", "&lt;leader&gt;fr", "&lt;cmd&gt;Telescope oldfiles&lt;cr&gt;", { desc = "Fuzzy find recent files" })
    keymap.set("n", "&lt;leader&gt;fs", "&lt;cmd&gt;Telescope live_grep&lt;cr&gt;", { desc = "Find string in cwd" })
    keymap.set("n", "&lt;leader&gt;fc", "&lt;cmd&gt;Telescope grep_string&lt;cr&gt;", { desc = "Find string under cursor in cwd" })
    keymap.set("n", "&lt;leader&gt;ft", "&lt;cmd&gt;TodoTelescope&lt;cr&gt;", { desc = "Find todos" })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup substitution plugin

This plugin allows us to use `s` followed by a `motion` to substitute text that was previously copied.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `substitute.lua`

Add the following code:

```
return {
  "gbprod/substitute.nvim",
  event = { "BufReadPre", "BufNewFile" },
  config = function()
    local substitute = require("substitute")

    substitute.setup()

    -- set keymaps
    local keymap = vim.keymap -- for conciseness

    vim.keymap.set("n", "s", substitute.operator, { desc = "Substitute with motion" })
    vim.keymap.set("n", "ss", substitute.line, { desc = "Substitute line" })
    vim.keymap.set("n", "S", substitute.eol, { desc = "Substitute to end of line" })
    vim.keymap.set("x", "s", substitute.visual, { desc = "Substitute in visual mode" })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup nvim-surround

This plugin is great for adding, deleting and modifying surrounding symbols and tags.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `surround.lua`

Add the following code:

```
return {
  "kylechui/nvim-surround",
  event = { "BufReadPre", "BufNewFile" },
  version = "*", -- Use for stability; omit to use `main` branch for the latest features
  config = true,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup LSP

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `lua/josean` add a new directory with `a`, calling it `lsp/`

Navigate to `lazy.lua` and modify it so that `lazy.nvim` knows about the new `lsp` directory like so:

```
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup({ { import = "josean.plugins" }, { import = "josean.plugins.lsp" } }, {
  checker = {
    enabled = true,
    notify = false,
  },
  change_detection = {
    notify = false,
  },
})
```

### Setup mason.nvim

Mason.nvim is used to install and manage all of the language servers that you need for the languages you work for.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins/lsp` add a new file with `a` and call it `mason.lua`

Add the following code:

```
return {
  "williamboman/mason.nvim",
  dependencies = {
    "williamboman/mason-lspconfig.nvim",
  },
  config = function()
    -- import mason
    local mason = require("mason")

    -- import mason-lspconfig
    local mason_lspconfig = require("mason-lspconfig")

    -- enable mason and configure icons
    mason.setup({
      ui = {
        icons = {
          package_installed = "✓",
          package_pending = "➜",
          package_uninstalled = "✗",
        },
      },
    })

    mason_lspconfig.setup({
      -- list of servers for mason to install
      ensure_installed = {
        "tsserver",
        "html",
        "cssls",
        "tailwindcss",
        "svelte",
        "lua_ls",
        "graphql",
        "emmet_ls",
        "prismals",
        "pyright",
      },
    })
  end,
}
```

### Setup nvim-lspconfig

Nvim-lspconfig is used to configure your language servers.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins/lsp` add a new file with `a` and call it `lspconfig.lua`

Add the following code:

```
return {
  "neovim/nvim-lspconfig",
  event = { "BufReadPre", "BufNewFile" },
  dependencies = {
    "hrsh7th/cmp-nvim-lsp",
    { "antosha417/nvim-lsp-file-operations", config = true },
    { "folke/neodev.nvim", opts = {} },
  },
  config = function()
    -- import lspconfig plugin
    local lspconfig = require("lspconfig")

    -- import mason_lspconfig plugin
    local mason_lspconfig = require("mason-lspconfig")

    -- import cmp-nvim-lsp plugin
    local cmp_nvim_lsp = require("cmp_nvim_lsp")

    local keymap = vim.keymap -- for conciseness

    vim.api.nvim_create_autocmd("LspAttach", {
      group = vim.api.nvim_create_augroup("UserLspConfig", {}),
      callback = function(ev)
        -- Buffer local mappings.
        -- See `:help vim.lsp.*` for documentation on any of the below functions
        local opts = { buffer = ev.buf, silent = true }

        -- set keybinds
        opts.desc = "Show LSP references"
        keymap.set("n", "gR", "&lt;cmd&gt;Telescope lsp_references&lt;CR&gt;", opts) -- show definition, references

        opts.desc = "Go to declaration"
        keymap.set("n", "gD", vim.lsp.buf.declaration, opts) -- go to declaration

        opts.desc = "Show LSP definitions"
        keymap.set("n", "gd", "&lt;cmd&gt;Telescope lsp_definitions&lt;CR&gt;", opts) -- show lsp definitions

        opts.desc = "Show LSP implementations"
        keymap.set("n", "gi", "&lt;cmd&gt;Telescope lsp_implementations&lt;CR&gt;", opts) -- show lsp implementations

        opts.desc = "Show LSP type definitions"
        keymap.set("n", "gt", "&lt;cmd&gt;Telescope lsp_type_definitions&lt;CR&gt;", opts) -- show lsp type definitions

        opts.desc = "See available code actions"
        keymap.set({ "n", "v" }, "&lt;leader&gt;ca", vim.lsp.buf.code_action, opts) -- see available code actions, in visual mode will apply to selection

        opts.desc = "Smart rename"
        keymap.set("n", "&lt;leader&gt;rn", vim.lsp.buf.rename, opts) -- smart rename

        opts.desc = "Show buffer diagnostics"
        keymap.set("n", "&lt;leader&gt;D", "&lt;cmd&gt;Telescope diagnostics bufnr=0&lt;CR&gt;", opts) -- show  diagnostics for file

        opts.desc = "Show line diagnostics"
        keymap.set("n", "&lt;leader&gt;d", vim.diagnostic.open_float, opts) -- show diagnostics for line

        opts.desc = "Go to previous diagnostic"
        keymap.set("n", "[d", vim.diagnostic.goto_prev, opts) -- jump to previous diagnostic in buffer

        opts.desc = "Go to next diagnostic"
        keymap.set("n", "]d", vim.diagnostic.goto_next, opts) -- jump to next diagnostic in buffer

        opts.desc = "Show documentation for what is under cursor"
        keymap.set("n", "K", vim.lsp.buf.hover, opts) -- show documentation for what is under cursor

        opts.desc = "Restart LSP"
        keymap.set("n", "&lt;leader&gt;rs", ":LspRestart&lt;CR&gt;", opts) -- mapping to restart lsp if necessary
      end,
    })

    -- used to enable autocompletion (assign to every lsp server config)
    local capabilities = cmp_nvim_lsp.default_capabilities()

    -- Change the Diagnostic symbols in the sign column (gutter)
    -- (not in youtube nvim video)
    local signs = { Error = " ", Warn = " ", Hint = "󰠠 ", Info = " " }
    for type, icon in pairs(signs) do
      local hl = "DiagnosticSign" .. type
      vim.fn.sign_define(hl, { text = icon, texthl = hl, numhl = "" })
    end

    mason_lspconfig.setup_handlers({
      -- default handler for installed servers
      function(server_name)
        lspconfig[server_name].setup({
          capabilities = capabilities,
        })
      end,
      ["svelte"] = function()
        -- configure svelte server
        lspconfig["svelte"].setup({
          capabilities = capabilities,
          on_attach = function(client, bufnr)
            vim.api.nvim_create_autocmd("BufWritePost", {
              pattern = { "*.js", "*.ts" },
              callback = function(ctx)
                -- Here use ctx.match instead of ctx.file
                client.notify("$/onDidChangeTsOrJsFile", { uri = ctx.match })
              end,
            })
          end,
        })
      end,
      ["graphql"] = function()
        -- configure graphql language server
        lspconfig["graphql"].setup({
          capabilities = capabilities,
          filetypes = { "graphql", "gql", "svelte", "typescriptreact", "javascriptreact" },
        })
      end,
      ["emmet_ls"] = function()
        -- configure emmet language server
        lspconfig["emmet_ls"].setup({
          capabilities = capabilities,
          filetypes = { "html", "typescriptreact", "javascriptreact", "css", "sass", "scss", "less", "svelte" },
        })
      end,
      ["lua_ls"] = function()
        -- configure lua server (with special settings)
        lspconfig["lua_ls"].setup({
          capabilities = capabilities,
          settings = {
            Lua = {
              -- make the language server recognize "vim" global
              diagnostics = {
                globals = { "vim" },
              },
              completion = {
                callSnippet = "Replace",
              },
            },
          },
        })
      end,
    })
  end,
}
```

_In the code under `mason_lspconfig.setup_handlers` I setup a default for my language servers and some custom configurations for `svelte`, `graphql`, `emmet_ls`, and `lua_ls`. This can vary depending on the languages that you’re gonna be using._

Navigate to `nvim-cmp.lua` and make the following change to add the lsp as a completion source:

```
return {
  "hrsh7th/nvim-cmp",
  event = "InsertEnter",
  dependencies = {
    "hrsh7th/cmp-buffer", -- source for text in buffer
    "hrsh7th/cmp-path", -- source for file system paths
    {
      "L3MON4D3/LuaSnip",
      -- follow latest release.
      version = "v2.*", -- Replace &lt;CurrentMajor&gt; by the latest released major (first number of latest release)
      -- install jsregexp (optional!).
      build = "make install_jsregexp",
    },
    "saadparwaiz1/cmp_luasnip", -- for autocompletion
    "rafamadriz/friendly-snippets", -- useful snippets
    "onsails/lspkind.nvim", -- vs-code like pictograms
  },
  config = function()
    local cmp = require("cmp")

    local luasnip = require("luasnip")

    local lspkind = require("lspkind")

    -- loads vscode style snippets from installed plugins (e.g. friendly-snippets)
    require("luasnip.loaders.from_vscode").lazy_load()

    cmp.setup({
      completion = {
        completeopt = "menu,menuone,preview,noselect",
      },
      snippet = { -- configure how nvim-cmp interacts with snippet engine
        expand = function(args)
          luasnip.lsp_expand(args.body)
        end,
      },
      mapping = cmp.mapping.preset.insert({
        ["&lt;C-k&gt;"] = cmp.mapping.select_prev_item(), -- previous suggestion
        ["&lt;C-j&gt;"] = cmp.mapping.select_next_item(), -- next suggestion
        ["&lt;C-b&gt;"] = cmp.mapping.scroll_docs(-4),
        ["&lt;C-f&gt;"] = cmp.mapping.scroll_docs(4),
        ["&lt;C-Space&gt;"] = cmp.mapping.complete(), -- show completion suggestions
        ["&lt;C-e&gt;"] = cmp.mapping.abort(), -- close completion window
        ["&lt;CR&gt;"] = cmp.mapping.confirm({ select = false }),
      }),
      -- sources for autocompletion
      sources = cmp.config.sources({
        { name = "nvim_lsp"},
        { name = "luasnip" }, -- snippets
        { name = "buffer" }, -- text within current buffer
        { name = "path" }, -- file system paths
      }),

      -- configure lspkind for vs-code like pictograms in completion menu
      formatting = {
        format = lspkind.cmp_format({
          maxwidth = 50,
          ellipsis_char = "...",
        }),
      },
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup trouble.nvim

This is another plugin that adds some nice functionality for interacting with the lsp and some other things like todo comments.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `trouble.lua`

Add the following code:

```
return {
  "folke/trouble.nvim",
  dependencies = { "nvim-tree/nvim-web-devicons", "folke/todo-comments.nvim" },
  keys = {
    { "&lt;leader&gt;xx", "&lt;cmd&gt;TroubleToggle&lt;CR&gt;", desc = "Open/close trouble list" },
    { "&lt;leader&gt;xw", "&lt;cmd&gt;TroubleToggle workspace_diagnostics&lt;CR&gt;", desc = "Open trouble workspace diagnostics" },
    { "&lt;leader&gt;xd", "&lt;cmd&gt;TroubleToggle document_diagnostics&lt;CR&gt;", desc = "Open trouble document diagnostics" },
    { "&lt;leader&gt;xq", "&lt;cmd&gt;TroubleToggle quickfix&lt;CR&gt;", desc = "Open trouble quickfix list" },
    { "&lt;leader&gt;xl", "&lt;cmd&gt;TroubleToggle loclist&lt;CR&gt;", desc = "Open trouble location list" },
    { "&lt;leader&gt;xt", "&lt;cmd&gt;TodoTrouble&lt;CR&gt;", desc = "Open todos in trouble" },
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup formatting

We’re gonna use `conform.nvim` to setup formatting in Neovim.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `formatting.lua`

Add the following code:

```
return {
  "stevearc/conform.nvim",
  event = { "BufReadPre", "BufNewFile" },
  config = function()
    local conform = require("conform")

    conform.setup({
      formatters_by_ft = {
        javascript = { "prettier" },
        typescript = { "prettier" },
        javascriptreact = { "prettier" },
        typescriptreact = { "prettier" },
        svelte = { "prettier" },
        css = { "prettier" },
        html = { "prettier" },
        json = { "prettier" },
        yaml = { "prettier" },
        markdown = { "prettier" },
        graphql = { "prettier" },
        liquid = { "prettier" },
        lua = { "stylua" },
        python = { "isort", "black" },
      },
      format_on_save = {
        lsp_fallback = true,
        async = false,
        timeout_ms = 1000,
      },
    })

    vim.keymap.set({ "n", "v" }, "&lt;leader&gt;mp", function()
      conform.format({
        lsp_fallback = true,
        async = false,
        timeout_ms = 1000,
      })
    end, { desc = "Format file or range (in visual mode)" })
  end,
}
```

Navigate to `mason.lua` and add the following to auto install formatters:

```
return {
  "williamboman/mason.nvim",
  dependencies = {
    "williamboman/mason-lspconfig.nvim",
    "WhoIsSethDaniel/mason-tool-installer.nvim",
  },
  config = function()
    -- import mason
    local mason = require("mason")

    -- import mason-lspconfig
    local mason_lspconfig = require("mason-lspconfig")

    local mason_tool_installer = require("mason-tool-installer")

    -- enable mason and configure icons
    mason.setup({
      ui = {
        icons = {
          package_installed = "✓",
          package_pending = "➜",
          package_uninstalled = "✗",
        },
      },
    })

    mason_lspconfig.setup({
      -- list of servers for mason to install
      ensure_installed = {
        "tsserver",
        "html",
        "cssls",
        "tailwindcss",
        "svelte",
        "lua_ls",
        "graphql",
        "emmet_ls",
        "prismals",
        "pyright",
      },
    })

    mason_tool_installer.setup({
      ensure_installed = {
        "prettier", -- prettier formatter
        "stylua", -- lua formatter
        "isort", -- python formatter
        "black", -- python formatter
      },
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup linting

We’re gonna be using nvim-lint to setup linting in Neovim.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `linting.lua`

Add the following code:

```
return {
  "mfussenegger/nvim-lint",
  event = { "BufReadPre", "BufNewFile" },
  config = function()
    local lint = require("lint")

    lint.linters_by_ft = {
      javascript = { "eslint_d" },
      typescript = { "eslint_d" },
      javascriptreact = { "eslint_d" },
      typescriptreact = { "eslint_d" },
      svelte = { "eslint_d" },
      python = { "pylint" },
    }

    local lint_augroup = vim.api.nvim_create_augroup("lint", { clear = true })

    vim.api.nvim_create_autocmd({ "BufEnter", "BufWritePost", "InsertLeave" }, {
      group = lint_augroup,
      callback = function()
        lint.try_lint()
      end,
    })

    vim.keymap.set("n", "&lt;leader&gt;l", function()
      lint.try_lint()
    end, { desc = "Trigger linting for current file" })
  end,
}
```

Navigate to `mason.lua` and add the following to auto install linters:

```
return {
  "williamboman/mason.nvim",
  dependencies = {
    "williamboman/mason-lspconfig.nvim",
    "WhoIsSethDaniel/mason-tool-installer.nvim",
  },
  config = function()
    -- import mason
    local mason = require("mason")

    -- import mason-lspconfig
    local mason_lspconfig = require("mason-lspconfig")

    local mason_tool_installer = require("mason-tool-installer")

    -- enable mason and configure icons
    mason.setup({
      ui = {
        icons = {
          package_installed = "✓",
          package_pending = "➜",
          package_uninstalled = "✗",
        },
      },
    })

    mason_lspconfig.setup({
      -- list of servers for mason to install
      ensure_installed = {
        "tsserver",
        "html",
        "cssls",
        "tailwindcss",
        "svelte",
        "lua_ls",
        "graphql",
        "emmet_ls",
        "prismals",
        "pyright",
      },
    })

    mason_tool_installer.setup({
      ensure_installed = {
        "prettier", -- prettier formatter
        "stylua", -- lua formatter
        "isort", -- python formatter
        "black", -- python formatter
        "pylint", -- python linter
        "eslint_d", -- js linter
      },
    })
  end,
}
```

Exit with `:q` and reenter Neovim with `nvim`

## Setup git functionality

### Setup gitsigns plugin

Gitsigns is a great plugin for interacting with git hunks in Neovim.

Open the file explorer with `<leader>ee` (in my config the `<leader>` key is `space`).

Under `plugins` add a new file with `a` and call it `gitsigns.lua`

Add the following code:

```
return {
  "lewis6991/gitsigns.nvim",
  event = { "BufReadPre", "BufNewFile" },
  opts = {
    on_attach = function(bufnr)
      local gs = package.loaded.gitsigns

      local function map(mode, l, r, desc)
        vim.keymap.set(mode, l, r, { buffer = bufnr, desc = desc })
      end

      -- Navigation
      map("n", "]h", gs.next_hunk, "Next Hunk")
      map("n", "[h", gs.prev_hunk, "Prev Hunk")

      -- Actions
      map("n", "&lt;leader&gt;hs", gs.stage_hunk, "Stage hunk")
      map("n", "&lt;leader&gt;hr", gs.reset_hunk, "Reset hunk")
      map("v", "&lt;leader&gt;hs", function()
        gs.stage_hunk({ vim.fn.line("."), vim.fn.line("v") })
      end, "Stage hunk")
      map("v", "&lt;leader&gt;hr", function()
        gs.reset_hunk({ vim.fn.line("."), vim.fn.line("v") })
      end, "Reset hunk")

      map("n", "&lt;leader&gt;hS", gs.stage_buffer, "Stage buffer")
      map("n", "&lt;leader&gt;hR", gs.reset_buffer, "Reset buffer")

      map("n", "&lt;leader&gt;hu", gs.undo_stage_hunk, "Undo stage hunk")

      map("n", "&lt;leader&gt;hp", gs.preview_hunk, "Preview hunk")

      map("n", "&lt;leader&gt;hb", function()
        gs.blame_line({ full = true })
      end, "Blame line")
      map("n", "&lt;leader&gt;hB", gs.toggle_current_line_blame, "Toggle line blame")

      map("n", "&lt;leader&gt;hd", gs.diffthis, "Diff this")
      map("n", "&lt;leader&gt;hD", function()
        gs.diffthis("~")
      end, "Diff this ~")

      -- Text object
      map({ "o", "x" }, "ih", ":&lt;C-U&gt;Gitsigns select_hunk&lt;CR&gt;", "Gitsigns select hunk")
    end,
  },
}
```

Exit with `:q`

### Setup lazygit integration

Make sure you have lazygit installed.

Install with homebrew:

```
brew install jesseduffield/lazygit/lazygit
```

Open Neovim with `nvim .`

Under `plugins` add a new file with `a` and call it `lazygit.lua`

Add the following code:

```
return {
  "kdheepak/lazygit.nvim",
  cmd = {
    "LazyGit",
    "LazyGitConfig",
    "LazyGitCurrentFile",
    "LazyGitFilter",
    "LazyGitFilterCurrentFile",
  },
  -- optional for floating window border decoration
  dependencies = {
    "nvim-lua/plenary.nvim",
  },
  -- setting the keybinding for LazyGit with 'keys' is recommended in
  -- order to load the plugin when the command is run for the first time
  keys = {
    { "&lt;leader&gt;lg", "&lt;cmd&gt;LazyGit&lt;cr&gt;", desc = "Open lazy git" },
  },
}
```

Exit with `:q` and reenter Neovim with `nvim`

## YOU’RE DONE! 🚀
