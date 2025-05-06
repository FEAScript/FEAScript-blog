---
layout: post
title: "Finite Element Method Notes"
date: 2023-12-01
categories: [Numerical Methods, FEM]
tags: [FEAScript, FEM, Galerkin, Numerical Methods, Tutorial]
mathjax: true
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

The finite element method is a discretization technique that can utilize a computational mesh to approximate the solution of a partial differential equation. Basic concepts of the finite element method are described below.

## Galerkin Residuals

Consider a typical formulation of a boundary value problem (BVP):

$$
\begin{eqnarray}
Lu &= f \quad \text{in} \quad D, \\
Bu &= g \quad \text{on} \quad \partial D.
\end{eqnarray} \tag{1}
$$

The solution \\(u\\) is a function of the position vector \\(\bar{x}\\) at the domain \\(D\\), which is a subregion of a one-, two-, or three-dimensional Euclidean space. The position vector \\(\bar{x}\\) is defined as: \\( \bar{x} = \sum_{i=1}^{n} x_i e_i \\), where \\(e_i\\) are the unit vectors and \\(n\\) is the dimension of the Euclidean space. \\(L\\) is the differential operator and \\(B\\) is a boundary operator defined at the boundary \\(\partial D\\). The solution \\(u\\) can be approximated using a linear combination of basis functions \\(\phi^1, \phi^2, \phi^3, \dots, \phi^N\\) such that: \\( u(x) = \sum_{j=1}^{N} u_j \phi^j(x) \\), where the number of basis functions equals the number of nodes of the computational mesh.

The Galerkin method seeks a solution that zeroes out every one of the following weighted residuals:

$$
\begin{aligned}
R_i &= \int_{D} (Lu - f) \phi^i \, dS \\
&= \int_{D} \phi^i \left( L\left( \sum_{j=1}^N u_j \phi^j \right) \right) \, dS - \int_{D} f \phi^i \, dS \\
&\quad \text{for} \quad i = 1, 2, \dots, N.
\end{aligned} \tag{2}
$$

These integrals depend solely on the nodal values \\(u_j\\), which are the unknowns to be determined. The number of residuals is equal to the number of basis functions, which in turn is equal to the number of nodes, \\(N\\), in the computational mesh. Setting the Galerkin residuals to zero leads to a system of \\(N\\) algebraic equations with \\(N\\) unknowns, which can be solved to obtain the approximate solution.

## Boundary Conditions

In general, there are three common types of boundary conditions that can be imposed in boundary value problems: Dirichlet, Neumann, and Robin boundary conditions. The boundary conditions that specify the value of \\(u\\) on a portion of \\(\partial D\\) are called Dirichlet boundary conditions, and they are imposed directly in the discretization equations. In particular, the Dirichlet boundary conditions replace the Galerkin residuals at the computational nodes that lie on the portion of the boundary where the solution value is prescribed.

Consider, for example, a boundary node \\(n\\) at position \\(t_n\\), where the solution is defined by the boundary condition \\(u = F(t)\\), with \\(F(t)\\) being a known function of the position \\(t\\) on \\(\partial D\\). In this case, the \\(n\\)-th residual is replaced by: \\(R_n = u_n - F(t_n)\\).

The boundary conditions that define the value of the derivative of \\(u\\) on a portion of \\(\partial D\\) are called Neumann (or natural) boundary conditions. These are imposed indirectly in the discretization equations. Consider that the highest rank of differentiation of the operator \\(L\\) is \\( \frac{d^m}{dx^m} \\). The corresponding integral at the residuals will be:

$$I_m = \int_{D} \phi^i \frac{d^m u}{dx^m} \, dx. \tag{3}$$

By applying integration by parts, we get:

$$ I_m = \oint_{\partial D} \phi^i \frac{d^{m-1} u}{dx^{m-1}} \, dt - \int_{D} \frac{d\phi^i}{dx} \frac{d^{m-1} u}{dx^{m-1}} \, dx, \tag{4}$$

where \\(t\\) is the independent variable at the boundary \\(\partial D\\). A boundary condition of \\(m-1\\) rank is imposed at the line integral. Thus, in the case where the Neumann boundary condition is \\( \frac{d^{m-1}u}{dx^{m-1}} = g(t) \\) on \\(\partial D\\), where \\(g(t)\\) is a known function, then:

$$ I_m = \oint_{\partial D} \phi^i g(t) \, dt - \int_{D} \frac{d\phi^i}{dx} \frac{d^{m-1} u}{dx^{m-1}} \, dx. \tag{5}$$

If the Neumann boundary condition has a rank \\(k < (m-1)\\), then we continue to apply integration by parts until the \\(k\\)-th rank derivative appears on the line integral.

Finally, Robin boundary conditions, also known as mixed boundary conditions, specify a linear combination of the function \\(u\\) and its derivative on a portion of \\(\partial D\\). These are imposed in a similar fashion to the Neumann boundary conditions.

## Isoparametric Mapping

The basis functions are defined on reference elements: on the unit interval \\(0 \le \xi \le 1\\) in 1D, and on the unit square \\(0 \le \xi \le 1\\), \\(0 \le \eta \le 1\\) in 2D. However, the basis functions also need to be mapped to the initial domain \\(D\\) of the BVP since the solution \\(u\\) is approximated by basis functions defined on \\(D\\). The change from the \\(\bar{\xi}\\) system to the \\(\bar{x}\\) system is performed through isoparametric mapping, where \\(\bar{\xi} = (\xi, \eta)\\) and \\(\bar{x} = (x, y)\\). In this process, the reference element is mapped to every element of the computational mesh on \\(D\\). The same basis functions are used for the mapping:

$$\bar{x} = \sum_{i=1}^{n_k} \bar{x_i} \phi_i(\xi), \tag{6}$$

where \\(\bar{x}\\) is the position vector of the mesh element, \\(\bar{x_i}\\) is the position vector of the \\(i\\)-th node in local numbering of the mesh element, \\(\bar{\xi}\\) is the position vector of the reference element, and \\(n_k\\) is the number of nodes in the reference element. Keep in mind that \\(\phi_i\\) corresponds to the local basis function, where \\(i\\) is the local number of the node in the reference element (as opposed to the global definition of the basis function \\(\phi^i\\), where \\(i\\) corresponds to the global node number in this case).

From the above mapping, we can define the reverse mapping from \\(\bar{x}\\) to \\(\bar{\xi}\\). The reverse mapping is calculated by solving the isoparametric mapping relation (Eq. (6)) for \\(\bar{\xi}\\) as a function of \\(\bar{x}\\): \\(\bar{\xi} = \bar{\xi}(\bar{x})\\). The basis functions are then expressed in the coordinate system of \\(D\\) (the \\(\bar{x}\\) system) as \\(\phi_i(\bar{\xi}(\bar{x}))\\), where \\(i = 1, 2, \dots, n_k\\).

In the case where \\(D\\) is a two-dimensional domain, the Jacobian of the mapping is the matrix:

$$ \bar{\bar{J}} = \begin{vmatrix} x_{\xi} & y_{\xi} \\ x_{\eta} & y_{\eta} \end{vmatrix}, \tag{7}$$

where \\( x_{\xi} = \frac{\partial x}{\partial \xi}\\), \\( y_{\xi} = \frac{\partial y}{\partial \xi}\\), \\( x_{\eta} = \frac{\partial x}{\partial \eta}\\), \\( y_{\eta} = \frac{\partial y}{\partial \eta}\\). The relation between the \\(\bar{x}\\)- and \\(\bar{\xi}\\)-partial derivatives of the basis function can also be calculated as:

$$ \bar{\bar{J}} \begin{vmatrix} \frac{\partial \phi_i}{\partial x} \\ \frac{\partial \phi_i}{\partial y} \end{vmatrix} = \begin{vmatrix} \frac{\partial \phi_i}{\partial \xi} \\ \frac{\partial \phi_i}{\partial \eta} \end{vmatrix}. \tag{8} $$

By solving the above equation, we can calculate the partial derivatives of the basis function with respect to \\(x\\) and \\(y\\):

$$
\begin{eqnarray}
\frac{\partial \phi_i}{\partial x} &=& \frac{1}{\text{det}\bar{\bar{J}}} \left( y_{\eta} \frac{\partial \phi_i}{\partial \xi} - y_{\xi} \frac{\partial \phi_i}{\partial \eta} \right), \\
\frac{\partial \phi_i}{\partial y} &=& \frac{1}{\text{det}\bar{\bar{J}}} \left( x_{\xi} \frac{\partial \phi_i}{\partial \eta} - x_{\eta} \frac{\partial \phi_i}{\partial \xi} \right).
\end{eqnarray} \tag{9}
$$

where \\(\text{det}\bar{\bar{J}}\\) is the determinant of the Jacobian: \\( \text{det}\bar{\bar{J}} = x_{\xi} y_{\eta} - x_{\eta} y_{\xi}\\). In the case where \\(D\\) is a one-dimensional domain, Eq. (6) is reduced to: \\( x = \sum_{i=1}^{n_k} x_i \phi_i(\xi) \\). The Jacobian of the mapping in this case is: \\( J = \frac{dx}{d\xi} = x_{\xi} \\), and the partial derivative of the basis function is: \\( \frac{d\phi_i}{dx} = \frac{d\phi_i}{d\xi} \Big/ x_{\xi} \\).

## Residuals Computation

A typical representative of the integrals in the Galerkin residuals is the following:

$$ I_{ij} = \int_{D} \phi^i L \phi^j \, d\bar{x}. \tag{10} $$

The computational mesh covering \\(D\\) consists of \\(NE\\) finite elements \\(E_k\\) \\((k = 1, 2, \dots, NE)\\). Thus, the integral \\(I_{ij}\\) is the sum of the partial integrals:

$$
\begin{aligned}
I_{ij} &= \sum_{k=1}^{NE} I_{ij}^k, \\
I_{ij}^k &\equiv \int_{E_k} \phi^i L \phi^j \, d\bar{x}.
\end{aligned} \tag{11}
$$

Each of the integrals \\(I_{ij}^k\\) is calculated through the isoparametric mapping by transforming the coordinate system as follows:

$$ I_{ij}^k = \int_{E_0} \phi_i(\bar{\xi}) L_{\bar{\xi}} \phi_j(\bar{\xi}) \, \text{det}(\bar{\bar{J}}) \, d\bar{\xi}, \tag{12} $$

where \\(E_0\\) is the reference element, and \\(L_{\bar{\xi}}\\) is the differential operator expressed in the \\(\bar{\xi}\\)-coordinate system. The integrals of the discretization equations are then calculated numerically on the reference element. Specifically, these calculations are performed using the Gauss quadrature method:

$$ \int_{E_0} f(\bar{\xi}) \, d\bar{\xi} = \sum_{k=1}^{NGP} w_k f(\bar{\xi}_{gk}), \tag{13} $$

where \\(w_k\\) are the Gauss weights, \\(\bar{\xi}_{gk}\\) are the Gauss points inside the reference element where the integrand is evaluated, and \\(NGP\\) is the number of Gauss points.

## References

- A. G. Boudouvis "Computational Analysis with the Finite Element Method", Lecture Notes, National Technical University of Athens, Athens, 1992 (In Greek)
- O. C. Zienkiewicz "The Finite Element Method", 3rd edition, McGraw-Hill, London, 1977