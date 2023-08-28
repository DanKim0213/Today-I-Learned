# NVIM Settings

1. [Configure NVIM](#configure-nvim)
1. [Install additional plugins](#install-additional-plugins)
1. [Option 1. Plugins for Python](#option-1.-plugins-for-python)
1. [How to clear the last search](#how-to-clear-the-last-search)
1. [Furthermore](#furthermore)

## Configure NVIM

1. Create your own vimrc file using [Vim Bootstrap](https://vim-bootstrap.com/#tagline) 
    - This website helps you to generates a vimrc file based on your preferences.
1. Move your vimrc file (~/Downloads/generate.vim) into ~/.config/nvim/init.vim
    - $XDG\_CONFIG\_HOME means ~/.config. 
1. Execute VIM and it will install plugins automatically
    - vim

## Install additional plugins 

1. Add new plugins into your vimrc file (~/.config/nvim/init.vim)
    - For example, Plug 'iamcco/markdown-preview.nvim', { 'do': 'cd app && yarn install' } " If you have nodejs and yarn
1. Execute :PlugInstall on your nvim

## Option 1. Plugins for Python 

[Flake8](https://flake8.pycqa.org/en/latest/) as a linter, [Black](https://github.com/psf/black) as a Fixer, and [Mypy](https://github.com/python/mypy) as a static type-hinter

#### Enable Black automatically on save?

1. `$ python3 -m pip install black`
1. `$ export PATH="/Users/dankim/Library/Python/3.9/bin/:$PATH" // to enable python modules with pip list -v`
1. init.vim
    ```
    " ale
    let g:ale_linters = { 'python': ['flake8'] }
    let g:ale_fixers = { 'python': ['black'] }
    let g:ale_fix_on_save = 1
    ```

#### WARNING Could not load Python 3

1. According to `:checkhealth provider`, see `:help provider-python`.
2. For Python 3 plugins:
    1. Make sure Python 3.4+ is available in your $PATH.
    2. Install the module (try "python" if "python3" is missing): `$ python3 -m pip install --user --upgrade pynvim`

#### Configure black-compatible flake8

1. `$ python3 -m pip install flake8`
1. Place `.flake8` file under your working directory such as `~/Programming`

    ```
    [flake8]
    max-line-length = 88
    extend-ignore = E203
    ```
1. And then, set your terminal window size to 92 columns and 30 rows. 

#### Enable Mypy automatically

1. `$python3 -m pip install -U mypy`
1. init.vim
    ```
    let b:ale_linters = ['mypy'] 
    ```
## How to Clear the last search

`command C let @/=""` in init.vim according to [Stack Overflow](https://stackoverflow.com/a/657484/13915193)

## Furthermore

- [Line length while using Black](https://black.readthedocs.io/en/stable/the_black_code_style/current_style.html#line-length)
- [VIM Bootstrap](https://github.com/editor-bootstrap/vim-bootstrap#installation)
- [NVIM Commands](https://github.com/editor-bootstrap/vim-bootstrap#commands)

    
