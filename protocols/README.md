# Protocols

One goal of ClawIo is being a reference implementation to future synchronization and sharing protocols.

In the moment of this writing, none of the following have a specification draft.

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

* [OpenCloudMesh](opencloudmesh.md)