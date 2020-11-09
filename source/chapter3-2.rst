3.2 Convergence of Line Search Methods
=====================================

We disucss requirements on the search direction in this section, focusing on the angle :math:`\theta_k` between :math:`p_k` and the steepest descent direction :math:`-\nabla f_k`, defined by

.. math::

  \cos \theta_k = \frac{-\nabla f_k^\top p_k}{\lVert \nabla f_k \rVert \lVert p_k \rVert}

The following theorem, due to Zoutendijk, quantifies the effort of properly chosen step lengths :math:`\alpha_k`, and shows that the steepest descent method is globally convergent. For other algorithms, it describes how far :math:`p_k` can deviate from the steepest descent direction and still produce a globally convergent iteration.

**Theorem 3.2.** Consider any iteration of the form

.. math::

  x_{k+1} = x_k + \alpha_kp_k

where :math:`p_k` is a descent direction and :math:`\alpha_k` satisfies the Wolfe conditions. Suppose that :math:`f` is bounded below in :math:`\mathbb{R}` and that :math:`f` is continuously differentiable in an open set :math:`\mathcal{N}` containing the level set :math:`\mathcal{L} \stackrel{\text{def}}{=} \{x: f(x) \leq f(x_0)\}`, where :math:`x_0` is the starting point of the iteration. Assuming also that the gradient :math:`\nabla f` is Lipshitz continuous on :math:`\mathcal{N}`, that is, there exists a constant :math:`L > 0` such that

.. math::

  \lVert \nabla f(x) - \nabla f(\tilde{x}) \leq L \lVert x - \tilde{x} \rVert, \;\;\; \text{for all } x, \tilde{x} \in \mathcal{N}

Then

.. math::

  \sum_{k \geq 0}^\infty \cos^2 \theta_k \lVert \nabla f_k \rVert^2 < \infty

Similar results to this theorem holds when the Goldstein conditions or strong Wolfe conditions are used. For all these strategies, the step length selection implies this inequality, which we call the *Zoutendijk condition*.

The Zoutendijk condition implies that

.. math::

  \cos^2 \theta_k \lVert \nabla f_k \rVert^2 \to 0

.. warning:

  How to show this?

This limit can be used to derive global convergence results for line serach algortihms.

If the angle :math:`\theta_k` is bounded away from :math:`\pi/2`, there is a positive constant :math:`\delta` such that

.. math::

  \cos \theta_k \geq \delta > 0, \;\;\; \text{for all } k

It follows immediately that

.. math::

  \lim_{k \to \infty} \lVert \nabla f_k \rVert = 0

We use the term *globally convergent* to refer to algorithms for which this property is satisfied. For line serach methods of the general form, this limit is the strongest global convergence result that can be obtained. Only by making additional requirements on the search direction :math:`p_k` -- by introducing negative curvature information from the Hessian :math:`\nabla^2 f(x_k)` -- can we strengthen these results to include convergence to a local minimum.

Consider now the Newton-like method and assume that the matrices :math:`\mathbf{B}_k` are positive definite with a uniformly bounded condition number. That is, there is a constant :math:`M` such that

.. math::

  \lVert \mathbf{B}_k \rVert \lVert \mathbf{B}_k^{-1} \rVert \leq M, \;\;\; \text{for all } k

It follows that

.. math::

  \cos \theta_k \geq 1/M

Thus we have

.. math::

  \lim_{k \to \infty} \lVert \nabla f_k \rVert = 0

Therefore, we have shown that Newton and quasi-Newton methods are globally convergent if the matrices :math:`\mathbf{B}_k` have a bounded condition number and are positive definite, and if the step lengths satisfy the Wolfe conditions.

For some algorithms, such as conjugate gradient methods, we will be able to prove the limit, but only the weaker result

.. math::

  \lim_{k \to \infty} \inf \lVert \nabla f_k \rVert = 0

In other words, just a subsequence of the gradient norms :math:`\lVert \nabla f_{k_j} \rVert` converges to zero. This can be proved using Zoutendijk's condition by contradiction. Therefore, for any algorithm that has a steepest descent step every :math:`m` th iteration, we can prove global convergence.
