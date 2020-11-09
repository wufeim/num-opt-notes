3.1 Introduction
=====================================

In computing the step lenght :math:`\alpha_k`, we face a tradeoff. We would like to choose :math:`\alpha_k` to give a substantial reduction of :math:`f`, but at the same time we do not want to spend too much time making the choice. The ideal choice would be the global optimizer of the univariate function :math:`\phi(\cdot)` defined by

.. math::

  \phi(\alpha) = f(x_k + \alpha p_k), \;\;\; \alpha > 0


but in general, it is too expensive to identify this value. More practical strategies perform an *inexact* line search to identify a step length that achieves adequate reductions in :math:`f` at minimal cost.

Typical line search algorithms try out a sequence of candidate values for :math:`\alpha`, stopping to accept one of these values when certain conditions are satisfied. The line search in done in two stages: A bracketing phase finds an interval containing desirable step lengths, and a bisection or interpolation phase computes a good step length within this interval.

We now discuss various termination conditions for line search algorithms and their effectiveness.

A simple condition we could impose on :math:`\alpha_k` is to require a reduction in :math:`f`, that is, :math:`f(x_k + \alpha_k p_k) < f(x_k)`. However, the insufficient reduction in :math:`f` at each step may cause it to fail to converge to the minimizer. Hence we need to enforce a *sufficient decrease* condition.

The Wolfe Conditions
-------------------------------------

A popular inexact line search condition stipulates that :math:`\alpha_k` should first of all give *sufficient decrease* in :math:`f`, as measured by the inequality:

.. math::

  f(x_k + \alpha p_k) \leq f(x_k) + c_k \alpha \nabla f_k^\top p_k

for some constant :math:`c_1 \in (0, 1)`. This is sometimes called the *Armijo condition*. The intervals on which this condition is satisfied are shown in the figure below. In practice, :math:`c_1` is chosen to be quite small, say :math:`c_1 = 10^{-4}`.

.. image:: images/fig3-1.png
  :width: 320pt

Note that the Armijo condition is satisfied on all sufficiently small values of :math:`\alpha`. To rule out unacceptably short steps we introduce a second requirement, called the *curvature condition*

.. math::

  \nabla f(x_k + \alpha_k p_k)^\top p_k \geq c_2 \nabla f_k^\top p_k

for some constant :math:`c_2 \in (c_1, 1)`. The left-hand-side is simply the derivative :math:`\phi'(\alpha_k)`, so the curvature ensures that the slope of :math:`\phi` at :math:`\alpha_k` is larger than :math:`c_2` times the initial slope :math:`\phi'(0)`. Typical values of :math:`c_2` are 0.9 for Newton or quasi-Newton method, and 0.1 for nonlinear conjugate gradient method.

The sufficient decrease and curvature conditions are known collectively as the *Wolfe conditions*. We restate here for future reference

.. math::

  f(x_k + \alpha_k p_k) & \leq f(x_k) + c_1 \alpha_k \nabla f_k^\top p_k \\
  \nabla f(x_k + \alpha_k p_k)^\top p_k & \geq c_2 \nabla f_k^\top p_k

with :math:`0 < c_1 < c_2 < 1`. We can modify the curvature condition to force :math:`\alpha_k` to lie in at least a broad neighborhood of a local minimizer or stationary point of :math:`\phi`. The *strong Wolfe conditions` require :math:`\alpha_k` to satisfy

.. math::

  f(x_k + \alpha_k p_k) & \leq f(x_k) + c_1 \alpha_k \nabla f_k^\top p_k \\
  \lvert \nabla f(x_k + \alpha_k p_k)^\top p_k \rvert & \leq \lvert c_2 \nabla f_k^\top p_k \rvert

with :math:`0 < c_1 < c_2 < 1`.

**Lemma 3.1:** Suppose that :math:`f: \mathbb{R}^n \to \mathbb{R}` is continuously differentiable. Let :math:`p_k` be a descent direction at :math:`x_k`, and assume that :math:`f` is bounded below along the ray :math:`\{x_k + \alpha p_k \mid \alpha > 0\}`. Then if :math:`0 < c_1 < c_2 < 1`, there exist intervals of step lengths satisfying the Wolfe conditions and the strong Wolfe conditions.

The Wolfe conditions are scale-invariant. They can be used in most line search methods, and are particularly important in the implementation of quasi-Newton methods.

The Goldstein Conditions
-------------------------------------

The Goldstein conditions can be stated as a pair of inequalities

.. math::

  f(x_k) + (1 - c) \alpha_k \nabla f_k^\top p_k \leq f(x_k + \alpha_k p_k) \leq f(x_k) + c \alpha_k \nabla f_k^\top p_k

with :math:`0 < c < 1/2`. The second inequality is the sufficient decrease condition, whereas the first inequality is introduced to control the the step length.

A disadvantage of the Goldstein condition is that the first inequality may exclude all minimizers of :math:`\phi`. The Goldstein conditions are often used in Newton-type methods but are not well-suited for quasi-Newton methods that maintain a positive definite Hessian approximation.

Sufficient Decrease and Backtracking
-------------------------------------

If we choose candidate step lengths appropriately by using the *backtracking* approach, we can dispense the curvature condition. In its most basic form, backtracking proceeds as follows.

| **Algorithm 3.1** (Backtracking Line Search).
|   Choose :math:`\bar{\alpha} > 0`, :math:`\rho \in (0, 1)`, :math:`c \in (0, 1)`; Set :math:`\alpha \leftarrow \bar{\alpha}`;
|   **repeat until** :math:`f(x_k + \alpha p_k) \leq f(x_k) + c\alpha \nabla f_k^\top p_k`
|     :math:`\alpha \leftarrow \rho\alpha`;
|   **end repead**
|   Terminate with :math:`\alpha_k = \alpha`.

The initial step length :math:`\bar{\alpha}` is chosen to be 1 in Newton and quasi-Newton methods. In practice, the contraction factor :math:`\rho` is often allowed to vary at each iteration. For example, it can be chosen by safeguard interpolation. We need ensure only at each iteration we have :math:`\rho \in [\rho_{lo}, \rho_{hi}]`, for some fixed constants :math:`0 < \rho_{lo} < \rho_{hi} < 1`.

This simple and popular strategy for terminating a line search is well-suited for Newton methods but is less appropriate for quasi-Newton and conjugate gradient methods.
