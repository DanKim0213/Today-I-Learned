# How do I configure NvChad

A few days ago, I couldn't write codes on Vs code once it was updated. In fact, Vs code worked fine but Vim didn't work. Though I knew Vim would work as it did soon, I couldn't wait and this malfunction would happen again whenever Vs code was up to date.

Therefore, I make my mind to switch to NvChad for my daily IDE. It is because I am used to VIM and I feel comfortible on working within terminal. However, there are a several steps to configure NvChad for IDE.

## Prerequisite

Install Iterm2 (for true colors)

> brew install --cask iterm2

Install Neovim

> brew install neovim

Install Nerd Font (for icons)

> brew tap homebrew/cask-fonts && brew install --cask font-jetbrains-mono-nerd-font

Set the font in `Text` settings.

Delete old neovim folders (or backup)

> mv ~/.config/nvim ~/.config/nvim.bak

## Usage

I personally use nvim for web programming in JS and solving algorithms in Python.

For the purpose, I need to install plugins using Lazy.nvim (a package manager), which is built in NvChad, and install lsp, linters, and formatters using Mason.nvim (a lsp+linter+formatter manager), which is also built in NvChad.

Plugins for Language Server Protocol using Mason.nvim:

- "eslint-lsp",
- "prettierd",
- "tailwindcss-language-server",
- "typescript-language-server",
- "pyright",
- "black",
- "pylint",

Plugins for IDE using Lazy.nvim:

- "nvimtools/none-ls.nvim"
- "nvim-treesitter/nvim-treesitter",
- "windwp/nvim-ts-autotag",

Before I move on, I need to install NvChad, according to [the doc](https://nvchad.com/docs/quickstart/install):

1. Install NvChad using Git repository
2. Go to nvim folder `cd ~/.config/nvim`
3. Delete the `.git` folder from nvim folder
4. Enter nvim in the current folder `nvim`
5. Run `:MasonInstallAll`
6. Update the package manager `:Lazy sync`

And then, the bellow config files will help to configure plugins :)

```
-- lua/plugins/init.lua
return {
  {
    "stevearc/conform.nvim",
    -- event = 'BufWritePre', -- uncomment for format on save
    config = function()
      require "configs.conform"
    end,
  },
  {
    "nvimtools/none-ls.nvim",
    event = "VeryLazy",
    opts = function ()
      return require "configs.null-ls"
    end
  },
  {
    "neovim/nvim-lspconfig",
    config = function ()
      require("nvchad.configs.lspconfig").defaults()
      require "configs.lspconfig"
    end
  },
  {
    "williamboman/mason.nvim",
    opts = {
      ensure_installed = {
        "eslint-lsp",
        "prettierd",
        "tailwindcss-language-server",
        "typescript-language-server",

        -- python
        "pyright",
        "black",
        "pylint",
      },
    },
  },
  {
    "nvim-treesitter/nvim-treesitter",
    opts = {
      ensure_installed = {
        -- defaults
        "vim",
        "lua",
        "vimdoc",

        -- web dev
        "html",
        "css",
        "javascript",
        "typescript",
        "tsx",
      },
    },
  },
  {
    "windwp/nvim-ts-autotag",
    dependencies = "nvim-treesitter/nvim-treesitter",
    config = function ()
      require('nvim-ts-autotag').setup()
    end,
    lazy = true,
    event = "VeryLazy"
  },
}

```

```
-- lua/configs/lspconfig.lua
local on_attach = require("nvchad.configs.lspconfig").on_attach
local on_init = require("nvchad.configs.lspconfig").on_init
local capabilities = require("nvchad.configs.lspconfig").capabilities

local lspconfig = require "lspconfig"
local servers = { "html", "cssls", "tsserver", "tailwindcss", "eslint", "cssls", "pyright" }

-- local servers = { "tsserver", "tailwindcss", "eslint", "cssls", "pyright" }
--
-- lsps with default config
for _, lsp in ipairs(servers) do
  lspconfig[lsp].setup {
    on_attach = on_attach,
    on_init = on_init,
    capabilities = capabilities,
  }
end
```

```
-- lua/configs/null-ls.lua
local augroup = vim.api.nvim_create_augroup("LspFormatting", {})
local null_ls = require("null-ls")

local opts = {
  sources = {
    null_ls.builtins.formatting.prettierd,
    null_ls.builtins.diagnostics.pylint,
    null_ls.builtins.formatting.black,
  },
  on_attach = function (client, bufnr)
    if client.supports_method("textDocument/formatting") then
      vim.api.nvim_clear_autocmds({
        group = augroup,
        buffer = bufnr,
      })
      vim.api.nvim_create_autocmd("BufWritePre", {
        group = augroup,
        buffer = bufnr,
        callback = function ()
          vim.lsp.buf.format({ bufnr = bufnr })
        end
      })
    end
  end
}
return opts

```

Once all set up, restart nvim and run `:MasonInstallAll` again.

Done.

## Misc

### Relative Number

You can set nvim to show relative numbers: `:set relativenumber`.
(or attach `vim.wo.relativenumber = true` onto `nvim/init.lua`)

### Option key is not working on Iterm2

You must set disable Option Input Symbol on iTerm2 config.

```
Preferences -> Profiles -> Keys -> Left Option key -> Esc+
```

[Check this issue](https://github.com/NvChad/NvChad/issues/897#issuecomment-1081693338)

### Prettierd is not working right away

It is because prettierd is a kind of demon. Therefore, log out and in of your computer.

### Useful plugins

There are bunch of useful plugins that helps you for web development:

- the builtin [NvChad/nvim-colorizer](https://github.com/NvChad/nvim-colorizer.lua)
- [tailwindcss-colorizer-cmp](https://github.com/roobert/tailwindcss-colorizer-cmp.nvim?tab=readme-ov-file)

## References

- [NvChad](https://nvchad.com/docs/quickstart/install)
- [NvChad Cheatsheet](https://nvchad.com/docs/features/#nvcheatsheet)
- [Lazy.nvim](http://www.lazyvim.org)
- [Mason.nvim](https://github.com/williamboman/mason.nvim)
- [Auto-tag not working](https://github.com/windwp/nvim-ts-autotag/issues/64#issuecomment-1509722026)
- [The perfect Neovim setup for Next.js (it's back)](https://www.youtube.com/watch?v=8um8OYwvz3c)
