# Build the manuscript

From this directory, run:

```sh
TEXINPUTS=style: BSTINPUTS=style: BIBINPUTS=.: latexmk -pdf \
  -jobname="Language-Model Distributions as Tools for Computational Linguistics" \
  -outdir=.build -interaction=nonstopmode -halt-on-error distributional_baselines.tex
cp .build/"Language-Model Distributions as Tools for Computational Linguistics.pdf" .
```
