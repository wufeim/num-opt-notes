3.5 Step-Length Selection Algorithms
=====================================

We now consider techniques for finding a minimum of the one-dimensional function

.. math::

  \phi(\alpha) = f(x_k + \alpha p_k)

or for simply finding a step length :math:`\alpha_k` satisfying one of the termination conditions described in Section 3.1. We assume that :math:`p_k` is a descent direction, so that our search can be confined to positive values of :math:`\alpha`.

If :math:`f` is convex quadratic, :math:`f(x) = \frac{1}{2} x^\top Qx - b^\top x`, its one-dimensional minimizer is given by

.. math::

  \alpha_k = -\frac{\nabla f_k^\top p_k}{p_k^\top Qp_k}

For general nonlinear functions, it is necessary to use an iterative procedure. The line search procedure deserves particular attention because it has a major impact on the robustness and efficiency of all nonlinear optimization methods.

All line serach procedures require an initial estimate :math:`\alpha_0` and generate a sequence :math:`\{\alpha_i\}`. Typical procedures consist of two phases: a *bracketing phase* that finds an interval :math:`[\bar{a}, \bar{b}]` containing acceptable step lengths, and a *selection phase* that zooms in to locate the final step length.

Interpolation
-------------------------------------

We begin by describing a line search procedure that aims to find a value of :math:`\alpha` that satisfies the sufficient decrease condition, without being "too small".

We can write the sufficient decrease condition as

.. math::

  \phi(\alpha_k) \leq \phi(0) + c_1\alpha_k \phi'(0)

Suppose that the initial guess :math:`\alpha_0` is given. If we have

.. math::

  \phi(\alpha_0) \leq \phi(0) + c_1\alpha_0\phi'(0)

this step length satisfies the condition, and we terminate the search. Otherwise we know that the interval :math:`[0, \alpha_0]` contains acceptable step lengths. We form a quadratic approximation :math:`\phi_q(\alpha)` to :math:`\phi` by interpolating :math:`\phi(0)`, :math:`\phi'(0)`, and :math:`\phi(\alpha_0)` to obtain

.. math::

  \phi_q(\alpha) = \left( \frac{\phi(\alpha_0) - \phi(0) - \alpha_0\phi'(0)}{\alpha_0^2} \right) \alpha^2 + \phi'(0)\alpha + \phi(0)

The new trial value :math:`\alpha_1` is defined as the minimizer of this quadratic, given by

.. math::

  \alpha_1 = - \frac{\phi'(0)\alpha_0^2}{2[\phi(\alpha_0) - \phi(0) - \phi'(0)\alpha_0]}

We terminate the search if the sufficient decrease condition is satisfied. Otherwise we construct a cubic function that interpolates the four pieces of information. This process of interpolating with a cubic function is repeated if necessary. If any :math:`\alpha_i` is either too close to its predecessor :math:`\alpha_{i-1}` or else too smaller than :math:`\alpha_{i-1}`, we reset :math:`\alpha_i = \alpha_{i-1}/2`.

This strategy above assumes that derivative values are significantly more expenseive to compute than function values. Cubic interpolation provides a good model for functions with significant changes of curvature, and usually produces a quadratic rate of convergence to the minimizing values of :math:`\alpha`.

Initial Step Lengths
-------------------------------------

A Line Search Algorithm for The Wolfe Conditions
-------------------------------------
