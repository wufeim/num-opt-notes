8.1 Finite-Difference Derivative Approximations
=====================================

The approach in this section is to make small, finite perturbations in the values of :math:`x` and examine the resulting differences in the function values.

Approximating the Gradient
-------------------------------------

A popular formula for approximating the partial derivative :math:`\partial f / \partial x` at a given point :math:`x` is the **forward-difference**, or **one-sided-difference**, approximation, defined as

.. math::

   \frac{\partial f}{\partial x_i}(x) \approx \frac{f(x + \epsilon e_i) - f(x)}{\epsilon}

This process requires :math:`(n+1)` evaluations of :math:`f` at :math:`x, x + \epsilon e_i`.

When :math:`f` is twice continuously differentiable, we have

.. math::

   f(x + p) = f(x) + \nabla f(x)^\top p + \frac{1}{2} p^\top \nabla^2 f(x + tp)p

for some :math:`t \in (0, 1)`. Let :math:`L` be a bound on the size of :math:`\lVert \nabla^2 f(\cdot) \rVert`. It follows that

.. math::

   \lVert f(x + p) - f(x) - \nabla f(x)^\top p \rVert \leq (L / 2)\lVert p \rVert^2

Let :math:`p` be :math:`\epsilon e_i`. We have that

.. math::

   \nabla f(x)^\top p = \nabla f(x)^\top e_i = \partial f / \partial x_i

and

.. math::

   \frac{\partial f}{\partial x_i}(x) = \frac{f(x + \epsilon e_i) - f(x)}{\epsilon} + \delta_\epsilon, \;\;\; \text{where } \lvert \delta_\epsilon \rvert \leq (L / 2)\epsilon
