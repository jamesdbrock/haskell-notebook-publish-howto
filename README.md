# WIP

# haskell-notebook-publish-howto

How to publish an existing GitHub repository of Haskell code as a Jupyter
notebook on http://mybinder.org .

This repository is also an example of to publish Haskell code as a
Jupyter notebook.

These instructions are a restatement of the instructions from
[Zero-to-Binder](https://the-turing-way.netlify.app/communication/binder/zero-to-binder.html)
and
[Use a Dockerfile for your Binder repository](https://mybinder.readthedocs.io/en/latest/tutorials/dockerfile.html),
specialized for the Jupyter IHaskell language kernel.

The Haskell code must be buildable with [Stack], and the GHC version
and Stack resolver from the base
[__ihaskell-notebook__](https://github.com/IHaskell/ihaskell-notebook)
image.


1. Create a `Dockerfile` at the top level of your repository.
   Choose from a version of
   [__ihaskell-notebook__](https://github.com/IHaskell/ihaskell-notebook/pkgs/container/ihaskell-notebook/49300728?tag=master)
   for the base image.

   #### `Dockerfile`

   ```
   FROM ghcr.io/ihaskell/ihaskell-notebook:master@sha256:7105b6519a07515babc254b7d3582f7e631149bc9b8ae5f2df0a215d4143cec6

   # USER root
   COPY stack.yaml /home/$NB_USER/stack.yaml
   COPY package.yaml /home/$NB_USER/package.yaml
   COPY LICENSE /home/$NB_USER/LICENSE
   COPY src /home/$NB_USER/src
   # USER $NB_UID
   RUN cd /home/$NB_USER && stack build

   ENV JUPYTER_ENABLE_LAB=yes
   ```

   In the Dockerfile, `stack build dep1 dep2`?
