---
layout: post
title: Google Summer of Code 2018 - Report 2
subtitle: Second coding phase starts!
image: /img/cern-logo-blue.png
gh-repo: ntauth/yampl
gh-badge: [star, fork, follow]
tags: [gsoc]
---
![CERN-HSF](/img/gsoc-cern-hsf.png)

It's been a very intense month of sweating, keybashing, coding and troubleshooting. But that's what a developer's life is all about, isn't it?
I'm now happy to announce I have successfully passed the first evaluation by reaching pretty much all the milestones I was tasked with
fulfilling for this very first phase. Here's a brief rundown of my work in the first coding phase:
- Ported the existing **GNU Autotools** based project to **CMake**
- Configured the project for continuous integration (build + testing) on **Travis CI**
- Created an extensible C-C++ plugin architecture (`DynamicModule`, `PluginArbiter` and `PluginApi`)
- Completely decoupled the core code of **YAMPL** from the IPC backends
- Updated yampl-zmq to use the latest version of **ZeroMQ** + **CppZMQ**

This would not have been possible without the support of my mentors at CERN-HSF and, in particular, to **Vakho**, who has been tirelessly
supporting me with ideas, giving insights and critiques and by constantly staying in touch. This now leads me to the second coding phase
of **GSoC18 @ CERN-HSF**.

The second phase of YAMPL consists in revamping the existing **Python** bindings generation procedure by making it seamlessly integrate
with the **YAMPL** core library build process. This means that **YAMPL** and the bindings should build in one go, effectively making the
whole process easier and far less cumbersome. The existing **Python** bindings rely on [**Cython**](http://cython.org/), "an optimising static compiler 
for both the Python programming language and the extended Cython programming language (based on Pyrex)", that "makes writing C extensions for Python as 
easy as Python itself".

I'm now working on a completely new version of the bindings, this time based on [**PyBind11**](https://github.com/pybind/pybind11), which is an extremely
powerful and versatile "lightweight header-only library that exposes C++ types in Python and vice versa, mainly to create Python bindings of existing C++ code".
I have long wanted to fiddle with this wonderful library and, finally, I've got the opportunity to do it while applying the acquired knowledge on a relevant project.

**OT**: I discovered that **PyBind11** was first designed by Wenzel Jakob, a very talented assistant professor at **EPFL**, and who I got to know (indirectly) by reading
one of the books he contributed to: `Physically Based Rendering: From Theory to Implementation`.

Here's a sneak peek into the current work on the second phase to treat yourself with
![PyBindModule.cpp](/img/yampl_pybind.png)

This is it for now, and there's a lot more work to do. Stay tuned for the upcoming articles!
