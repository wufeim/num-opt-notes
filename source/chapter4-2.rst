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
