# The storages

There are different types of storages and the goal of ClawIO is to be flexible to be able to use all of them independent of their architecture.

To provide a scalable sync and share server ClawIO behavies differently depending on the stoage used based on this three features.

The perfect storage for a sync and share server is the one that provides the following features built-in:

* **Namespace**
* **Unique resource ID**
* **Propagation of changes in the namespace**

## Namespace

The namespace or file catalog is the component reponsible for the handling of the metadata of all the resources inside the data storage.

Most of the filesystems have this concept of namespace.

For example, if you are using local storage, you are able to create a directory hierarchy and you can navigate trough it.

If you storage is object store, you only have a data store nd you need to create the namespace on top of the data store.

## Unique Resource ID

For being able to scale every storage must provide a unique resource ID for every resource inside the storage.

This is required to handle remote moves in the syncrhonization client to avoid a delete+upload operation.

If the storage does not provide this unique ID, you need to have a system on top of your storage that provides it.

## Propagation of changes in the namespace

When a file is modified, its ETag is modified, but this change must be propagated botom-up to the top level directory to help the synchronization client to scale (avoiding the traverse of all the namespace for discovering changes).

EOS is the only storage backend that provides this functionality built-in.

If your storage does not provide this feature, you need to construct an alternative on top of it.

## Comparison table of storage backends

|  | Namespace built-in | Unique Resource ID | Propagation of ETag |
| -- | -- | -- | -- |
| Local Storage | ✔ |  ✗ | ✗ |
| Amazon S3 | ✗ | ✗ | ✗ |
| EOS | ✔ | ✔ | ✔ |
