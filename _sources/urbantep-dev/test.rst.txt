Local processor test
--------------------

The example processor can be tested locally - first without docker container as it is able to run in CentOS. There is a README file in the urbanuser's home directory with all steps to be performed. This may be used as copy-paste template when performing the steps in a terminal.

.. code:: bash

   urbanuser@urbandev:~ $ cat ~/urbantep-dev.readme  
   VM login
   ========
   
    o user urbanuser, password urbanuser
    o either via desktop (start terminal)
    o or via ssh
    o urbantep software pre-installed in /urbantep/
   
   Example setup
   =============
   
   cd ~
   rm -r example
   /urbantep/software/urbantep-dev/bin/setup-example.sh 
   cd example
   ls -l $(find . -type f)
   
   Local processor test (without Docker)
   =====================================
   
   cd ~/example
   mkdir -p wd
   rm -r wd/*
   cd wd
   ../fmask-3.2/fmask-and-merge.sh /urbantep/eodata/LC8/v1/2014/07/03/LC81940272014184LGN00.tar.gz
   
   Local processor test (with Docker)
   ==================================
   
   cd ~/example
   mkdir -p wd
   rm -rf wd/*
   cd wd
   mkdir fmask-package-info
   cp ../Dockerfile fmask-package-info/
   echo "threshold=0.5" > parameters
   cp /urbantep/eodata/LC8/v1/2014/07/03/LC81940272014184LGN00.tar.gz .
   docker build -t urbancentos fmask-package-info
   docker run --rm=true -v /urbantep/software/snap-3.0.1:/urbantep/software/snap-3.0.1 -v /urbantep/software/mcr_root-v81:/urbantep/software/mcr_root-v81 -v /home/urbanuser/example/wd:/wd -v /home/urbanuser/example/fmask-3.2:/urbantep-fmask-3.2 -w /wd urbancentos /urbantep-fmask-3.2/fmask-and-merge.sh /wd/LC81940272014184LGN00.tar.gz /wd/parameters
   
   Packaging and upload to processing centre
   =========================================
   
   cd ~/example
   /urbantep/software/urbantep-dev/bin/package-bc.sh descriptor.xml
   /urbantep/software/urbantep-dev/bin/upload-bc.sh descriptor.xml
   /urbantep/software/urbantep-dev/bin/describeProcess-bc.sh descriptor.xml
   
   Cleaning up
   ===========
   
   cd ~
   rm -r example

The follwing figure shows the call of the processor with one of the provided inputs and its execution.

.. figure:: urbantep-dev-test-local.png
   :scale: 65
   :align: center

   Running the processor with local test data

The result can be inspected using the installed SNAP. Open the result NetCDF product in the working directory, view an RGB, open the fmask band, and split horizontally.

.. figure:: urbantep-dev-snap-fmask.png
   :scale: 65
   :align: center

   Opening and inspecting the processing result with SNAP

Next, the processor can be tested running it in a Docker container. There are two steps, docker build and docker run.

.. figure:: urbantep-dev-test-dockerbuild.png
   :scale: 65
   :align: center

   Building the Docker image

.. figure:: urbantep-dev-test-dockerrun.png
   :scale: 65
   :align: center

   Running the processor in the Docker image

.. figure:: urbantep-dev-test-result.png
   :scale: 65
   :align: center

   Inspecting the result in the working directory

We get the same NetCDF result as before. The Docker container makes sure that this is reproducible in any of the processing centres that may have different native operating system environments.

