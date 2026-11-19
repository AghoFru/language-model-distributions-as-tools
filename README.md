# Language-Model Distributions as Tools for Computational Linguistics

A cross-task calibration study, with mostly negative results. Frozen LM word
priors help query-likelihood retrieval only against an artificially small
1,000-token background, and do not beat BM25 or collection smoothing. In
Bosnian/Croatian and Indonesian/Malay identification, a from-scratch causal
model beats a matched subword unigram and a simple character n-gram model after
post-hoc dev calibration, but trails GlotLID-M. Most gains elsewhere align
with the LM training objective or are consistent with Hawkins et al. (2020).
The MERLIN German learner-proficiency pilot fits neither group. LM surprisal
lowered CEFR prediction error there, but prior work already links LM
perplexity to CEFR level, so it is not a new finding.

Read the paper:
[Language-Model Distributions as Tools for Computational Linguistics](Language-Model%20Distributions%20as%20Tools%20for%20Computational%20Linguistics.pdf).

## Key numbers

| Comparison | Result |
| --- | --- |
| SciFact nDCG@10, LM hybrid prior with a 1,000-token background | .650 |
| SciFact nDCG@10, BM25 (default k1=1.2, b=0.75) | .663 |
| SciFact nDCG@10, collection Dirichlet | .659 |
| BM25 minus hybrid, paired test | +.013, 95% CI [-.005, .032], not significant |
| FLORES-200 four-way accuracy, raw: causal / unigram / GlotLID-M | 77.94% / 76.24% / 82.19% |
| Same, after post-hoc dev calibration | 81.74% / 79.72% / 86.34% |
| Character 1-5 gram naive Bayes, post hoc, calibrated | 79.27% |

## Limits

- The evidence blocks are separate studies with different models and data.
  No pooled effect is estimated.
- The 1,000-token retrieval background is artificial. BM25 was not tuned,
  while the hybrid and Dirichlet were tuned on development data.
- The language-ID calibration and the character n-gram control were added
  after the raw evaluation. The language-ID models have one training seed.
- Four of the five human-judgment pilots were chosen from a screen of 31
  candidates, and EIFFEL was added beside that screen. The pilots have no
  independent confirmatory split. The DAIS pilot failed its registered
  standalone test and passed only a post-hoc additive test. The MERLIN
  interval rests on only 16 exam-prompt clusters.

## Data and licenses

The paper cites every dataset and model it uses and lists their licenses in
its "Data, Models, and Licenses" section. This repository does not
redistribute dataset text. EIFFEL, MERLIN, and FLORES-200 are CC BY-SA 4.0,
and any derived data must keep that license. NFCorpus is free for academic use
only, and the FiQA question and answer data are for noncommercial use only.

## Build

The repository holds the manuscript source, bibliography, ACL style files, and
rendered PDF. From this directory:

```sh
TEXINPUTS=style: BSTINPUTS=style: BIBINPUTS=.: latexmk -pdf \
  -jobname="Language-Model Distributions as Tools for Computational Linguistics" \
  -outdir=.build -interaction=nonstopmode -halt-on-error distributional_baselines.tex
cp .build/"Language-Model Distributions as Tools for Computational Linguistics.pdf" .
```
