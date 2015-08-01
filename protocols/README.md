# Protocols

One goal of ClawIo is being a reference implementation for future synchronization and sharing protocols.

In the moment of this writing, none of the following protocols have a specification draft.

##  [MSUAP (Multi-Storage Universal Access Protocol)](msuap.md)

The Multi-Storage Universal Access Protocol is an open protocol to be used with HTTP to provide an universal access to multiple cloud storages in a scalable and flexible way.

## [OSYNCP (Open Sync Protocol)](osyncp.md)

The Open Sync Protocol will be an open protocol to allow the synchronization between different cloud storage providers in a standard way, reducing multiple implementations on client side.

The protocol will deal with these aspects:

* Chunking strategy or chunking size
* Bundling small files together
* Delayed ack mechanism
* Delta encoding
* Deduplication
* Compression

The protocol must negotiate the best strategy according to the permanent capabilities and dynamic state of the cloud storage provider.

OwnCloud synchronization protocol can be a starting point due to the protocol is storage backend agnostic and is based on WebDAV industry standard for resource manipulation + custom extensions.

Documentation of the OwnCloud sync protocol has been started by Jakub Moscicki as part of the CERNBox project and can be found [here](https://github.com/cernbox/smashbox/blob/master/protocol/protocol.md).

Also, documentation for a end-to-end checksum has been elaborated by Jakub Mosciki as part of the CERNBox project and can be found [here](https://github.com/cernbox/smashbox/blob/master/protocol/checksum.md).

**ClawIO is a reference sync and share server implementation of both OwnCloud protocol and the checksuming extension.**

## [OpenCloudMesh](opencloudmesh.md)

The OpenCloudMesh Protocol is a protocol invented by OwnCloud™ to allow inter-cloud sharing between different cloud storage vendors.

Details to join the OpenCloudMesh can be found [here](https://owncloud.com/lp/opencloudmesh/).

Frank Karlitschek, CTO, Community Leader and Co-Founder of OwnCloud™, explained in a series of blog posts the concept and necessity for the OpenCloudMesh.

* [It is time to Federate our Clouds](https://owncloud.com/it-is-time-to-federate-our-clouds/)
* [The Next Generation File Sync and Share Technology ](https://owncloud.com/the-next-generation-file-sync-and-share-technology/)
* [The Federated Architecture of Next Generation File Sync and Share ](https://owncloud.com/the-federated-architecture-of-next-generation-file-sync-and-share/)

Despite the fact of being a powerful initiative, there is not yet a formal specification of the protocol.
