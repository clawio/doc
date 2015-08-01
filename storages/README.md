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

