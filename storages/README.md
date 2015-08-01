# Storage Classification

There are different types of storages and the goal of ClawIO is to be flexible to be able to use all of them independent of their architecture.

The perfect storage for a sync and share server is the one that provides the following features built-in:

* **Data store**
* **Namespace (Metadata store)**
* **Unique resource ID for all resources within the namespace**
* **Propagation of resource modification botom-up in the namespace**
* **ACL support**


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

## ACL Support

ACL Support is the capability of a storage backend to protect resources using individual and group permissions.

Modern storage backends like EOS or Amazon S3 offer this feature.

Some local storages like the ones based on  [UFS](https://www.freebsd.org/doc/handbook/fs-acl.html) offer it also.

## Comparison table of storage backends for sync and share purposes

|  | Data store| Namespace | Unique Resource ID | Propagation of changes | Storage ACL
| -- | -- | -- | -- | -- | -- |
| Local Storage | ✔ | ✔ |  ✗ | ✗  | ✔ * |
| Amazon S3 | ✔ | ✗ | ✗ | ✗ | ✔ |
| EOS | ✔ | ✔ | ✔ | ✔ | ✔ |

*Only UFS based 

## DAS (Direct Access to Storage)

The term DAS (Direct Access to Storage) defines the capability of a storage backend to be used from a variety of clients without losing the high scalable synchronization capability.

Only storages with these features built-in (not as external components) can offer DAS:

* Data store
* Namespace
* Unique Resource ID
* Propagation of changes

*Sync and Share platforms using  NFS as storage backend can provide DAS, but in a very inefficient way due to NFS lack of built-in Unique Resource ID and the Change Propagation features.*

**EOS is the only known storage backend that provides scalable DAS at the time of this writing**.

## HASD (Homogeneous Access to Share Data)

The term HASD (Homogeneous Access to Share Data) defines the capability of a storage backend for maintaining the ACL (Access Control List) consistency independently of the clients accessing the shared data.

None of the Open Source Sync and Share Platform in the market offer HASD.

To offer HASD the ACLs MUST be kept inside the storage and not in external components.

Traditional Sync and Share platforms have an ad-hoc component (usually and SQL DB) inside the sync and share server to handle the ACLs independently of the ACLs support provided by the storage.

ClawIO and CERNBox offer HASD, propagating share information to the underlying storage, creating new ways of collaboration.

**ClawIO and CERNBox are the only ones that provide HASD at the time of this writing.**
