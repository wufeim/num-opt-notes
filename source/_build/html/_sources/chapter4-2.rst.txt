4.2 Global Convergence
=====================================

Reduction Obtained by the Cauchy Point
-------------------------------------

The first main result is that the dogleg and two-dimensional subspace minimization algorithms and Steihaug's Algorithm produce approximate solutions :math:`p_k` of the subproblem satisfying the following estimate of decrease in the model function

.. math::
  :label: eq4-20

  m_k(0) - m_k(p_k) \geq c_1 \lVert g_k \rVert \min\left(\delta_k, \frac{\lVert g_k \rVert}{\lVert B_k \rVert} \right)

**Lemma 4.3.** The Cauchy point :math:`p_k^C` satisifies :eq:`eq4-20` with :math:`c_1 = \frac{1}{2}`, that is,

.. math::

  m_k(0) - m_k(p_k^C) \geq \frac{1}{2} \lVert g_k \rVert \min\left(\delta_k, \frac{\lVert g_k \rVert}{\lVert B_k \rVert} \right)

**Theorem 4.4.** Let :math:`p_k` be any vector such that :math:`\lVert p_k \rVert \leq \delta_k` and :math:`m_k(0) - m_k(p_k) \geq c_2 (m_k(0) - m_k(p_k^C))`. Then :math:`p_k` satisfies :eq:`eq4-20` with :math:`c_1 = c_2 / 2`. In particular, if :math:`p_k` is the exact solution of

.. math::

  \min_{p \in \mathbb{R}^n} m_k(p) = f_k + g_k^\top p + \frac{1}{2} p^\top B_k p \;\;\; \text{s.t. } \lVert p \rVert \leq \delta_k

then it satisfies :eq:`eq4-20` with :math:`c_1 = \frac{1}{2}`.
