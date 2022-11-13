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

After generating the mesh you must now define the problem by inserting the initial freestream values like Pressure, Temperature, Mach number, etc,. In *CO*:sub:`2` solver you can even adjust the Mass fractions for all eight species. The initial values must be added in the file ``input_values.h`` located in the ``base_solver`` directory. Here is an example of some initial variables being defined in *PerfectGas* solver:

.. code-block:: c

   /*---------- PerfectGas solver-----------*/
   temp_ini = 131.70;
   Pr_ini = 199.4345;
   mach_no = 6.0;
   wall_temp = 300.00;
   R_ini = 287.00;
   rho_ini = Pr_ini/(R_ini*temp_ini);
   gamma_ini = 1.40;
   viscosity_ref = 0.00001716;
   prandtl_no = 0.71;

.. caution::

   Do not change or remove any other constant values defined in ``input_values.h`` it may cause compilation errors and the solver will not work.

.. warning::

   Should change the variable for number of iterations to ``input_values.h``.


Code Generation and Compilation
-------------------------------

To generate the solver code and run it on single/multi-core CPU's you must execute the python code and the translate the generated OP2 compliant code using the OP2 code translator and run it on the target architecture.

.. code-block:: bash

   # Generating OP2 compliant code
   python3 generate_solver.py

   # Translating the generated code
   cd code/
   make clean
   python2.7 ~/softwares/OP2-Common/translator/c/python/op2.py cfdsolver.cpp

   # Executing the Solver in sequential
   make cfdsolver_seq
   ./cfdsolver_seq


Post Processing
---------------

After the simulation is completed the solver generates the results in the ``code/results.dat`` file. The results can be post-processed using the `TecPlot 360 <https://www.tecplot.com/>`_ software or an open source software `ParaView <https://www.paraview.org/>`_.
