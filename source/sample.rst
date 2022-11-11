Generating a uFVM Solver
========================

This page provides a tutorial in the basics of simulating an unstructured-mesh configuration using uFVM solvers. The process of initializing and running a simulation in both *PerfectGas* and *CO*:sub:`2` solvers is identical.


Unstructured-Mesh
-----------------

First you should create an unstructured-mesh for a desired geometry that you are willing to study. We primarily used an open source application named `Gmsh <https://gmsh.info/>`_ which generates a mesh file with ``.msh`` extention and created a parser which takes the standard output file from Gmsh and converts it into an unstructured-mesh file with ``.dat`` extention.

The solver only accepts a mesh file with name ``grid.dat`` and should be located in the same directory along with the source code. There are various ways in which we generate an mesh, these are mentioned in `Mesh Generation <gridgen>`_.

.. note::

   A sample unstructured-mesh is given in the source code to make things easier at the start.


Freestream Conditions
---------------------


Code Generation and Compilation
-------------------------------


Post Processing
---------------

