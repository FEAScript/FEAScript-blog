---
layout: post
title: "The Eikonal Equation: Implementation with FEAScript"
date: 2025-06-15
categories: [Tutorial]
tags: [FEAScript, FEM, Galerkin, Numerical Methods, JavaScript]
mathjax: true
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

## Introduction to the Eikonal Equation

The eikonal equation is a nonlinear first-order partial differential equation (PDE) that describes how wavefronts propagate through a medium. Its origins go back to the 19th century, when Sir William Rowan Hamilton developed a new framework for geometrical optics. Hamilton introduced the concept of a <i>point characteristic function</i>[^1] which represents the optical path length of a ray between two points on chosen surfaces. These functions are direct precursors to what would later be termed as eikonal by Ernst Heinrich Bruns (1895). Today, the eikonal equation is recognized as a fundamental tool for analyzing wave propagation in diverse cases, from optics and acoustics to seismology and materials science.

---

## Mathematical Formulation

The standard form of the eikonal equation is[^2]:

$$|\nabla u(\mathbf{x})| = f(\mathbf{x}), \quad \mathbf{x} \in \Omega \subset \mathbb{R}^n$$

where \\(u(\mathbf{x})\\) is the travel time or distance from a source, and \\(f(\mathbf{x})\\) represents the slowness field, i.e., the reciprocal of the local wave speed. The eikonal equation's nonlinearity, originating from the absolute value of the gradient, makes it intrinsically challenging to solve analytically. A more significant challenge, however, arises from the potential for solutions to exhibit non-differentiability at certain points[^3]. At these specific points, the classical definition of a derivative breaks down, rendering traditional analytical methods insufficient. It is crucial to recognize that these singularities are not merely numerical artifacts or errors introduced by computational approximations; rather, they are intrinsic features of the wave propagation phenomena that the eikonal equation is designed to describe. Consequently, standard numerical methods that are typically designed for smooth solutions would either fail to converge or produce incorrect and unphysical results in the presence of such inherent non-differentiability.

Among the different methods for solving the eikonal equation (e.g. <i>Fast Marching Method</i>, <i>Fast Sweeping Method</i>), in FEAScript we focus on the <i>Vanishing Viscosity Method</i>[^4]. This method modifies the PDE as:

$$|\nabla u(\mathbf{x})| = f(\mathbf{x}) + \varepsilon \Delta u(\mathbf{x}), \quad \varepsilon > 0$$

where the small parameter \\(\varepsilon\\) enforces smoothness. As \\(\varepsilon \to 0\\), the solution converges to the true viscosity solution of the eikonal equation. This approach blends naturally with finite element and Galerkin formulations, making it ideal for integration into FEAScript.

---

## Implementation with FEAScript

As a demonstration, consider the [solidification front propagation example](https://feascript.com/tutorials/SolidificationFront2D.html). Here, the eikonal equation governs the motion of a solidification interface during processes such as metal cooling. The interface propagates with a speed determined by the material properties (described by the slowness field \\(f(\mathbf{x})\\)). By solving the eikonal equation numerically with vanishing viscosity in FEAScript, we can visualize how the interface evolves over time.

This example highlights how a seemingly abstract PDE translates directly into a materials science application, showing FEAScript's versatility for modeling complex physical processes in JavaScript.

---

## Conclusion

The eikonal equation provides a unifying framework for understanding wavefront propagation across physics and engineering: from geometrical optics (Hamilton's original motivation), to seismology, acoustics, and solidification dynamics.  

Eikonal's nonlinear nature and its inherent presence of singularities make, however, closed-form analytical solutions rare and numerical treatment challenging. Through the <i>Vanishing Viscosity Method</i> implemented in FEAScript, we gain a robust way to approximate viscosity solutions of the eikonal equation in a JavaScript environment. This demonstrates how modern numerical methods can be embedded directly in accessible, browser-based platforms, lowering the barrier to experimenting with PDEs that once required specialized scientific computing software.

---

## References

[^1]: J. Rubinstein, G. Wolansky. "Eikonal functions: Old and new." A Celebration of Mathematical Modeling: The Joseph B. Keller Anniversary Volume, Springer Netherlands, Dordrecht, 2004.
[^2]: J. A. Sethian. "A fast marching level set method for monotonically advancing fronts." Proceedings of the National Academy of Sciences, 93.4 (1996): 1591-1595.
[^3]: J. Miao. "Viscosity solutions of the eikonal equations." The University of Chicago, 2020.
[^4]: Y. Yang, W. Hao, Y.-T. Zhang. "A continuous finite element method with homotopy vanishing viscosity for solving the static eikonal equation." Communications in Computational Physics, 31.5 (2022): 1402-1433.