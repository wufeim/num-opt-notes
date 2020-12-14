8 Calculating Derivatives
*************************************

.. toctree::
   :maxdepth: 2
   
   chapter8-1
   chapter8-2
   chapter8-3
   chapter8-4
   chapter8-5

Some functions are too complicated and we have to look for ways to calculate or approximate the derivatives automatically.

**Finite Differencing.** The partial derivative of a smooth function :math:`f: \mathbb{R}^n \mapsto \mathbb{R}` with respect to the :math:`i`th variable :math:`x_i` can be approximated by the central difference formula

.. math::

   \frac{\partial f}{\partial x_i} \approx \frac{f(x + \epsilon e_i) - f(x - \epsilon e_i)}{2\epsilon}

where :math:`\epsilon` is a small positive scalar and :math:`e_i` is the :math:`i`th unit vector.

**Automatic Differentiation.** This tehnique takes the view that the computer code for evaluating the function can be broken down into a composition of elementary arithmetic operations, to which the chain rule can be applied.

**Symbolic Differentiation.** In this technique, the algebraic specification for the function :math:`f` is manipulated by symbolic manipulation tools to produce new algebriac expressions for each component of the gradient.

Derivative estimation are not only useful for optimization, but also in other areas, such as sensitivity analysis, nonnlinear differential equations, and optimization.
