(qsm5)=

# Upload Your Own Data and Tools

These options are available only to the registered users after sign-on using your EO-SSO ID. This service is open to well-known, registered users of the U-TEP portal and to become one, you have to register with one of the U-TEP processing centres. The registration form is located on the "Develop and offer content" page.

:::{figure} includes/qsm5-f1.png
:align: center
:figclass: img-container-border
:width: 80%
:::

:::{figure} includes/qsm5-f5.png
:align: center
:figclass: img-container-border
:width: 80%
:::

The submission of the registration form generates the ticket within the platform's ticketing system. The helpdesk operator is automatically informed about the new ticket and the following use case specific communitation is performed via this ticketing system.

## Upload your data

You have the following options regarding your own dataset which you want to use on the platform:

- request upload of your dataset on the platform and make it available for all users or selected community as a new product
- request upload of your dataset on the platform and make it available for all users or selected community as a new dataset for processing (using existing processors or custom processors)
- request upload of your dataset on the platform and make it available just for your processing (using existing processors or custom processors)
- request publication of the dataset you have generated on the platform as a new product for all users or selected community

When you log into the platform you can find the appropriate request forms on the "Develop and offer content" page. To view the request forms use "Managing your own datasets" link.

:::{figure} includes/qsm5-f2.png
:align: center
:figclass: img-container-border
:width: 80%
:::

..NOTE::

: There are only two request forms regarding the uploading or publishing of a dataset. The specified use case should be described within the form or later on through the created ticket in the helpdesk system.

### Request upload of a dataset

Fill the "Requesting upload of a user-provided dataset" form to upload your dataset for the publication as a product or as a dataset for processing.

:::{figure} includes/qsm5-f3.png
:align: center
:figclass: img-container-border
:width: 80%
:::

You will be contacted by a selected processing center operator via the helpdesk system about the method of the dataset upload. The processing center operator ingests the data e.g. by harvesting it from a remote location, or by offering you an FTP drop-down point for the processing center. In the end, the help desk operator informs you about the finalisation of your request.

### Request publication of a dataset

Fill the "Requesting publication of a dataset" form to publish the dataset you have generated on the platform as a new product.

:::{figure} includes/qsm5-f4.png
:align: center
:figclass: img-container-border
:width: 80%
:::

This form creates a new ticket within the helpdesk system of the platform. When the necesarry configuration is done, the help desk operator informs you via this ticket about the finalisation of your request.

## Upload your tool

To upload your own tool you have to use the processor development environment package available on the "Develop and offer content" page.

:::{figure} includes/qsm5-f6.png
:align: center
:figclass: img-container-border
:width: 80%
:::

The whole proces of creating, uploading and publishing your own processor (tool) is described in detail in the user manual's "Processor Development Environment" tab. This process could be summarized in the following steps:

1. Download U-TEP's Virtual Machine for processor development and deployment
2. Develop, test, package and upload your processor to a processing center
3. (OPTIONAL) Request publication of your processor for use by other users
4. (OPTIONAL) Propose your processor for systematic processing

### Processor Development Environment

Donwload the VM image from the following link. It is a linux VM that comes with the a graphical user interface providing you the tools to create your own processor, test it locally within the VM and upload it to a selected processing center to make it available on the platform just for you or also for other users.

:::{figure} includes/qsm5-f7.png
:align: center
:figclass: img-container-border
:width: 80%
:::

Copy the content of the virtual machine image directory to a local directory on your machine. Unless done, install Oracle Virtual Box on your machine. Start the VM and log-in using the "**urbanuser**" password for the default username.

### Develop, test, package and upload your processor

The desktop of the Urban-TEP VM shows some icons of pre-installed applications:

- Terminal, used for local processor tests, packaging, upload
- Web browser
- Sentinel Toolbox SNAP
- **urban-dev.readme** with tutorial instructions for an example processor

:::{figure} includes/qsm5-f8.png
:align: center
:figclass: img-container-border
:width: 80%
:::

The Urban TEP processor development VM comes with a few Earth observation products from different missions and sensors. The test data is located in directory **/urbantep/eodata/\<type>** in the virtual machine:

- Sentinel 2 L1C subset
- Landsat 8 OLI+TIRS
- ENVISAT MERIS

The development environment contains one processor example as a template how local test, packaging and upload to a processing centre can be performed. You can copy this example into your home directory of the VM with **/urbantep/software/urbantep-dev/bin/setup-example.sh**.

The result is a directory called example with the following content:

- Fmask is the executable - It requires Matlab runtime
- run_fmask.sh is the wrapper script that comes with Fmask
- merge-graph.xml is the SNAP GPT graph that merges the output of Fmask as one band into the Landsat product
- fmask-and-merge.sh is the wrapper script that calls Fmask and SNAP in sequence
- Dockerfile declares Linux package dependencies of the processor
- descriptor.xml declares environment and parameterisation of the processor for deployment

Processors are usually packaged with **Docker** to allow for a constant environment of the processor even in different processing centres. The **descriptor XML** is a declaration that is independent of the target processing centre. It declares names and versions, the processor script to be started to run the processor, formal parameters, and dependencies.

```xml
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
```

The example processor can be tested locally with or without the docker container. There is a **README** file in the urbanuser’s home directory with all steps to be performed. The result can also be inspected using the installed SNAP by opening the result NetCDF product in the working directory of the example processor.

> :::{figure} includes/qsm5-f9.png
> :align: center
> :figclass: img-container-border
> :width: 80%
> :::

After the successful local test the processor can be **packaged** and **uploaded** to a processing centre for deployment and later application to larger datasets. The same way an updated processor can be installed to supersede a previously installed processor version (with explicit versioning, you are responsible for version numbers yourself).

**Upload tool requires user name and password of a well-known user of the respective processing centre.**

Brockmann Consult processing center

- use **package-bc.sh** to package the content of the processor to a .zip file
- use **upload-bc.sh** to upload the packed processor to a Brockmann Consult processing center
- use **describeProcess-bc.sh** to verify the deployed processor within the processing center

IT4Innovations processing center

- use **package-it4i.sh** to package the content of the processor to a .zip file
- use **upload-it4i.sh** to upload the packed processor to a IT4Innovations processing center
- use **describeProcess-it4i.sh** to verify the deployed processor within the processing center

After the successful upload, the processor should be available directly on the platform in the "**Test my processor**" thematic application.

:::{figure} includes/qsm5-f10.png
:align: center
:figclass: img-container-border
:width: 80%
:::

All uploaded processors are listed in the "Services" tab in "Test my processor" thematic application.

:::{figure} includes/qsm5-f11.png
:align: center
:figclass: img-container-border
:width: 80%
:::

### Request publication of your processor

If you want to publish your processor for all users or just selected community, you can do it via the request form on the "Develop and offer content" page. This form will initiate new ticket in the helpdesk system. The help desk operator informs you about the finalisation of your request.

:::{figure} includes/qsm5-f12.png
:align: center
:figclass: img-container-border
:width: 80%
:::

### Propose your processor for systematic processing

If you want your custom processor to systematically generate the data, you need to submit an appropriate request form on the "Develop and offer content" page. This form will initiate new ticket in the helpdesk system. The help desk operator informs you about the finalisation of your request.

:::{figure} includes/qsm5-f13.png
:align: center
:figclass: img-container-border
:width: 80%
:::
