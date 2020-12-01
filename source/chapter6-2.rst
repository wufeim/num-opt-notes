6.2 The SR2 Method
=====================================

There is in fact a simpler rank-1 update for :math:`B_k` that maintains symmetry of the matrix and allows it to satisfy the secant equation. However, this **symmetric-rank-1**, or SR1, update does not guarantee that the updated matrix maintains positive definiteness.

The symmetric rank-1 update has the general form

.. math::

  B_{k+1} = B_k + \sigma vv^\top

where :math:`\sigma = \pm 1` and :math:`\sigma` and :math:`v` are chosen so that :math:`B_{k+1}` satisfies the secant equation :math:`y_k = B_{k+1}s_k`.
