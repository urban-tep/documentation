Example processor
-----------------

The development environment contains one processor example as a template how local test, packaging and upload to a processing centre can be performed. You can copy this example into your home directory of the VM with

   /urbantep/software/urbantep-dev/bin/setup-example.sh

The result is a directory called example with the following content:

.. figure:: urbantep-dev-example-processor.png
   :scale: 65
   :align: center

   Example processor Fmask with some wrapper scripts and package information

- Fmask is the executable - It requires Matlab runtime
- run_fmask.sh is the wrapper script that comes with Fmask
- merge-graph.xml is the SNAP GPT graph that merges the output of Fmask as one band into the Landsat product
- fmask-and-merge.sh is the wrapper script that calls Fmask and SNAP in sequence
- Dockerfile declares Linux package dependencies of the processor
- descriptor.xml declares environment and parameterisation of the processor for deployment

fmask-and-merge.sh is the processor that shall be applied to Landsat-8 inputs. It is shown here mainly for illustration. Your own processors may look different. The processor will be called with the path to the Landsat-8 input file as command line argument. The processor finally uses a tagged line in stdout (OUTPUT_PRODUCT) to inform about the filename of the result.

.. code:: bash

   urbanuser@urbandev:~ $ cat /urbantep/software/urbantep-dev/example/fmask-3.2/fmask-and-merge.sh
   #!/bin/bash
   set -e
   
   input=$(basename $1)
   id=${input%.tar.gz}
   id=${id%.tgz}
   metadatafile=${id}_MTL.txt
   mask=${id}_MTLFmask.hdr
   output=${id}-fmask.nc
   
   wd=$(pwd)
   SNAP_DIR=/urbantep/software/snap-3.0.1
   MCR_DIR=/urbantep/software/mcr_root-v81
   FMASK_DIR=$(cd $(dirname $0); pwd)
   
   if [ ! -e $wd/$metadatafile ]; then
       echo 'unpacking tgz input ...'
       tar xf $1
   fi
   
   if [ ! -e $wd/$mask ]; then
       echo 'masking with Fmask ...'
       export MCR_CACHE_ROOT=${wd}/mcrcache
       mkdir -p ${MCR_CACHE_ROOT}
       $FMASK_DIR/run_Fmask.sh $MCR_DIR
   fi
   
   if [ ! -e $wd/$output ]; then
       echo 'merging mask into product ...'
       ${SNAP_DIR}/bin/gpt -c 4G $FMASK_DIR/merge-graph.xml -PmasterProduct=$wd/$metadatafile $wd/$mask -f NetCDF4-BEAM -t $wd/$output
   fi
   
   echo OUTPUT_PRODUCT $output

Processors are usually packaged with Docker to allow for a constant environment of the processor even in different processing centres. The Dockerfile

- identifies the operating system and version. We recommend to stick to CentOS 7 for the moment if ever possible. There may be constraints on certain processing centres which OS are allowed.
- installs additional packages required by the processor, in this case in fact required by Matlab runtime. Note that Matlab runtime and SNAP are provided as software package that will be mounted into the Docker container. Do not install it in the Docker file.

.. code::

   urbanuser@urbandev:~ $ cat /urbantep/software/urbantep-dev/example/Dockerfile 
   FROM centos:7
   RUN yum install -y libXext.x86_64 libXt.x86_64 libXmu.x86_64

The descriptor XML is a declaration that is independent of the target processing centre. It declares names and versions, the processor script to be started to run the processor, formal parameters, and dependencies.

.. code:: xml

   urbanuser@urbandev:~ $ cat /urbantep/software/urbantep-dev/example/descriptor.xml 
   <?xml version="1.0" encoding="utf-8"?>
   <utep:descriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                    xmlns:utep="http://urban-tep.eo.esa.int/schema/urban-tep-schema.xsd"
                    xsi:schemaLocation="http://urban-tep.eo.esa.int/schema/urban-tep-schema.xsd urban-tep-schema.xsd">
     <utep:processor>
       <utep:name>Fmask8</utep:name>
       <utep:executable>fmask-and-merge.sh</utep:executable>
       <utep:title>Urban TEP Fmask for Landsat 8</utep:title>
       <utep:description><p>Performs cloud detection for Landsat 8 L1 products.</p></utep:description>
       <utep:inputTypes>Landsat8</utep:inputTypes>
       <utep:parameters>
         <utep:parameter>
           <utep:name>threshold</utep:name>
           <utep:type>string</utep:type>
           <utep:description>cloud probability threshold</utep:description>
           <utep:default>0.2</utep:default>
         </utep:parameter>
       </utep:parameters>
       <utep:packaging>
         <utep:name>fmask</utep:name>
         <utep:version>3.2</utep:version>
         <utep:type>Docker</utep:type>
         <utep:dependencies>
           <utep:dependency>
             <utep:name>snap</utep:name>
           </utep:dependency>
           <utep:dependency>
             <utep:name>mcr_root</utep:name>
             <utep:version>v81</utep:version>
           </utep:dependency>
         </utep:dependencies>
         <utep:resources>
           <utep:resource>
             <utep:name>memory</utep:name>
             <utep:value>7000</utep:value>
           </utep:resource>
           <utep:resource>
             <utep:name>timelimit</utep:name>
             <utep:value>3600</utep:value>
           </utep:resource>
         </utep:resources>
       </utep:packaging>
     </utep:processor>
   </utep:descriptor>

The elements of this descriptor.xml file content are:

- name is the displayed name of the processor.
- executable is the script to be started to run the processor
- title and description are explanatory information for users of the processor
- inputTypes is a comma-separated list of product types, one or several of Landsat8, S2, MERIS
- the parameter structure with name, type, description and default declares parameters of the processor. The threshold parameter is provided here for illustration purposes. It is not an actual externally accessible parameter of Fmask. Always use string for all types of parameters for the moment.

- packaging name and version are the identifying information for the software package that contains the processor
- Docker for the moment is the package type supported by all processing centres. Other types (SNAP, BEAM) may be supported by particular processing centres.
- dependencies shall list the software packages that shall be mounted into the Docker container. The packages are those are made available in the development VM locally in /urbantep/software/<package>-<version>/ . Later versions of the development VM may come with additional packages. The same packages are available in the processing centres and will be made available to the Docker container at runtime. 

- The resource "memory" for the processing of a single input product can be configured in MB. The default and upper limit is processing-centre dependent. It may be around 2024 MB. A high value restricts concurrency but may be required for certain processors.
- The resource "timelimit" for the processing of a single input product can be configured in seconds. The default and upper limit is processing-centre dependent. It may be around 600 seconds. Processors requiring more than this time may be aborted automatically. Too high values may use up a lot of resources in case the processor has no internal clock and limitation.

