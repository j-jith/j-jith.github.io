.. title: Software Projects
.. slug: software
.. date: 2018-01-23 08:17:51 UTC+05:30
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Model order reduction framework for second-order system with frequency dependent (non-viscous) damping
------------------------------------------------------------------------------------------------------

- Fast frequency sweep of second-order systems arising from
  structural dynamics, fluid-structure interactions, etc.

- Computationally efficient error estimate for determining
  appropriate order of ROM

- Parallel execution through `PETSc`_ and MPI. Source code
  available on request.

FEM solver for visco-thermal acousto-elastic interaction studies
----------------------------------------------------------------

- Frequency sweep of acousto-elastic problems considering viscosity
  and thermal conductivity of the fluid

- FE assembly using Python based `FEniCS`_ framework, and linear
  algebra using `PETSc`_. Source code available on request.

`pythermophy`_
--------------

- Package for computing thermo-physical properties of real fluids

- Fluids modelled using cubic (RK, SRK, PR) or Lee-Kesler equations
  of state

- Calculates properties like density, speed of sound, heat
  capacities, isothermal compressibility, etc.

`OrthoPoly`_
------------

- Package for generating orthogonal polynomials with respect to arbitrary probability densities

- Generates orthogonal polynomials for use in uncertainty
  quantification studies using Polynomial Chaos Expansion (PCE)

- Can handle random variables with arbitrary probability density
  functions

- Determines quadrature points and weights for numerical integration
  with respect to generated polynomials

----

For more, please visit my GitHub page - `@j-jith <https://github.com/j-jith>`_.


.. _pythermophy: https://github.com/j-jith/pythermophy

.. _OrthoPoly: https://github.com/j-jith/orthopoly

.. _FEniCS: https://fenicsproject.org/

.. _PETSc: https://www.mcs.anl.gov/petsc/
