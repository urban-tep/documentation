Building your own processor package
-----------------------------------

For building you own processor package you may follow the example in structure and steps:

- Create an empty directory corresponing to ~/example . You may use your package name for it, but it does not matter.
- Create a subdirectory with the name <package>-<version> and place all your software and auxiliary data into it in a directory tree. This will be available at runtime in the same structure.
- Unless you have a script that calls the processor with a single input, add one to your software. This is the "processor".
- Test your processor locally if it can be run in the CentOS VM. If you need to install additional software packages, note them down for the Dockerfile if they are required at runtime.
- Write a Dockerfile and test your processor using docker build and docker run.
- Write a descriptor.xml file. 

Input datasets available in the processing centres comprise at least Sentinel-2 Africa+selected urban areas, Landsat, and MERIS Level 1. Other datasets available in the processing centres can be provided for processing on request. In the descriptor.xml file you refer to an input product type your processor is able to process. The product types that correspond to the datasets are:

- S2_L1C
- Landsat8_L1
- MERIS_L1B

Processor parameters that users can select shall be described in the descriptor.xml file. This allows the portal to generate a form for users to specify values for these processor parameters. At runtime, the key-value pairs of the parameters filled by the user (submitter of the request) are provided to the processor in an additional parameter file. The processor will get called with the path to the product input as first command line argument and to a processor parameter file as second command line argument. This processor parameters file contains lines with key-value pairs separated by '='. It can be source'd in the script to convert the parameters into environment variables, or forwarded to a Java application as property file.

The parameter file may look like the following:

.. code::

   threshold=0.2
   someotherparameter=A

The processor may look like the following:

.. code::

   #!/bin/bash

   input=$1
   parameter_file=$2

   if [ "$parameter_file" != "" ]; then
       . $parameter_file
   fi

   # from now on we have access to the parameters as shell variables $threshold and $someotherparameter ...
   ...
