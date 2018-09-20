## Brain Flux User Manual / Introduction

**1. System Overview**

Brain Flux is a big data management and analysis system developed by the cooperation of School of Medicine and School of Computer and Information at University of Pittsburgh. The goal of the system is to (1) persist brain signal data from medical practice in a large-scale data warehouse utilized by time-series database, and, (2) use the warehoused data for further R&D tasks on both medical research and database techniques improvement.  

Users of this system should be able to perform the following tasks:

* Import preprocessed time-series data into the data warehouse ([Section 3](#section_3))
* Build complicated big data analysis queries with no requirement of technical background ([Section 4](#section_4))
* Export results from previously built queries for further research ([Section 5](#section_5))

<a name="section_2"></a>**2. Architecture**

**Computing resources**: The system uses on demand, distributed computing resources from Pittsburgh Supercomputing Center for utilizing the main data warehouse. We also built up a local version of the system with the same functionality but only a fraction of data stored on it. The local version runs on a single node and can be used to test the performance of our algorithms and detect flaws in the system. Both versions of the system fully utilize the multi-threading functionality of powerful computers for a boost of performance.  
**Database**: Our choice of data warehouse is *InfluxDB*. InfluxDB is a state-of-the-art distributed time-series database with the capability of high speed read and write. All the other data, including meta-data of patients, queries built by users, warehouse version log, etc., are stored in a separate *MySQL* database for easier management.  
**Interface**: The main user interface is a web-based system written in *Java* with *Spring Framework*. *Grafana* was used as the graphics tool on visualizing data from every level of the warehouse.

<img src="https://i.imgur.com/S3aBwqT.jpg" alt="Figure" width="400">

<a name="section_3"></a>**3. Data Import**

Users can import preprocessed data from the data import page. The preprocessed data is located on the same machine where the system is deployed. This implementation is to save the time of transferring large amount of data (terabytes) before loading into the database. The data waiting to be imported could either be linked to a cluster with deployed system physically with an external hard drive, or we can simply deploy to system to the cluster containing the data source. In the latter case, the cluster just needs a high-speed internet connection and Java installed. The data warehouse, on the other hand, can be installed at any location, remotely or locally.   
Users can search local file system for desired files to be imported. Upon clicking the import button, the selected files are added into a queue for a multi-thread import process. 
 
![Figure](https://i.imgur.com/XOl7ffc.png)  

Multi-threaded data loading, in our case, gives approximately linear boost to the speed of the import processing. Considering the 36-core computer we used, when utilizing 18 cores on threads that writes into the database, each core can contribute to loading 500 ~ 900 KB/s of the preprocessed files. We can load up to 16 MB of files, or about 2 million data points per second. In the setting of our data, patients' brain signal is recorded every second. The final preprocessed file has about 6,000 columns. That means we have the potential to do real-time monitoring for more than 300 patients on a single node system. 

***[Table placeholder for import performance]***

<a name="section_4"></a>**4. Query Builder**

The query builder is the component of our system to help users with little technical background (medical experts), build up complex data analysis queries for the data warehouse to process. 

![Figure](https://i.imgur.com/Q5rkWN4.png)
![Figure](https://i.imgur.com/qlbG2fF.png)

<a name="section_5"></a>**5. Data Analysis**

