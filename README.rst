ConjugateGradients
==================

Implementation of Conjugate Gradient method for solving systems of linear equation using Python, C and Nvidia CUDA.
Currently only Python implementation is available - it includes Conjugate Gradient Method and Preconditioned Conjugate Gradient with Jacobi
pre-conditioner (hopefully others will be added as well).

Getting Started
---------------

::

    $ git clone https://github.com/stovorov/ConjugateGradients
    $ cd ConjugateGradients


Python implementation
---------------------

Prepare environment
~~~~~~~~~~~~~~~~~~~

::

    $ source run_me.sh (sets PYTHONPATH)
    $ cd scripts
    $ make venv
    $ source venv/bin/activate
    $ make test


Usage
~~~~~

.. code:: python

    from scripts.ConjugateGradients.utils import get_test_matrix_three_diagonal, get_solver
    import numpy as np

    matrix_size = 100
    a_matrix = get_test_matrix_three_diagonal(matrix_size)
    x_vec = np.vstack([1 for x in range(matrix_size)])
    b_vec = np.vstack([uniform(0, 1) for x in range(matrix_size)])
    CGSolver = get_solver('CG')
    cg_solver = CGSolver(a_matrix, b_vec, x_vec)
    x_vec, residual_vec = cg_solver.solve()

You can view convergence profile using solver's ``show_convergence_profile`` method:

    .. image:: doc/cg_conv_visual.png
        :height: 200 px
        :width: 200 px
        :scale: 50 %

You can compare convergence profiles of difference solvers using ``compare_convergence_profiles`` method:

    .. image:: doc/comparison.png
        :height: 200 px
        :width: 200 px
        :scale: 50 %

Examples can be found in ``scripts/ConjugateGradients/demo.py``


C implementation - TBA
----------------------

CUDA implementation - TBA
-------------------------

Conjugate Gradients description
-------------------------------

A bit about Conjugate Gradients and when it actually works (collection of information found over internet):

CG will work when is applied on symmetrical and positively defined matrix.

``CG is equivalent to applying the Lanczos algorithm on the given matrix with the starting vector given by the (normalized)
residual of the initial approximation.``
source: https://math.stackexchange.com/questions/882713/application-of-conjugate-gradient-method-to-non-symmetric-matrices

Resources:
~~~~~~~~~~

General overview and derivation is described on Wiki:
https://en.wikipedia.org/wiki/Derivation_of_the_conjugate_gradient_method

Though this description has a lot of shortcuts and will probably leave you with a more questions then before reading it...

A good description can be found in ``Painless Conjugate Gradient``:

https://www.cs.cmu.edu/~quake-papers/painless-conjugate-gradient.pdf
A bit complex work but worth reading (but requires a lot of focus...at least from me...).

A lot about ``preconditioning`` could be found here:
http://netlib.org/linalg/html_templates/node51.html
haven't read everything but may explain a lot (still, will probably leave you with a lot of questions...).