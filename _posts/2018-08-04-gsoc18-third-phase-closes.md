---
layout: post
title: Google Summer of Code 2018 - Report 4
subtitle: Wrap-up
image: /img/cern-logo-blue.png
gh-repo: ntauth/yampl
gh-badge: [star, fork, follow]
tags: [gsoc]
---
![CERN-HSF](/img/gsoc-cern-hsf.png)

# Wrap-up
This year's edition of **GSoC @ CERN-HSF** has nearly come to an end, and what an end! These past 3 months have been incredibly exciting and
packed with moments of joy, finals stress and, eventually, even more joy. Having been given such a precious opportunity means a lot to me
and I can't thank both **Google** and the people at **CERN-HSF** (Vakho in particular) enough for all this.

I dedicated countless hours to **YAMPL**, learned so much and had a lot of fun implementing the plugin architecture: hours well spent all in
all. I don't have any regrets and I'm absolutely glad and proud to have contributed to such an important project; YAMPL (Yet Another
Message Passing Library) is the IPC library used at **CERN** in the **ATLAS** experiment. Improving it was a priceless experience and I can't
wait to see what the people at CERN think of this modular, revisited, modern YAMPL.

The final evaluations are at the doorstep and start on August 6th. This post is meant to be a wrap-up breakdown of everything I've done in
these last 3 months as part of project `Modular YAMPL`. This is supposed to be the last of the series:
- [Report 1 - First coding phase starts](/2018-05-16-gsoc18-coding-phase-starts/)
- [Report 2 - Second coding phase starts](/2018-06-20-gsoc18-second-phase-starts/)
- [Report 3 - Third coding phase starts](/2018-07-14-gsoc18-third-phase-starts/)

# Milestones
The objectives of the project can be subdivided in multiple milestones, all of which have been successfully fulfilled:
- Ported the existing C++03 **GNU Autotools** based project to C++14 + **CMake**
- Configured the project for continuous integration (build + testing) on **Travis CI**
- Created an extensible C-C++ plugin architecture (`DynamicModule`, `PluginArbiter` and `PluginApi`)
- Completely decoupled the core code of YAMPL from the IPC backends
- Updated `yampl-zmq` to use the latest version of **ZeroMQ** + **CppZMQ**
- Developed a new procedure for the generation of **Python** bindings for YAMPL that allows for a seamless integration with the core code 
of YAMPL. This allows to build the YAMPL library and its Python bindings in one go.
- Ported the existing **Cython** bindings to C++-based **PyBind11** bindings.
- Ported the bindings preserving the internal structures and interfaces, effectively ensuring backwards compatibility with existing 
code consuming the Python bindings.

These are some of the technologies that were used for the improvement of YAMPL
<table>
<tr>
<td><img src="/img/2018-08-04-gsoc18-third-phase-closes/travis-ci-card.png" alt="travis-ci" width="250px"/></td>
<td><img src="/img/2018-08-04-gsoc18-third-phase-closes/docker-logo.png" alt="docker" width="250px"/></td>
<td><img src="/img/2018-08-04-gsoc18-third-phase-closes/pybind11-logo.png" alt="pybind11" width="250px"/></td>
<td><img src="/img/2018-08-04-gsoc18-third-phase-closes/python-logo.png" alt="python" width="250px"/></td>
<td><img src="/img/2018-08-04-gsoc18-third-phase-closes/cmake-logo.png" alt="cmake" width="250px"/></td>
</tr>
</table>

**Travis CI** has been instrumental in speeding up the testing and continuous integration of YAMPL, which required ensuring that the code
and tests work on **CentOS 7** and CERN's **Scientific Linux 6**. This is exactly where **Docker** comes in handy: I set up two .Dockerfile's
used by Travis to run the **CMake** build on two different machines (**centos7** and **slc6-base**).
**CMake** has enabled me to better organize the project and manage the various dependencies of YAMPL. And, last, **Pybind11** is an exceptional
library I have used to develop C++14-Python bindings of **libyampl**.

# Closing remarks
All in all, my [contribution](https://github.com/ntauth/yampl/graphs/contributors) has consisted in 300 commits, with peak activity happening in 
the first phase of the project. The changes have resulted in a complete overhaul of the library architecture (lean, modular and extensible) and this
is exactly the initial goal of `Modular YAMPL`. I'm very happy of the end result and I'm more than sure that YAMPL still has room for further
improvements.

This was my first ever attempt at **Google Summer of Code**: I'm 100% satisfacted and I hope I'll have the chance to participate next year too.
