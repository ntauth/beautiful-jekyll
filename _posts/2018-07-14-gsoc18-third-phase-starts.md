---
layout: post
title: Google Summer of Code 2018 - Report 3
subtitle: Third coding phase starts!
image: /img/cern-logo-blue.png
gh-repo: ntauth/yampl
gh-badge: [star, fork, follow]
tags: [gsoc]
---
![CERN-HSF](/img/gsoc-cern-hsf.png)

And here I'm back with the latest updates on **GSoC 18 @ CERN-HSF** after 24 days of silence. I'm proud to announce
I have successfully passed the 2nd evaluation. This required the fulfillment of a few objectives I briefly discussed
about in the last blog post:
- Developing a new procedure for the generation of Python bindings for YAMPL that allows for a seamless integration
with the core code of YAMPL. This allows to build the YAMPL library and its Python bindings in one go.
- Porting the existing `Cython` bindings to C++-based `PyBind11` bindings.
- Porting the bindings preserving the internal structures and interfaces, effectively ensuring backwards compatibility
with existing code consuming the Python bindings.
