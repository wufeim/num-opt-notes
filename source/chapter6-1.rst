6.1 The BFGS Method
=====================================

The BFGS method is named for its discoverers Broyden, Fletcher, Goldfarb, and Shanno.

We begin with the quadratic model of the objective function at the current iterate :math:`x_k`:

.. math::

  m_k(p) = f_k + \nabla f_k^\top p + \frac{1}{2} p^\top B_k p

Here :math:`B_k` is an :math:`n \times n` symmetric positive definite matrix that will be updated at every iteration. The minimizer :math:`p_k` of this model is given by

.. math::

  p_k = -B_k^{-1}\nabla f_k

and is used as the search direction. The new iterate is

.. math::

  x_{k+1} = x_k + \alpha_kp_k

where :math:`\alpha_k` is chosen to satisfy the Wolfe conditions.

Davidon proposed to update :math:`B_k` in a simple manner to account for the curvature measured during the most recent step. Given :math:`x_{k+1}`, we wish to construct a new quadratic model, of the form

.. math::

  m_{k+1}(p) = f_{k+1} + \nabla f_{k+1}^\top p + \frac{1}{2}p^\top B_{k+1}p

One resonable requirement of :math:`B_{k+1}` is that the gradient of :math:`m_{k+1}` should match the gradient of the objective function :math:`f` at :math:`x_k` and :math:`x_{k+1}`. Since :math:`\nabla m_{k+1}(0)` is precisely :math:`\nabla f_{k+1}`, we only care about the first condition, written by

.. math::

  \nabla m_{k+1}(-\alpha_kp_k) = \nabla f_{k+1} - \alpha_kB_{k+1}p_k = \nabla f_k

Then we obtain

.. math::

  B_{k+1}\alpha_k p_k = \nabla f_{k+1} - \nabla f_k

To simplify the notation, we define the vectors

.. math::

  s_k = x_{k+1} - x_k = \alpha_kp_k, \;\;\; y_k = \nabla f_{k+1} - \nabla f_k

So we have

.. math::

  B_{k+1}s_k = y_k

We refer to this formula as the **secant equation**.
