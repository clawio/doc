# Introduction

ClawIO is a live prototype implementation of a high scalable, flexible and standard-based synchronization and sharing platform.

This project is part of the R&D process of my bachelor thesis about  [CERNBox: Petabyte-scale synchronization and sharing service](https://github.com/labkode/tfg/raw/master/tfg.pdf) 

## Why ClawIO?

Cloud computing introduces a different way of communicate with computer services, from email communications to the usage of social networks. 

With this paradigm the heavy and hard job has been moved from the client to remote servers,
converting the client into a thin client promoting for mobility and
network pervasiveness. 

Cloud storage is a special type of cloud service
with the primary goal of providing a pervasive and coherent access to data from a variety of devices.

The usage of cloud storage services like DropBox has been very successful because they provide a convenient way for people to synchronize and share their data across different devices. 

The adoption of these proprietary solutions has some potential problems:

* Off-premise deployments: data is outside the control of your
  organization with unclear business and security policies.

* Closed source code: the application logic is hidden, without the
  possibility to customize or optimize the code.

* Unclear service level: the data confidentiality and jurisdiction may
  be in risk.

To handle these problems, in the last five years, some open source
solutions came to play the sync and share game. The most popular
products are OwnCloud, SeaFile, PowerFolder and Pydio, which provide open source and on-premise solutions to online cloud storage.

These products offer the sync and share layer in top of different storage back ends like local storage, network storage like NFS or object storage like Amazon S3 or OpenStack Swift, among others.

None of these products offer a high-performance integration with a petabyte-scale storage backend.

The only actual solution to this problem is the[ CERNBox project](http://cernbox.web.cern.ch/).

I am one the main developers of the CERNBox project, and my main job is the integration of the OwnCloud Web Server with [EOS](http://eos.readthedocs.org/en/latest/), the CERN multi-petabyte storage.  

After the successful creation and service launch of the CERNBox project, some architectural problems have been found in the core of the OwnCloud Web Server.

To understand more about the integration problems and the solution provided with CERNBox, read my thesis: [CERNBox: Petabyte-scale synchronization and sharing service](https://github.com/labkode/tfg/raw/master/tfg.pdf).

ClawIO goes beyond CERNBox, taking the ideas and design optimizations from it to create a live prototype of a higher scalable synchronization and sharing server.

The goals to achieve with this project are three:

1. **Provide a high scalability sync and share server on top of modern storages**
2. **Provide a flexible architecture to be used by a variety of modern storages without lossing scalability**
3. **Be a reference implementation for future sync and share standars that are being created nowadays**


## LICENSE

ClawIO project is published under the  AGPLv3 license.

## Contribute to this manual

The source code of this manual is hosted on Github, feel free to contribute at  https://github.com/clawio/doc

## Contact information

* Twitter: [@clawio](https://twitter.com/clawio)
* Email: [hugo@clawio.co](mailto:hugo@clawio.co)

## DISCLAIMER
**The only working solution to provide a high scalable sync and share service nowadays is CERNBox, using OwnCloud and EOS**