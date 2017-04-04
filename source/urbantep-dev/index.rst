Urban TEP Processor Development Environment
===========================================

The Urban TEP processor development environment is a virtual machine with CentOS and some pre-installed Earth observation data and applications, among them tools for packaging and upload of processors to processing centres.

.. figure:: urbantep-dev-concept.png
   :scale: 65
   :align: center

   Development VM and processing centre for local test, deployment, and application

Develop and test your own processor in this VM, describe parameters and calling convention in a processor descriptor XML file, and package and upload it to one of the Urban TEP processing centres for concurrent application on large datasets. The VM may be hosted in the cloud of a processing centre or locally in a virtual box of your desktop machine.

.. toctree::
   :maxdepth: 1
   
   Processor concepts <processor>
   Obtaining and starting the VM <vm>
   Test data <data>
   Installed applications and tools <apps>
   Example processor <example>
   Local processor test <test>
   Packaging and upload <upload>
   Building your own processor <userprocessor>

