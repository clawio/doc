# Storage Classification

There are different types of storages and the goal of ClawIO is to be flexible to be able to use all of them independent of their architecture.

The perfect storage for a sync and share server is the one that provides the following features built-in:

* **Data store**
* **Namespace (Metadata store)**
* **Unique resource ID for all resources within the namespace**
* **Propagation of resource modification botom-up in the namespace**

ClawIO is very flexible and will adapt its architecture depending of the features offered by the storages.

## Data store

The data store is the component of the storage responsible for keeping and serving the binary data.

## Namespace (Metadata store)

The namespace, metadata store or file catalog is the component responsible for the handling of the metadata of all the resources inside the data storage.

It usually keeps track of the hierarchy of the resources and extra information like modification time, checksum, size ...

## Unique resource ID for all resources within the namespace

For being able to scale every storage must provide a unique resource ID for every resource inside the storage.

This is required to handle remote moves in the synchronization client to avoid a **delete + upload** operation.

If the storage does not provide this unique ID, you need to have a component on top of your storage that provides it.

## Propagation of resource modification botom-up in the namespace

When a resource is modified, its modification must be propagated botom-up to the top level directory to help the synchronization client to scale (avoiding the recursive traversal of all the namespace for discovering changes).

Usually, the attributes used for reflecting the modification of a resource are the mtime (modification time) or ETag, but a custom one can be used also.

If your storage does not provide this feature, you need to have a component on top of your storage that provides it.

## Comparison table of storage backends

|  | Data store| Namespace | Unique Resource ID | Propagation of changes 
| -- | -- | -- | -- | -- |
| Local Storage | ✔ | ✔ |  ✗ | ✗ |
| Amazon S3 | ✔ | ✗ | ✗ | ✗ |
| EOS | ✔ | ✔ | ✔ | ✔ |
