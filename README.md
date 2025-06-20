# RLSolver Contest Documentation

To contribute to the documentation, please clone this repo.

Install required packages:
```
pip install sphinx sphinx-autobuild sphinx_rtd_theme
pip install nbsphinx nbsphinx_link
```

Edit in `docgit diff upstream/main -- docs/source/
s/source/`, and then run on local machine:
```
cd docs/source

sphinx-autobuild . ../build --open-browser --port 8000
```

After confirming that the edited content is displayed normally, please commit and push it to the main.
