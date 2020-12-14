7.4 Algorithms for Partially Separable Functions
=====================================

In a **separable** unconstrained optimization, the objective function can be decomposed into a sum of simpler functions that can be optimized independently.

.. math::

   f(x) = f_1(x_1, x_3) + f_2(x_2, x_4, x_6) + f_3(x_5)

The cost of performing :math:`m` lower-dimensional optimizations is much less in general than the cost of optimizing an :math:`n`-dimensional function.

In many large problems, the objective function :math:`f: \mathbb{R}^n \to \mathbb{R}` is not separable, but it can still be written as the sum of simpler function, known as **element functions**. Each element function has the property that it is unaffected when we move along a large number of linearly independent directions. If this property holds, we say that :math:`f` is partially separable. All functions whose Hessian :math:`\nabla^2 f` are sparse are partially separable, but so are many functions whose Hessian is not sparse.

The simplest form of partial separability arises when the objective function can be written as

.. math::

   f(x) = \sum_{i=1}^{ne} f_i(x)

where each of the element functions :math:`f_i` depends on only a few components of :math:`x`. It follows that the gradients :math:`\nabla f_i` and Hessian :math:`\nabla^2 f_i` of each element function contain just a few nonzeros. We obtain

.. math::

   \nabla f(x) = \sum_{i=1}^{ne} \nabla f_i(x), \;\;\; \nabla^2f(x) = \sum_{i=1}^{ne} \nabla^2 f_i(x)

It is more effective to maintian quasi-Newton approximations to each of the element Hessians :math:`\nabla^2 f_i(x)` separably, rather than approximating the entire Hessian :math:`\nabla^2f(x)`.
