---
layout: post
title: "Examples of using stow to manage your dotfiles"
excerpt: "Cheatsheet of stow usage"
category: blog
tags:
  - mac
  - linux
  - homebrew
  - stow
published: true
---
This is a quick guide on using stow, a very useful tool if you like to centralise
your dotfile storage.

From the manpage:

    Stow is a tool for managing the installation of multiple software packages in the same 
    run-time directory tree.
    
    The approach used by Stow is to install each package into its own tree, then use 
    symbolic links to make it appear as though the files are installed in the common 
    tree. Administration can be performed in the package's private tree in isolation 
    from clutter from other packages. Stow can then be used to update the symbolic 
    links. The structure of each private tree should reflect the desired structure in 
    the common tree; i.e. (in the typical case) there should be a bin directory 
    containing executables, a man/man1 directory containing section 1 man pages, 
    and so on.

Additionally, one can use stow to symlink dotfiles by grouping them into "packages"
within a specific version-controlled tree. For example, one could have a `.dotfiles`
directory in their homedir, containing the "package" `bash` with the configuration 
file `.bashrc`, and symlink this file to `~/.bashrc` with a simple command.

## Quick Usage

    stow [ options ] package ...
    
Install a package

    stow foobar
    
Uninstall package

    stow -D foobar
    
In our case, the "package" we'll be managing would be the dotfiles we're interested in.


## Main Options

I'll not repeat all of stow's options; you can find those by reading the man page.
However, here are those which are most commonly used:

`-n | --no`
Do not perform any operations that modify the filesystem; merely show what would happen.

`-d dir | --dir=dir`
Set the stow directory to `dir` instead of the current directory.  
This also has the effect of making the default target directory be the parent of `dir`. 

`-t dir | --target=dir`
Set the target directory to `dir` instead of the parent of the stow directory.

`-S | --stow`
Stow the packages that follow this option into the target directory. This is the 
default action and so can be omitted if you are only stowing packages rather than 
performing a mixture of stow/delete/restow actions.

`-v | --verbose [0|1|2|3]`
Increase verboseness. Possible levels are 0,1,2 or 3. Simple setting -v or -verbose
adds 1.

`-D | --delete`
Unstow the packages that follow this option from the target directory rather than installing them.

`-R | --restow`
Restow packages (first unstow, then stow again). This is useful for pruning obsolete symlinks from 
the target tree after updating the software in a package.


## Useful Options

There are also some very useful pattern-based options:

`--ignore=REGEX`
Ignore files ending in this Perl regex.

`--defer=REGEX`
Don't stow files beginning with this Perl regex if the file is already stowed to another package.


## Examples

Let's say we're using a mac and we have a `.dotfiles` directory in our home directory
which looks like the following:

    $ tree -a ~/.dotfiles
    .dotfiles
    ├── git
    │   ├── .gitconfig
    │   └── .gitignore_global
    ├── htop
    │   └── .htoprc
    ├── osx
    │   ├── .inputrc
    │   ├── .osx
    ├── python
    │   ├── .pypirc
    │   ├── .pythonrc.py
    │   └── python.zsh
    ├── tmux
    │   └── .tmux.conf
    └── zsh
        └── .zshrc
        
Generally we'd like to "install" various files in our home directory. Let's take
a look at some common cases
        
### Basic install

    $ stow -d ~/.dotfiles -t ~ -S git
    
The `-S` option can be ignored here if preferred.
    
### Reinstall

    $ stow -d ~/.dotfiles -t ~ -R git
    
### Remove

    $ stow -d ~/.dotfiles -t ~ -D git

### `--ignore`

    $ stow -d ~/.dotfiles -t ~ --ignore="\.zsh$|~$" -S python
