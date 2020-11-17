4.1 Algorithms Based on the Cauchy Point
=====================================

The Cauchy Point
-------------------------------------

It is enough for purposes of global convergence to find an approximate solution :math:`p_k` that lies within the trust region and gives a *sufficient reduction* in the model. The sufficient reduction can be quantified in terms of the Cauchy point, denoted by :math:`p_k^c`.

| **Algorithm 4.2** (Steihaug's Algorithm, Cauchy Point Calculation).
|   Find the vector :math:`p_k^s` that solves a linear version of the trust-region subproblem, given by
|     :math:`p_k^s = \text{argmin}_{p \in \mathbb{R}^n} f_k + g_k^\top p \;\;\; \text{s.t. } \lVert p \rVert \leq \delta_k`
|   Calculate the scalar :math:`\tau_k > 0` that minimizes :math:`m_k(\tau p_k^s)` subject to satisfying the trust-region bound, that is
|     :math:`\tau_k = \text{argmin}_{\tau \geq 0} m_k(\tau p_k^s) \;\;\; \text{s.t. } \lVert \tau p_k^s \rVert \leq \delta_k`
|   Set :math:`p_k^c = \tau_kp_k^s`.

The closed-form solution to the first subproblem is simply

.. math::

  p_k^s = - \frac{\delta_k}{\lVert g_k \rVert} g_k

By considering :math:`g_k^\top B_kg_k \leq 0` and :math:`g_k^\top B_kg_k > 0` separately, we have

.. math::

  p_k^c = -\tau_k \frac{\delta_k}{\lVert g_k \rVert} g_k

where

.. math::

  \tau_k = \begin{cases}
    1 & \text{if } g_k^\top B_kg_k \leq 0 \\
    \min(\lVert g_k \rVert^3/(\delta_k g_k^\top B_kg_k), 1) & \text{otherwise}
  \end{cases}

The Cauchy step :math:`p_k^c` is inexpensive to calculate and is of crucial importance in deciding if an approximate solution of the trust-region subproblem is acceptable. Specifically, a trust-region method will be globally convergent if its steps :math:`p_k` give a reduction in the :math:`m_k` that is at least some fixed positive multiple of the decrease attained by the Cauchy step.

Improving on the Cauchy Point
-------------------------------------

The Cauchy point is simply the steepest descent method with a particular choice of step lengths. Steepest descent methods perform poorly even if an *optimal* step length is used at each iteration. Now we focus on the trust-region subproblem

.. math::

  \min_{p \in \mathbb{R}^n} m(p) = f + g^\top p + \frac{1}{2}p^\top Bp \;\;\; \text{s.t. } \lVert p \rVert \leq \delta

and we denote the solution by :math:`p^*(\delta)`.

The Dogleg method
-------------------------------------

The *dogleg method* an be used when :math:`B` is positive definite. The unconstrained minimizer of :math:`m` is :math:`p^B = -B^{-1}g`, so we have

.. math::

  p^*(\delta) = p^B \;\;\; \text{when } \delta \geq \lVert p^B \rVert

When :math:`delta` is small relative to :math:`p^B`, the restriction :math:`\lVert p \rVert \leq \delta` ensures that the quadratic term in :math:`m` has little effect on the solution, and we can get an approximation to :math:`p(\delta)` by omitting the qudaratic term and writing

.. math::

  p^*(\delta) \approx - \delta \frac{g}{\lVert g \rVert} \;\;\; \text{when } \delta \text{ is small}

For intermediate values of :math:`\delta`, the solution :math:`p^*(\delta)` typically follows a curved trajectory like the one in the figure below.

.. image:: images/fig4-3.png
  :width: 320pt

The dogleg method finds an approximate solution by replacing the curved trajectory for :math:`p^*(\delta)` with a path consisting of two line segments. The first line segment runs from the origin to the minimizer of :math:`m` along the steepest descent direction, which is

.. math::

  p^U = - \frac{g^\top g}{g^\top Bg} g

while the second line segment runs from :math:`p^U` to :math:`p^B`. We denote this trajectory by :math:`\tilde{p}(\tau)` for :math:`\tau \in [0, 2]`, where

.. math::

  \tilde{p}(\tau) = \begin{cases}
    \tau p^U & 0 \leq \tau \leq 1 \\
    p^U + (\tau - 1)(p^B - p^U)
  \end{cases}

The dogleg method chooses :math:`p` to minimize the model :math:`m` along this path.

**Lemma 4.2.** Let :math:`B` be positive definite, then
1. :math:`\lVert \tilde{p}(\tau) \rVert` is an increasing function of :math:`\tau`
2. :math:`m(\tilde{p}(\tau))` is a decreasing function of :math:`\tau`

It follows that the chosen value :math:`p` will be at :math:`p^B` if :math:`\lVert p^B \rVert \leq \delta`, otherwise at the point of intersection of the dogleg and the trust-region boundary.

When the exact Hessian :math:`\nabla^2 f(x_k)` is available, we find the Newton-dogleg step. We conclude that the Newton-dogleg method is most appropriate when the objective function is convex (when :math:`\nabla^2 f(x_k)` is always positive semidefinite).

Two-Dimensional Subspace Minimization
-------------------------------------

The dogleg method can be made slightly more complicated by widening the search for :math:`p` to the entire two-dimensional subspace spanned by :math:`p^U` and :math:`p^B`. The subproblem is repalced by

.. math::

  \min_p m(p) = f + g^\top p + \frac{1}{2} p^\top Bp \;\;\; \text{s.t. } \lVert p \rVert \leq \delta, p \in \text{span}[g, B^{-1}g]

It can be reduced to finding the roots of a fourth degree polynomial. Clearly the Cauchy point :math:`p^C` is feasible, resulting in global convergence of the algorithm.
