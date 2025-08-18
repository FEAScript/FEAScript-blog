---
layout: post
title: "JavaScript for Scientific Computations: Oxymoron or a Real Possibility?"
date: 2025-04-04
categories: [Opinion]
tags: [FEAScript, FEM, Galerkin, Numerical Methods, JavaScript]
---

## A Heretical Statement

Scientific computing has long been the domain of performance-heavy languages like C++ and Fortran. More recently, Python has gained traction, particularly in statistical analysis and machine learning. Yet, when it comes to computationally demanding tasks like finite element analysis (FEM), C++ and Fortran remain the standard.

But what if JavaScript—a language originally designed for web development—could challenge this norm? At first glance, the idea sounds almost heretical. Can JavaScript truly handle scientific computing? Let's break it down from the ground up.

---

## Speed

In order to evaluate JavaScript's speed compared to C++ (which is widely accepted as a very fast language for scientific computations), we can reference the work of Franziska Hinkelmann (Engineering Manager at Google) [^1]. According to her measurements, JavaScript is almost as fast as C++ for tasks like prime number calculation. This performance can be obtained by utilizing the TurboFan optimization feature of Google's V8 JavaScript engine. Similar comparisons by Momtchil Momtchev [^2] show that JavaScript, optimized by TurboFan, can achieve performance close to C++ for tasks like matrix operations.

---

## Libraries

We cannot deny that JavaScript lacks the extensive scientific ecosystem of C++ or Fortran. However, several libraries have emerged in recent years that bring serious numerical capabilities to the JavaScript world:

- **[math.js](https://mathjs.org/)**: A comprehensive math library supporting a wide range of mathematical operations, including matrix calculations and symbolic math.
- **[ndarray](https://github.com/scijs/ndarray)** and **[scijs](https://github.com/scijs)** ecosystem: A collection of libraries focused on multidimensional arrays and scientific computing.
- **[numbers.js](https://github.com/numbers/numbers.js)**: A library for basic numerical methods, such as root finding and integration.
- **[Scribbler](https://scribbler.live/)**: A notebook tool with several preloaded scientific libraries.
- **[FEAScript](https://feascript.com/)**: The finite element simulation library that we are developing, with a focus on simplicity and zero-install usage.

---

## WebAssembly (Wasm) Considerations

While WebAssembly (Wasm) offers tremendous potential for accelerating browser-based numerical computation, it comes with caveats. As of today, no major FEA library has been successfully compiled to WebAssembly with full functionality. Compiling complex software like CalculiX is theoretically possible but brings numerous challenges: handling extensive C/C++ dependencies, dealing with file I/O in a sandboxed environment, and working around limitations in threading and hardware acceleration.

On the other hand, pure JavaScript libraries offer a simpler, native solution for scientific computations that run entirely in the browser without compilation. Of course, a potential enhancement down the line might be integrating WebAssembly _selectively_ for the more performance-critical parts. But that’s for the future.

---

## Conclusions

So, is JavaScript for scientific computing an oxymoron? Maybe not. While it may never dethrone C++ or Fortran in heavy-duty HPC environments, JavaScript is evolving. Thanks to modern engines like V8 and a growing ecosystem of numerical libraries, it's now possible to perform non-trivial scientific computations with reasonable performance.

The future might not belong to JavaScript alone, but it certainly has a place at the scientific computing table!

---

## References

[^1]: F. Hinkelmann. "Speed up Your Node.js App with Native Addons." [https://www.fhinkel.rocks/posts/Speed-up-Your-Node-js-App-with-Native-Addons](https://www.fhinkel.rocks/posts/Speed-up-Your-Node-js-App-with-Native-Addons), 2017.
[^2]: M. Momtchev. "In 2021, is there still a huge performance difference between JavaScript and C++ for CPU-bound?" [https://mmomtchev.medium.com/in-2021-is-there-still-a-huge-performance-difference-between-javascript-and-c-for-cpu-bound-8ff798d999d6](https://mmomtchev.medium.com/in-2021-is-there-still-a-huge-performance-difference-between-javascript-and-c-for-cpu-bound-8ff798d999d6), 2021.
