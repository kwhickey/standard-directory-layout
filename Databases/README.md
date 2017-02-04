A place to store database source code that can be used to initially create, or re-create all of the components physically added to databases.

A sub-folder should exist for each logical databases instance, with the individual database files stored under there, eventually grouped by each "database" itself.

NOTE: If using heterogeneous storage, such as some RDBMSs and some NoSQL, or perhaps different RDBMS vendors, you can optionally add another folder at the root of this `Databases` folder for each vendor product, and the `Common` folder would get pushed down into each of those vendor-specific folders.
- Oracle
- SqlServer
- Postgres
- MongoDb
- Redis
- Dynamo
- SqlLite
- Lmdb

etc.