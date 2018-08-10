---
layout: post
title: "Posting Python packages to PyPI"
excerpt: ""
category: blog
tags:
  - packaging
  - python
  - pypi
published: true
---

If you've ever issued a `pip install {foo}` or `easy_install {foo}` on the command line you've probably hit [PyPI](http://pypi.python.org), the Python Package Index. From the official website:

> PyPI — the Python Package Index
> The Python Package Index is a repository of software for the Python programming language.
> Written something cool? Want others to be able to install it with easy_install or pip? Put your code on PyPI. It's a big list of python packages that you absolutely must submit your package to for it to be easily one-line installable.

So, if you *have* written something cool that you want others to be able to install with `easy_install` or `pip`, you'll need to submit your package to PyPI.

Here's how you do it.

***

## Step 1: Create your PyPI account(s)

I've written this guide with the following assumptions:

* The module/library/package that you're submitting is called `mypackage`.
* `mypackage` is hosted on github.

### Create your accounts

...on PyPI Live and also on PyPI Test. You must create an account in order to be able to upload your code.

### Create a .pypirc configuration file

This file holds your information for authenticating with PyPI.

    [distutils] # this tells distutils what package indexes you can push to
    index-servers =
        pypi # the live PyPI
        pypitest # test PyPI

    [pypi] # authentication details for live PyPI
    repository: https://pypi.python.org/pypi
    username: {{your_username}}
    password: {{your_password}}

    [pypitest] # authentication details for test PyPI
    repository: https://testpypi.python.org/pypi
    username: {{your_username}}

This is just to make your life easier, so that when it comes time to upload you don't have to type/remember your username and password. Make sure to put this file in your home folder.

### Prepare your package

Every package on PyPI needs to have a file called setup.py at the root of the directory. If your'e using a markdown-formatted read me file you'll also need a setup.cfg file. Also, you'll want a LICENSE.txt file describing what can be done with your code. So if I've been working on a library called mypackage, my directory structure would look like this:

    root-dir/   # arbitrary working directory name
        setup.py
        setup.cfg
        LICENSE.txt
        README.md
        mypackage/
            __init__.py
            foo.py
            bar.py
            baz.py

Here's a breakdown of what goes in which file:

`setup.py`: This is metadata about your library, and should look something like this:

    from distutils.core import setup
    setup(
      name = 'mypackage',
      packages = ['mypackage'], # this must be the same as the name above
      version = '0.1',
      description = 'A random test lib',
      author = 'Peter Downs',
      author_email = 'peterldowns@gmail.com',
      url = 'https://github.com/peterldowns/mypackage', # use the URL to the github repo
      download_url = 'https://github.com/peterldowns/mypackage/tarball/0.1', # I'll explain this in a second
      keywords = ['testing', 'logging', 'example'], # arbitrary keywords
      classifiers = [],
    )

The `download_url` is a link to a hosted file with your repository's code. Github will host this for you, but only if you create a git tag.

In your repository, type:

    git tag 0.1 -m "Adds a tag so that we can put this on PyPI."

Then, type `git tag` to show a list of tags — you should see `0.1` in the list. `git push --tags origin master` will push your tags to Github. Github creates tarballs for download at https://github.com/{username}/{module_name}/tarball/{tag}.

`setup.cfg`: This tells PyPI where your README file is, and should look like this:

    [metadata]
    description-file = README.md

This is necessary if you're using a markdown README file. At upload time, you may still get some errors about the lack of a readme — don't worry about it. If you don't have to use a markdown README file, I would recommend using reStructuredText (rST) instead.

`LICENSE.txt`: This file will contain whichver license you want your code to have. I tend to use the MIT license.

### Upload your package to PyPI Test

    python setup.py register -r pypitest

This will attempt to register your package against PyPI's test server, just to make sure you've set up everything correctly.

Then:

    python setup.py sdist upload -r pypitest

You should hopefully see no errors, and should now be able to see your library in the test PyPI repository.

### Upload to PyPI Live

Once you've successfully uploaded to PyPI Test, perform the same steps but point to the live PyPI server instead. To register, run:

    python setup.py register -r pypi

Then, run:

    python setup.py sdist upload -r pypi

...and you're done!

Congratulations on successfully publishing your first package!
