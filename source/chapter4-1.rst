4.1 Algorithms Based on the Cauchy Point
=====================================

The Cauchy Point
-------------------------------------

It is enough for purposes of global convergence to find an approximate solution :math:`p_k` that lies within the trust region and gives a *sufficient reduction* in the model. The sufficient reduction can be quantified in terms of the Cauchy point, denoted by :math:`p_k^c`.

| **Algorithm 4.2** (Cauchy Point Calculation).
|   Find the vector :math:`p_k^s` that solves a linear version of the trust-region subproblem, given by
|

.. math::

  p_k^s = \text{argmin}_{p \in \mathbb{R}^n} f_k + g_k^\top p \;\;\; \text{s.t. } \lVert p \rVert \leq \delta_k

|   Calculate the scalar :math:`\tau_k > 0` that minimizes :math:`m_k(\tau p_k^s)` subject to satisfying the trust-region bound, that is

.. math::

  \tau_k = \text{argmin}_{\tau \geq 0} m_k(\tau p_k^s) \;\;\; \text{s.t. } \lVert \tau p_k^s \rVert \leq \delta_k

|   Set :math:`p_k^c = \tau_kp_k^s`.
