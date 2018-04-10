# Proposal for PSC Virtual Machines

## Form questions

This is the questions on the web form.

### How you will use this VM?

We want to run a specialized database (maybe clusters) to store some medical data, and we also have a web ui for other researchers to operate on.

For now I think we have about 20TB of data, the database itself has a compression ratio of 40%. We have to import the raw data into the database for the initial stage, then we will delete the raw data. The database’s files will remain in the file system.

### List any software that needs to be installed.

A fresh installed Debian 9 OS would be enough, we will take care of the softwares ourself.

### Estimate your storage requirements

> Please list:
> - What type of data will be used: a database? large files? etc.
> - Estimated space required for each type
> - Estimated space requirements for installed software

We will use a database, which may take 20TB of storage space. A temperatory space (~2TB) for transferring. Softwares will take about 10G.

### How many cores do you need?

> 1 core comes with 4G RAM

### Do you have any specific configuration requests?

VMs should have a fast storage system.

## Our plans
