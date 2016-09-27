---
layout: post
title: Subword movement in ZSH
excerpt: "Handy tip for ZSH users coming from Emacs"
category: tip
tags:
  - zsh
  - emacs
---
Working on the terminal, we often have a keybindings for things like `forward-word` and `backward-word`;
moving the cursor back and forth between "words" delimited by whitespace. If you work in emacs like I do, 
you might be used to "words" being delimited by non-letter characters, and therefore get a little frustrated
by the default behavior.

For example, if we had the following line in our shell (cursor denoted by `|`):

    $ cd /usr/local/bin|
    
My `backward-word` and `forward-word` keybindings are set to `Alt-Left` and `Alt-Right` respectively. I
would expect, then, to hit `Alt-Left` and land 3 characters back, before the last `/`:

    $ cd /usr/local/|bin
    
However, what actually happens is that I jump to the previous whitespace point:

    $ cd |/usr/local/bin
    
To allow modification of this behaviour, we can edit the `WORDCHARS` variable in our ZSH config. By default,
it is set to:

    WORDCHARS='*?_-.[]~=/&;!#$%^(){}<>'
    
If I remove `_`, `-`, and `/`, I get the behavior I was expecting, which makes working with paths and files
in the terminal so much easier!
