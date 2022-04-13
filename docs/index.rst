
Sphinx Documentation building and publishing to GitHub Pages with GitHub Actions
================================================================================

You have a Python (or other) project that is documented with 
`Sphinx <https://www.sphinx-doc.org/en/master/index.html>`_
and you want to automatically build, deploy and publish that documentation
with `GitHub Actions <https://docs.github.com/en/actions>`_
and `GitHub Pages <https://docs.github.com/en/pages>`_.


Using third party GitHub Actions
--------------------------------

While the `GitHub Actions MarketPlace <https://github.com/marketplace?type=actions>`_
contains a lot of potential pieces for that puzzle,
it can be quite daunting to **find the right actions** for your use case.
Moreover, you might have **security concerns** about automatically running
third party code from some random GitHub user 
in a background context with certain write or push permissions on your repository.


Do it yourself
--------------

If you use such third party GitHub Actions, you typically introduce a dependency
on tens or hundred lines of third party code, 
while you actually **just need a handful of commands**
to achieve the same result.


Template
~~~~~~~~

This is a minimal template of a GitHub Actions YAML definition
that only uses official GitHub actions and a bunch of ``git`` commands:


.. literalinclude:: ../.github/workflows/sphinx2ghpages.yml
    :language: YAML


Tweaking
~~~~~~~~

Things you might want to change or tweak:

-   Is your main branch called something else than ``main``? 
    Change the ``on: push: branches`` list.
-   Install the dependencies of your package with an extra line like 
    ``python -m pip install .`` or ``python -m pip install -r requirements.txt``
    under "Install dependencies and Sphinx"
-   Use the desired source and target folders of your documentation. 
    In this template the documentation is assumed to be under ``docs``
    and the output HTML goes to ``build``.
    Note that your project's source and target folders can be a bit more complex, e.g.
    ``docs/sources`` and ``docs/build/html`` respectively.
-   Change user name, email or message for the commit on ``gh-pages`` branch



.. warning:: This approach **overwrites and removes**
    any existing content and history on your gh-pages branch. 

    In most cases this is ok or even desired. 
    The generated HTML is just a derivative of
    your documentation's source under ``docs`` (which is left untouched)
    and doing full version control of that generated HTML
    is usually overkill.

    Also see `ghp-import's behavior <https://github.com/c-w/ghp-import#big-fat-warning>`_



.. raw:: html

    <style>#forkongithub a{background:#472;color:#fff;text-decoration:none;font-family:arial,sans-serif;text-align:center;font-weight:bold;padding:5px 40px;font-size:1rem;line-height:2rem;position:relative;transition:0.5s;}#forkongithub a:hover{background:#681;color:#fff;}#forkongithub a::before,#forkongithub a::after{content:"";width:100%;display:block;position:absolute;top:1px;left:0;height:1px;background:#efc;}#forkongithub a::after{bottom:1px;top:auto;}@media screen and (min-width:800px){#forkongithub{position:fixed;display:block;top:0;right:0;width:200px;overflow:hidden;height:200px;z-index:9999;}#forkongithub a{width:200px;position:absolute;top:60px;right:-60px;transform:rotate(45deg);-webkit-transform:rotate(45deg);-ms-transform:rotate(45deg);-moz-transform:rotate(45deg);-o-transform:rotate(45deg);box-shadow:4px 4px 10px rgba(0,0,0,0.8);}}</style>
    <span id="forkongithub"><a href="https://github.com/soxofaan/github-actions-sphinx2ghpages/blob/main/.github/workflows/sphinx2ghpages.yml">Fork me on GitHub</a></span>


