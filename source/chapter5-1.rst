5.1 The Linear Conjugate Gradient Method
=====================================

The conjugate gradient method is an iterative method for solving a lienar system of equations

.. math::

  Ax = b

where :math:`A` is an :math:`n \times n` symmetric positive definite matrix. This problem can be stated equivalently as the following minimization problem

.. math::

  \min \phi(x) \stackrel{\text{def}}{=} \frac{1}{2} x^\top Ax - b^\top x

For further reference, we note that the gradient of :math:`\phi` equals the residual of the linear system

.. math::

  \nabla \phi(x) = Ax - b \stackrel{\text{def}}{=} r(x)

Conjugate Direction Methods
-------------------------------------

One of the remarkable properties of the conjugate gradient method is its ability to generate a set of vectors with a property knwon as **conjugacy**. A set of nonzero vectors :math:`\{p_0, \dots, p_l\}` is said to be *conjugate* with respect to the symmetric positive definite :math:`A` if

.. math::

  p_k^\top A p_j = 0, \;\;\; \text{for all } i \neq j

It is easy to show that such set of vectors is linearly independent.

The importance of conjugacy lies in the fact that we can minimize :math:`\phi(\cdot)` in :math:`n` steps by successively minimizing it along the individual directions in a conjugate set. We consider the following **conjugate direction method**. Given a starting point :math:`x_0 \in \mathbb{R}^n` and a set of conjugate directions :math:`\{p_0, \dots, p_{n-1}\}`, we generate the sequence :math:`\{x_k\}` by setting

.. math::

  x_{k+1} = x_k + \alpha_k p_k

where :math:`\alpha_k` is the one-dimensional minimizer of the quadratic function :math:`\phi(k)` given by

.. math::

  \alpha_k = - \frac{r_k^\top p_k}{p_k^\top A p_k}
