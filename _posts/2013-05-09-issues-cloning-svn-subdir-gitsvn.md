---
layout: post
title: Can't clone svn subdirectory using git-svn?
tags:
  - git
  - svn
  - development
---
If you're having trouble cloning from an SVN subdirerctory when using `git svn` and you're seeing errors like:

    W: Ignoring error from SVN, path probably does not exist: (160013):
    Filesystem has no item: '/path/to/subdir' path not found
    W: Do not be alarmed at the above message git-svn is just searching
    aggressively for old history.

Try using this format:

    git svn clone --revision 12345:HEAD --no-minimize-url {YourRepositoryPath} {LocalRepoDirectory}

The key thing is to make sure you're using the latest revision number **for the directory you're cloning**.

Feel free to add options like `--stdlayout` if you need them.
