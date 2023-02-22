# Documentation

!!! Warning
    **🚧 Work in progress!**

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