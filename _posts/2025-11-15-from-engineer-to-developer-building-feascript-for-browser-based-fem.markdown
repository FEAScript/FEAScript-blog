---
layout: post
title: "From Engineer to Developer: Building FEAScript for Browser-Based FEM"
date: 2025-11-15
categories: [Opinion]
tags: [FEAScript, FEM, Galerkin, Numerical Methods, JavaScript]
mathjax: false
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

_Originally posted on dev.to: [From Engineer to Developer: Building FEAScript for Browser-Based FEM](https://dev.to/nikoscham/from-engineer-to-developer-building-feascript-for-browser-based-fem-3cf6)_

_This is a submission for the [2025 Hacktoberfest Writing Challenge](https://dev.to/t/hacktoberfest): Maintainer Spotlight_

---

## 1. JavaScript is bad, right?

Engineers hate installing software. As a chemical engineer myself, I’ve learned to focus on the practical side of things—how to provide solutions and overcome obstacles. Sure, issues like dependencies, version incompatibilities, or retrieving licenses for proprietary software can be seen as obstacles we should use our skills to overcome. But that’s not usually the main problem. What we really need is to reach our target with as few distractions as possible.

In many cases in my work, I’ve faced challenges such as this:

I wanted to develop a web application for a customer that would solve a system of equations using Finite Element Method, or FEM, (the method I know best). But I wanted to deliver it dependency-free. I didn’t want to tell the customer, “_Hey, here’s the web app, but you’ll need to install this and that._” These people don’t have time for that. I wanted it to be easy for them—and I wanted it to be free (or as low-cost as possible).

So, what was the solution? Have you heard the phrase, “_If you want peace, prepare for war_”? That’s exactly what I did. To avoid dependencies and incompatibilities, I dove deep into programming to build my own library.

Of course, I’m not a freshman in software development—I’ve been coding throughout my PhD (I’ve always had an inclination toward programming). But I mostly worked in “_engineering languages_” like C++ and Fortran. Creating software in these languages is super fast—I know—but it didn’t solve my problem. For this, I needed something notorious, something engineers love to hate: JavaScript!

JavaScript can solve the dependency problem since it runs in the browser, right? But wait a minute—building a Finite Element solver in JavaScript? That’s crazy, right? It’s slow, right? It’s a disaster, right? **Right?**

---

## 2. I choose JavaScript

So, two years ago, I started programming. Initially, I was translating some old Fortran routines I had developed during my PhD into JavaScript. It wasn’t easy (#$!@# 0-based indexing)! But I managed to create a proof of concept—a 2D heat conduction simulation. Still, there was much work to do.

Another thing: JavaScript is a heavily object-oriented language, while Fortran (90, which I was using) is primarily functional. I’m still trying to shake off that functional mindset I inherited from Fortran.

So I have chosen JavaScript, but **not because it's easy**. The road is tough, but I have to go on.

---

## 3. FEAScript

The project has improved a lot since its beginning in 2023—and I’ve improved along with it. I’ve dived into the strange but brilliant world of JavaScript. I’ve taken courses, I’ve read (and read, and read…), and I’m still learning. The journey is just beginning.

So what can FEAScript offer up to now?

Using its API, you can run simulations for heat conduction, front propagation, or even solve a general-form partial differential equation. And you can do all of this directly in your browser (for web apps), in a Node.js environment, or on interactive JavaScript notebooks such as [Scribber](https://scribbler.live/).

You can generate meshes using an in-house mesher (currently for simple cases), or import more advanced meshes created in [Gmsh](https://gmsh.info/doc/texinfo/gmsh.html).

For solving linear systems, FEAScript supports LU decomposition (adapted from [math.js](https://mathjs.org/)) and an in-house Frontal solver. For nonlinear systems, you can use the Newton-Raphson method.

(Many more features are also included. Check the resources if you want to dive deeper - Hint: FEAScript is not as slow as a C++ developer might think, thanks to V8).

And what does it need? It just **needs your help**!

---

## 4. Hacktoberfest

When I tagged my repository for Hacktoberfest, I honestly didn’t believe anyone would want to contribute. Not because I doubted the value of my project, but because Finite Elements is a niche topic. But luckily, reality proved me wrong!

I’d describe these contributors as “_navigator explorers_”—and that’s impressive. They want to contribute even though they might not know much about Finite Elements, or how difficult it can be to understand the whole codebase that’s (hmm) still not ideally written.

I’ve had the honor of receiving contributions from such brave people, and that’s the beauty of open-source: they don’t have to fully understand the entire code. They can build a small piece—something necessary for the rest of the project, yet independent of it.

That’s beautiful to my eyes. **Thank you**

---

## Resources

Wow, thanks for reading this far! So, what’s next?

Want to learn more about the project?  
Visit the [website](https://feascript.com/)

Want to contribute?  
Check out the [repository](https://github.com/FEAScript/FEAScript-core)

Want to support the project?  
Donate via [GitHub sponsors](https://github.com/sponsors/FEAScript) or [Liberapay](https://liberapay.com/FEAScript/donate)
