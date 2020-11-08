3.1 Introduction
=====================================

In computing the step lenght :math:`\alpha_k`, we face a tradeoff. We would like to choose :math:`\alpha_k` to give a substantial reduction of :math:`f`, but at the same time we do not want to spend too much time making the choice. The ideal choice would be the global optimizer of the univariate function :math:`\phi(\cdot)` defined by

.. math::

  \phi(\alpha) = f(x_k + \alpha p_k), \;\;\; \alpha > 0
