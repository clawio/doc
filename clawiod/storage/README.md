# Storage configuration

ClawIO splits namespace operations from data handling into two different controllers:

- The data controller handles the upload and download of files.
- The metadata controller handles metadata operations: creating dirs, moving and deleting files, initializing the home directory...

The current storages are the following:

- The [simple storage](simple.md) connects to the underlying local filesystem and retrieves all the metadata from it.
- The [ocsql storage](ocsql.md) connects to the underlying local filesystem and also handles the ownCloud Sync Protocl using a MySQL/MariaDB database.

*We plan to develop more storage backends for object storages.*

To change the storage you to change the data and metadata controllers in the configuration file:

```json
{
 "data": {
    "type": "simple",
  },
 "metadata": {
    "type": "simple",
}
```
