# The storages

There are different types of storages and the goal of ClawIO is to be flexible to be able to use all of them independent of their architecture.

The perfect storage for a sync and share server is the one that provides the following features built-in:

* **Data storage**
* **Namespace**
* **Unique resource ID**
* **Propagation of changes in the namespace**

ClawIO is very flexible and will adapt its architecture depending of the features offered by the storages.

## Data store

The data storage is the component of the storage responsible for interacting the data.

## Namespace (Metadata store)

The namespace, file catalog or metadata store is the component responsible for the handling of the metadata of all the resources inside the data storage.

It usually keeps track of the hierarchy of the resources and extra information like modification time, checksum, size ...

## Unique Resource ID

For being able to scale every storage must provide a unique resource ID for every resource inside the storage.

This is required to handle remote moves in the synchronization client to avoid a **delete + upload** operation.

If the storage does not provide this unique ID, you need to have a component on top of your storage that provides it.

## Propagation of changes in the namespace

When a file is modified, its modification (mtime, ETag or custom attribute) must be propagated botom-up to the top level directory to help the synchronization client to scale (avoiding the recursive traversal of all the namespace for discovering changes).

If your storage does not provide this feature, you need to have a component on top of your storage that provides it.

## Comparison table of storage backends

|  | Data store| Namespace | Unique Resource ID | Propagation of changes 
| -- | -- | -- | -- | -- |
| Local Storage | ✔ | ✔ |  ✗ | ✗ |
| Amazon S3 | ✔ | ✗ | ✗ | ✗ |
| EOS | ✔ | ✔ | ✔ | ✔ |
