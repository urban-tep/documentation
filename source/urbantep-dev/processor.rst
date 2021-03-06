Processor concepts
------------------

There are three concepts that may need to be defined in order to avoid misuderstandings: Earth observation data product, Earth observation data product sets, and Earth observation data processors.

- An Earth observation data product - product for short - is a single file or a group of files that together form one observation, usually in raster format. One product can be one granule of an acquisition, e.g. 5 minutes of a swath, a full orbit, or a tile of a certain extent, or whatever granularity has been selected for the respective product type and mission. Note that in some communities "product" is used like "product type" in our definition.

- A product set is a collection of products. The collection may be identified by a name, or by enumerating the products, or by specifying criteria - often product type, time range, and spatial coverage. When requesting processing at a processing centre inputs are product sets, and the outputs of processing are product sets as well. The product set may contain a single product in particular cases.

- An Earth observation data processor - processor for short - in its simplest form is a software item that when applied to a single Earth observation product (file) generates a single output. This output usually is a higher level product. Processors are called, i.e. started, for each input by a "framework". This differs from the approach where "processor" is a "service" that runs forever and from time to time gets requests to be processed.

Processors in this definition are functional units that can be called for a single input and produce the output, using optionally auxiliary data that comes with the processor, but only write to the current working directory to store intermediate data and also the processing result. They do not else modify their environment, in particular not the software itself. They shall not write anything into the software installation directories or "databases" outside the allocated working directory. Make sure for your own processors that they follow this understanding. 

If you in addition obey the rule that the processor software shall be relocatable, i.e. does not depend on absolute paths, but rather use $(dirname $0) in scripts to find the installation location of the software and necessary auxiliary data, then it can easily be deployed in a processing centre and applied concurrently.

