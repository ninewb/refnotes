The files added as attachments to Visual Investigator objects are stored as BLOBs in the internal Postgres data source: `pg_catalog.pg_largeobjects`

They are registered in the Files service (tables `files.file_meta` and `files.file_content` in Postgres), then in VI folders (Folders service, not physical directory) and finally registered within DataHub service (table `fdhdata.dh_file`).

The authorization rules ensure that these files are only accessible through DataHub. On file retrieval through DataHub service, the service ensures the user has access to the document the file is associated with. This is also true when using Visual Investigator REST APIs.


- To our best knowledge, they are not encrypted, unless the database itself is encrypted.
- There is no checksum or fingerprint mechanism in place in the standard deployment, besides the audit trace you can set up at database level.
- As a side note, these files can also be indexed and the text contents would be stored within ElasticSearch.

SAS Viya simply relies on what PostgreSQL provides by default. The encryption features in PostgreSQL are explained in [17.8. Encryption Options](https://www.postgresql.org/docs/9.4/encryption-options.html).

In short, most data (data at rest) is not really encrypted unless user implements encryption at the file system level.

The Viya deployment has set the correct ownership and permission to assure its functionality.  Beneath excerpt from my test server and the permission is only permissive by owner only.

```other
$ ls -ld /opt/sas/viya/config/data/sasdatasvrc/postgres/node0
drwx——— 19 sas sas 4096 Apr 25 13:43 /opt/sas/viya/config/data/sasdatasvrc/postgres/node0
```


Data files are binary files.  Data files generated in above folder is only accessible by owner, i.e. sas user
