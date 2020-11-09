3.2 Convergence of Line Search Methods
=====================================

We disucss requirements on the search direction in this section, focusing on the angle :math:`\theta_k` between :math:`p_k` and the steepest descent direction :math:`-\nabla f_k`, defined by

.. math::

  \cos \theta_k = \frac{-\nabla f_k^\top p_k}{\lVert \nabla f_k \rVert \lVert p_k \rVert}

**Theorem 3.2.** Consider any iteration of the form

.. math::

  x_{k+1} = x_k + \alpha_kp_k

where :math:`p_k` is a descent direction and :math:`\alpha_k` satisfies the Wolfe conditions. Suppose that :math:`f` is bounded below in :math:`\mathbb{R}` and that :math:`f` is continuously differentiable in an open set :math:`\mathcal{N}` containing the level set :math:`\mathcal{L} \stackrel{\text{def}}{=} \{x: f(x) \leq f(x_0)\}`, where :math:`x_0` is the starting point of the iteration. Assuming also that the gradient :math:`\nabla f` is Lipshitz continuous on :math:`\mathcal{N}`, that is, there exists a constant :math:`L > 0` such that

.. math::

  \lVert \nabla f(x) - \nabla f(\tilde{x}) \leq L \lVert x - \tilde{x} \rVert, \;\;\; \text{for all } x, \tilde{x} \in \mathcal{N}

Then

.. math::

  \sum_{k \geq 0} \cos^2 \theta_k \lVert \nabla f_k \rVert^2 < \infty
