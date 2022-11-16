# ECMWF's Digital Twin Engine

!!! Warning
    **🚧 Work in progress!**

The Digital Twin Engine is a collection of components built to facilitate the implementation of Digital Twins. These components are developed by ECMWF as part of Destination Earth.

## Documentation

* multio [[docs](https://multio.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/multio)]
* aviso [[docs](https://pyaviso.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/aviso)]
* polytope [[docs](https://polytope.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/polytope-client)]
* pyfdb [[docs](https://pyfdb.readthedocs.io/en/latest), [repo](https://github.com/ecmwf/pyfdb)]
* atlas [[docs](https://sites.ecmwf.int/docs/atlas), [repo](https://github.com/ecmwf/atlas)]

> **🚧 Full docs coming soon:**

* ecflow [[docs](https://ecflow.readthedocs.io/en/latest/index.html), [repo](https://github.com/ecmwf/ecflow)]
* fdb [docs, [repo](https://github.com/ecmwf/fdb)]
* infero [[docs](https://infero.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/infero)]
* pgen [[docs](https://pgen.readthedocs.io/en/latest/), [repo](https://github.com/ecmwf/pgen)]
* plume [[docs](https://plume-plugin-mechanism.readthedocs.io/en/latest), [repo](https://github.com/ecmwf-projects/plume)]

## Components

### multio

**multio** is a library providing an I/O server for distributed HPC jobs, post-processing pipelines and I/O multiplexing. It provides an asynchronous system for aggregating data distributed across compute nodes into global data objects. It uses the associated metadata to route the data through configurable data processing pipelines, both pre- and post-aggregation. These pipelines can be configured to perform on-the-fly post-processing, as well as forwarding the data (or post-processed output) to a selection of downstream data consumers, including the FDB. 

### aviso

**aviso** is a notification service, primarily used for notifying downstream systems or users of the availability of new data – for example, notifying when a step of a DT is complete. The interface to **aviso** allows listening for notifications based on a metadata query. When data becomes available, a notification is posted with the full metadata of the available data, such that it can be retrieved via **fdb** or **polytope**. This allows the construction of data-centric workflows using the other DTE components.

### polytope

**polytope** is a horizontally scalable service which provides a datacube access API over HTTPS. Its purpose within Destination Earth is to serve the data stored in the FDB. **polytope** implements access control and is also capable of federating access to data across different data centres. **polytope** contains novel algorithms for performing feature extraction from datacubes, allowing direct subsetting of high-density data per user requests.

### fdb/pyfdb

The **fdb** is a domain-specific object store for meteorological data described by a curated schema of scientifically meaningful metadata. It acts as a high-performance data sink within the HPC, enabling the model to write out large amounts of data efficiently whilst simultaneously indexing the data and making it available to concurrently running consumers. The FDB then acts as a rolling archive, such that the full, high-resolution output of the last few cycles (subject to available resources) of the model are made available to all consumers directly. The **fdb** can also be used as a large capacity, long-term indexed store of meteorological data. **pyfdb** is the Python interface to **fdb**.

### atlas

**atlas** is an open source library providing grids, mesh generation, and parallel data structures targetting Numerical Weather Prediction or Climate Model developments.

### ecflow

### infero

### pgen

**pgen** is a parallel execution framework designed to perform post-processing on model output. **pgen** is configured with downstream (user) data requirements, which specify what post-processing should be applied to which elements of the output. This post-processing may take the form of interpolation of the data to a different resolution, along with rotations and/or regional subselections. Typically one **pgen** instance is started for each step of the model output, once it has been made available by all instances of the model. Each instance consists of one broker task, and a number of worker tasks to whom the work is distributed. They retrieve data from the FDB according to the specified metadata and write data to the parallel filesystem as required. 

### plume

## Diagram

![DTE diagram](diagram.png)


## Contact

 * Tiago Quintino
 * Simon Smart
 * James Hawkes

*(firstname.lastname@ecmwf.int)*
