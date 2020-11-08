3 Line Search Methods
*************************************

.. toctree::
   :maxdepth: 2
   
   chapter3-1
   chapter3-2

Each iteration of a line search method computes a search direction :math:`p_k` and then decides how far to move along that direction. The iteration is given by

.. math::

  x_{k+1} = x_k + \alpha_k p_k

where the positive scalar :math:`\alpha_k` is called the *step length*.

Most line search algorithms require :math:`p_k` to be a *descent direction* -- one for which :math:`p_k^\top \nabla f_k < 0` -- because this property guarantees that the function :math:`f` can be reduced along this direction. Moreover, the search direction often has the form

.. math::

  p_k = - \mathbf{B}_k^{-1} \nabla f_k

where :math:`\mathbf{B}_k` is a symmetric and nonsingular matrix. In the steepest descent method, :math:`\mathbf{B}_k` is simply the identity matrix :math:`\mathbf{I}`. In Newton's method, :math:`\mathbf{B}_k` is the exact Hessian :math:`\nabla^2 f(x_k)`. In quasi-Newton methods, :math:`\mathbf{B}_k` is an approximation to the Hessian updated by a low-rank formula. When :math:`\mathbf{B}_k` is positive definite, we have

.. math::

  p_k^\top \nabla f_k = - \nabla f_k^\top \mathbf{B}_k^{-1} \nabla f_k < 0

and therefore :math:`p_k` is a descent direction. In this chapter, we discuss how to choose :math:`\alpha_k` and :math:`p_k` to promote convergence from remote starting points. We also study the rate of convergence of steepest descent, quasi-Newton, and Newton methods. We also discuss modifications to Newton methods in Section 3.4.
