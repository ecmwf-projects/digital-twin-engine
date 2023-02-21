# Destination Earth Digital Twin Engine

!!! Warning
    **🚧 Work in progress!**

<div>
<p style="float: left; margin: 0 20px 0 20px;">
    <img src="destination-earth-logo.png" alt="Destination Earth Logo" width="250"/>
</p>
<p style="padding: 15px 0 10px 0;">
</p>
<p style="float: middle; margin: 0 5px 0 0px;">
    <img src="eu-logo.png" alt="EU Logo" width="250"/>
</p>
</div>

<br />
<br />

<!-- <br />

<br /> -->

Welcome to the ECMWF Digital Twin Engine documentation developers’ page. 

The European Centre for Medium-Range Weather Forecasts ECMWF is developing the Digital Twin Engine (DTE) in the frame of Destination Earth (DestinE), the ambitious initiative of the European Union to create digital twins of the Earth system.  

The DTE consists of the software infrastructure necessary for extreme-scale simulations, data fusion, data handling, and machine learning necessary to efficiently deploy and connect different digital twins with the overall DestinE platform. 

The opt-in DTE components are continuously evolving to comply with equally evolving standards on data access and data transformations and provide hooks for adaptors that facilitate interoperability. Meteorological data will comply with World Meteorological Organisation (WMO) data standards, in addition we seek to be INSPIRE compliant[<sup>1</sup>](#1), and follow as much as possible OGC standards to make location information and services FAIR – Findable, Accessible, Interoperable and Reusable. Some of the digital twin data will also comply with the directives on the availability of public datasets[<sup>2</sup>](#2). 

ECMWF  will contribute to the development and maintenance of efficient data access methods to such data and provide hooks to community-relevant connectors and be interoperable with other tools (e.g., CDO, CDS toolbox), community software platform (e.g. Pangeo) and infrastructure (Wekeo, EWC, etc.).  

Following the ECWMF 2022 software strategy, all DTE data handling and processing components are openly developed, fostering direct interactions with the community, and ensuring interoperability of standards, data formats and API’s. In addition, the development of DTE components will leverage community software stacks and contribute back to them. 

ECMWF is making available its software, with a proven track record, which is tested and continuously run in operational NWP, and is made available and further developed with community contributions to address the needs of the wider Earth System modelling and Earth observations community.   

### Intellectual Property Rights:  

This software is licensed under the terms of the Apache License Version 2.0 which can be obtained at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0). 

In applying this license, ECMWF does not waive the privileges and immunities granted to it by virtue of its status as an intergovernmental organisation nor does it submit to any jurisdiction. 

The core software has been developed by ECMWF through several projects with R&I co-funding from the European Commission.  

With the support of the European Union under the DestinE initiative, ECMWF will ensure the interoperability with the first developed DTs, will follow widely adopted standards for the DTE software development process, and consider a range of other publicly available Earth system software through the incorporation and/or development of suitable connectors. 

<!-- Enter the developers’ page [https://digital-twin-engine.readthedocs.io/en/latest/](https://digital-twin-engine.readthedocs.io/en/latest/) -->


<div>
<p style="float: right; margin: 0 5px 0 0px;">
    <img src="eu-logo.png" alt="EU Logo" width="80"/>
</p>
<p style="padding: 15px 20px 20px 20px; text-align: right;">
<i><small>This software is developed with co-funding by the European Union under the Destination Earth initiative.&nbsp;&nbsp;&nbsp;</small></i>
</p>
</div>


## Documentation

* multio [[docs](https://multio.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/multio)]
* aviso [[docs](https://pyaviso.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/aviso)]
* polytope [[docs](https://polytope.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/polytope-client)]
* pyfdb [[docs](https://pyfdb.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/pyfdb)]
* atlas [[docs](https://sites.ecmwf.int/docs/atlas), [repo](https://github.com/ecmwf/atlas)]
* pyflow [[docs](https://pyflow-workflow-generator.readthedocs.io/en/latest/), [repo](https://github.com/ecmwf/pyflow)]

> **🚧 Full docs coming soon:**

* ecflow [[docs](https://ecflow.readthedocs.io/en/latest/index.html), [repo](https://github.com/ecmwf/ecflow)]
* fdb [docs, [repo](https://github.com/ecmwf/fdb)]
* infero [[docs](https://infero.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/infero)]
* pgen [[docs](https://pgen.readthedocs.io/en/latest/), [repo](https://github.com/ecmwf/pgen)]
* plume [[docs](https://plume-plugin-mechanism.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/plume)]

## The DTE in Destination Earth

This diagram illustrates how the Digital Twin Engine components are deployed on EuroHPC machines and connected infrastructure-as-a-service in Destination Earth.

![DTE diagram](diagram.png)

## Components

### multio [[docs](https://multio.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/multio)]

**multio** is a library providing an I/O server for distributed HPC jobs, post-processing pipelines and I/O multiplexing. It provides an asynchronous system for aggregating data distributed across compute nodes into global data objects. It uses the associated metadata to route the data through configurable data processing pipelines, both pre- and post-aggregation. These pipelines can be configured to perform on-the-fly post-processing, as well as forwarding the data (or post-processed output) to a selection of downstream data consumers, including the **fdb**. 

### aviso [[docs](https://pyaviso.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/aviso)]

**aviso** is a notification service, primarily used for notifying downstream systems or users of the availability of new data – for example, notifying when a step of a DT is complete. The interface to **aviso** allows listening for notifications based on a metadata query. When data becomes available, a notification is posted with the full metadata of the available data, such that it can be retrieved via **fdb** or **polytope**. This allows the construction of data-centric workflows using the other DTE components.

### polytope [[docs](https://polytope.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/polytope-client)]

**polytope** is a horizontally scalable service which provides a datacube access API over HTTPS. Its purpose within Destination Earth is to serve the data stored in the **fdb**. **polytope** implements access control and is also capable of federating access to data across different data centres. **polytope** contains novel algorithms for performing feature extraction from datacubes, allowing direct subsetting of high-density data per user requests.

### fdb [docs, [repo](https://github.com/ecmwf/fdb)] 

The **fdb** is a domain-specific object store for meteorological data described by a curated schema of scientifically meaningful metadata. In destination earth, **fdb** acts as a high-performance data sink for digital twins, enabling writing of large amounts of data efficiently whilst simultaneously indexing the data and making it available to concurrently running consumers. The **fdb** is used as a rolling archive for full, high-resolution output of digital twins on HPC, and is also used as a large capacity, long-term indexed store of meteorological data.

### pyfdb [[docs](https://pyfdb.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/pyfdb)]

**pyfdb** is the Python interface to **fdb**.

### atlas [[docs](https://sites.ecmwf.int/docs/atlas), [repo](https://github.com/ecmwf/atlas)]

**atlas** is an open source library providing grids, mesh generation, and parallel data structures targetting numerical weather prediction or climate model developments.

### pyflow [[docs](https://pyflow-workflow-generator.readthedocs.io/en/latest/), [repo](https://github.com/ecmwf/pyflow)]

**pyflow** is a high level Python interface to **ecflow** allowing the creation of suites in an efficient and “pythonic” way. **pyflow** acts both as a compiler and a library for **ecflow** definition files which generate suites.

### ecflow [[docs](https://ecflow.readthedocs.io/en/latest/index.html), [repo](https://github.com/ecmwf/ecflow)]

**ecflow** is a client/server workflow package that enables users to run a large number of programs (with dependencies on each other and on time) in a controlled environment. It provides tolerance for hardware and software failures, combined with restart capabilities. It can used to orchestrate Digital Twins, as well as their data handling and post-processing tasks, across a range of platforms.

### infero [[docs](https://infero.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/infero)]

**infero** is a machine learning support library that runs a pre-trained machine learning model for inference. **infero** provides a common interface to multiple inference engines and can be called from multiple languages (C/C++, Fortran, Python). **infero** requires a relatively small dependency stack and is therefore also suitable for tightly-managed HPC environments.

### pgen [[docs](https://pgen.readthedocs.io/en/latest/), [repo](https://github.com/ecmwf/pgen)]

**pgen** is a parallel execution framework designed to perform post-processing on model output. **pgen** is configured with downstream (user) data requirements, which specify what post-processing should be applied to which elements of the output. This post-processing may take the form of interpolation of the data to a different resolution, along with rotations and/or regional subselections. Typically one **pgen** instance is started for each step of the model output, once it has been made available by all instances of the model. Each instance consists of one broker task, and a number of worker tasks to whom the work is distributed. They retrieve data from the **fdb** according to the specified metadata and write data to the parallel filesystem as required. 

### plume [[docs](https://plume-plugin-mechanism.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/plume)]

**plume** (**plu**gin **me**chanism) allows Earth System models to load plugins dynamically. **plume** offers APIs for controlling the loading mechanism and transferring data from the model to the plugins. A plugin can read input data generated by the model and implement specific calculations and analysis, providing a high-level of modularity and flexibility. plume plugins benefit from access to internal data of the Earth System model, which may not ever be written to **multio** and **fdb**.



## Contact

 * Tiago Quintino
 * Simon Smart
 * James Hawkes

*(firstname.lastname@ecmwf.int)*

<a name="1"></a> [1] [https://inspire.ec.europa.eu/training/inspire-data-specifications](https://inspire.ec.europa.eu/training/inspire-data-specifications)

<a name="2"></a> [2] [https://digital-strategy.ec.europa.eu/en/news/commission-defines-high-value-datasets-be-made-available-re-use](https://digital-strategy.ec.europa.eu/en/news/commission-defines-high-value-datasets-be-made-available-re-use)
