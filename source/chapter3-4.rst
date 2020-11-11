3.4 Newton's Method with Hessian Modification
=====================================

Away from the solution, the Hessian matrix :math:`\nabla^2 f(x)` may not be positive definite, so the Newton direction defined by

.. math::

  \nabla^2 f(x_k)p_k^N = - \nabla f(x_k)

may not be a descent direction.

| **Algorithm 3.2** (Line Search Newton with Modification).
|   Given initial point :math:`x_0`;
|   **for** :math:`k = 0, 1, 2, \dots`
|     Factorize the matrix :math:`B_k = \nabla^2f(x_k) + E_k`, where :math:`E_k = 0` if :math:`\nabla^2f(x_k)` is sufficiently positive definite; otherwise, :math:`E_k` is chosen to ensure that :math:`B_k` is sufficiently positive definite;
|     Solve :math:`B_kp_k = - \nabla f(x_k)`;
|     Set :math:`x_{k+1} = x_k + \alpha_kp_k`, where :math:`\alpha_k` satisfies the Wolfe, Goldstein, or Armijo backtracking conditions;
|   **end**

We would have fairly satisfactory global convergence results for it, provided that the strategy for choosing :math:`E_k` satisfies the *bounded modified factorization* property. This property is that the matrices in the sequence :math:`\{B_k\}` have bounded condition number whenever the sequence of Hessians :math:`\{ \nabla^2f(x_k) \}` is bounded; that is,

.. math::

  \kappa(B_k) = \lVert B_k \rVert \lVert B_k^{-1} \rVert \leq C, \;\;\; \text{some } C > 0 \text{ and all } k = 0, 1, 2, \dots

If this property holds, global convergence of the modified line search Newton method follows from the results of Section 3.2.

**Theorem 3.8.** Let :math:`f` be twice continuously differentiable on an open set :math:`\mathcal{D}`, and assume that the starting point :math:`x_0` of Algorithm 3.2 is such that the level set :math:`\mathcal{L} = \{ x \in \mathcal{D}: f(x) \leq f(x_0)\}` is compact. Then if the bounded modified factorization property holds, we have that

.. math::

  \lim_{k \to \infty} \nabla f(x_k) = 0

For problems in which :math:`\nabla f^*` is close to singular, there is no guarantee that the modification :math:`E_k` will eventually vanish, and the convergence rate may be only linear. Besides requiring the modified matrix :math:`B_k` to be well conditioned, we would like the modification to be as small as possible, so that the second-order information in the Hessian is preserved as far as possible.

Eigenvalue Modification
-------------------------------------

Adding A Multiple of The Identity
-------------------------------------

Modified Cholesky Factorization
-------------------------------------

Modified Symmetric Indefinite Factorization
-------------------------------------
