# 

```
cas fsiauto sessopts=(azureTenantId='b1c14d5c-3625-45b3-a430-9552373a0c2f');

CASLIB fsitest
   DATASOURCE=(
      SRCTYPE="ADLS" 
      ACCOUNTNAME="fsidlstorage" /* Storage Account Name */
      APPLICATIONID="a5ad54c3-fa0f-450b-9088-f995431dde8f" /* fsi-pac-processing app registration */ 
      TENANTID="b1c14d5c-3625-45b3-a430-9552373a0c2f" /* Subscription Tenant Id */
      FILESYSTEM="testing" 
      DNSSUFFIX="dfs.core.windows.net"
   )
PATH="/" subdirs
libref=AzureDL;
caslib _all_ assign;

proc casutil;
   list files;
quit;

cas fsiauto terminate;
```

SAS Decision Container Runtime
3
500m
6000Mi
4000Mi

SAS Detection Engine
3
500m
6000Mi
4000Mi