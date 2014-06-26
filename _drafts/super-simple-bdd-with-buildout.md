I've been doing BDD for years. I've never used Lettuce, or behave, or Cucumber, or in fact any BDD framework. I've never needed to, as I can achieve a similar result with the tools I'm already using: Python and Buildout.

To get started, we add the following additions to our Buildout config:

    [buildout]
    parts =
        ...
        specs

    ...

    [specs]
    recipe =
        pbp.recipe.noserunner
    eggs =
        unittest2
        pbp.recipe.noserunner
        pinocchio
    working-directory =
        ${buildout:directory}
    defaults =
        --where specs
        --exe
        --include ^(it|ensure|must|should|specs?|examples?)
        --include (specs?(.py)?|examples?(.py)?)$
        --with-spec
        --spec-color

As you can see we're using `nose` to aggregate and run our tests, but we're tweaking the way it works and specifying that it should look in a "specs" directory.

The "BDD" magic is in the 2 `--include` lines. Here we tell nose to include files and classes that end with either `spec(s)` or `example(s)`, and tests that start with the BDD keywords: `it`, `ensure`, `must`, and `should`.

However, the real star of the show is Pinocchio. By specifying `--with-spec` and `--spec-color` we get nicely laid-out, colourised test results which you saw in the screenshot at the top of the article.

Here's an example of the sort of spec file we'd create in our project, `./specs/foo_spec.py`:

    try:
        import unittest2 as unittest
    except ImportError:
        import unittest

    from nose.plugins.skip import SkipTest

    from foo import foo

    class FooSpec(unittest.TestCase):
        def it_should_return_true_for_true_values(self):
            raise SkipTest('Not implemented')

        def it_should_return_false_for_false_values(self):
            self.assertFalse(foo())

        def it_should_return_true_for_None_values(self):
            self.assertTrue(foo(None))


The nice thing about this is that we're writing simple unittest classes & methods. We can skip writing the plain-English "feature" files and go straight to writing Python. We're also not using any quirky decorators to tie things together, instead we're following a simple naming convention.

We can also embellish our output with the use of docstrings on the classes and methods -- these will be used in place of the class/function name to give us more control over what we see in the results.

Additionally, there's nothing that could get in the way when using standard nose plugins. So we can add plugins for coverage.
