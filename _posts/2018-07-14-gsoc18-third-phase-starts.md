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

This phase proved to be trickier than expected and the new bindings required extensive testing and profiling in order to
detect hidden flaws, memory leaks (yes **Py_XINCREF/XDECREF**, I'm glaring at you) due to Python garbage collection and performance
bottlenecks (fixed thanks to `Valgrind`).

In order to test how the bindings performed, I developed a Python benchmark that
tests all the possible implementations (Shared Memory, Named Pipe and ZeroMQ) and contexts (Thread, Local and Distributed). The
benchmark works as expected except for the `THREAD` context: this requires the execution of multiple parallel threads which
communicate by exchanging messages, however this was no easy feat due to Python's `Global Interpreter Lock (GIL)`.

Here's a picture of the final result
![Python Bindings Test](/img/yampl_pybind_test.png)

The client is sending a dataset to the server using a named pipe in a local context. There's a marshaling/unmarshaling process 
in between that allows for Python objects to be relayed to the other peer transparently. The bindings also support raw data
exchange by using the `*_raw` variants of `send` and `recv`.

All in all, I'm proud of the end result. But let us now talk about the third and last phase of this exceptional experience. The third phase will officially close on August 6, so there are roughly 2 weeks and a half. After discussing with my mentor, Vakho, and since the I've already fulfilled the required tasks for the project, we have decided that the last few remaining things to do would be the following:
- Polishing the code (removing dead code, documenting, etc.)
- Fixing some gnarly issues on Ubuntu (partly fixed already)

As for the Ubuntu issues, I discovered that the issue is related to the buffer size of named pipes on Linux. `YAMPL` needs to change the buffer size to 1048576 bytes (possible kernel versions >= 2.6.35) but there are two main complications:
- The new buffer size must not exceed the one reported in `/proc/sys/fs/pipe-max-size`
- If the new buffer size does exceed the one in `/proc/sys/fs/pipe-max-size`, the user must be root or the process must have the `CAP_SYS_RESOURCE` capability in order to successfully change the size.

If none of those two requirements hold, the request to change the buffer size returns `EPERM`, in which case `YAMPL` would just throw an exception. This turned out to be an issue not strictly related to Ubuntu, but rather it is related to the policies of each Linux distributions and many other parameters. The issue has now been fixed by silencing the exception and letting the program continue with the original buffer size.

This is pretty much it for this blog post. A final wrap-up post will follow on the next weeks, so stay tuned!
