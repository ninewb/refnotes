# SAS Anti-Money Laundering

Looking forward with Anti-Money Laundering on SAS Viya 4.  

[Internal Documentation][1]

BYPASSRLS is mainly impacting when it comes to bulk load (employeesspolicy)

Workaround is to use the amldbadmin user

AGP for AML (bulk load is in the transaction monitoring stuff, should just be able to run as is)

```
- ../../../sas-bases/overlays/required/transformers.yaml
```


## Issues

```
{"level":"fatal","version":1,"source":"sas-aml-tenant-job","messageKey":"Error getting tenant job parameters from environment: validation failed for The tenant database username '_tenant1'","properties":{"logger":"aml-tenant-job/main","caller":"sdsci/main.go:569"},"timeStamp":"2023-09-23T14:49:58.887214+00:00","message":"Error getting tenant job parameters from environment: validation failed for The tenant database username '_tenant1'"}
{"level":"fatal","version":1,"source":"sas-run-tool","messageKey":"Service executor failed to execute successfully: exit status 1","properties":{"logger":"tools/run","caller":"impl/tooling.go:132"},"timeStamp":"2023-09-23T14:49:58.888898+00:00","message":"Service executor failed to execute successfully: exit status 1"}

===============================================================================
[Sat Sep 23 14:50:09 UTC 2023] Job finished: FAILED
===============================================================================


===============================================================================
[Sat Sep 23 14:50:09 UTC 2023] Dumping job logs to stdout
===============================================================================

{"level":"info","version":1,"source":"sas-run-tool","messageKey":"sonder-log-icu.run.tool.waiting.for.service.finish.log","properties":{"logger":"tools/run","caller":"impl/executor.go:263"},"timeStamp":"2023-09-23T14:49:58.025336+00:00","message":"Service successfully launched. Waiting for service to finish."}
{"level":"error","version":1,"source":"sas-aml-tenant-job","messageKey":"aml-tenant-job-log-icu.test.error.log","messageParameters":{},"properties":{"caller":"sdsci/main.go:544"},"timeStamp":"2023-09-23T14:49:58.064374+00:00","message":"No error this is just a test This is an example error."}
{"level":"info","version":1,"source":"sas-aml-tenant-job","messageKey":"'config/application/sas.multi.tenancy.db.mode' key found","properties":{"logger":"aml-tenant-job/database/tpg","caller":"tpg/tpg.go:555"},"timeStamp":"2023-09-23T14:49:58.259772+00:00","message":"'config/application/sas.multi.tenancy.db.mode' key found"}
{"level":"info","version":1,"source":"sas-aml-tenant-job","messageKey":"NOTE: MultiTenancy DB Credentials Mode defaults to 'single'","properties":{"logger":"aml-tenant-job/database/tpg","caller":"tpg/tpg.go:590"},"timeStamp":"2023-09-23T14:49:58.275144+00:00","message":"NOTE: MultiTenancy DB Credentials Mode defaults to 'single'"}
{"level":"error","version":1,"source":"sas-aml-tenant-job","messageKey":"The tenant Database Username '_tenant1' does not start with a letter","properties":{"logger":"aml-tenant-job/job","caller":"tenant/validation.go:117"},"timeStamp":"2023-09-23T14:49:58.887171+00:00","message":"The tenant Database Username '_tenant1' does not start with a letter"}
{"level":"fatal","version":1,"source":"sas-aml-tenant-job","messageKey":"Error getting tenant job parameters from environment: validation failed for The tenant database username '_tenant1'","properties":{"logger":"aml-tenant-job/main","caller":"sdsci/main.go:569"},"timeStamp":"2023-09-23T14:49:58.887214+00:00","message":"Error getting tenant job parameters from environment: validation failed for The tenant database username '_tenant1'"}
{"level":"error","version":1,"source":"sas-run-tool","messageKey":"Tool executor failed starting service: exit status 1","properties":{"logger":"tools/run","caller":"impl/executor.go:67"},"timeStamp":"2023-09-23T14:49:58.888875+00:00","message":"Tool executor failed starting service: exit status 1"}
{"level":"fatal","version":1,"source":"sas-run-tool","messageKey":"Service executor failed to execute successfully: exit status 1","properties":{"logger":"tools/run","caller":"impl/tooling.go:132"},"timeStamp":"2023-09-23T14:49:58.888898+00:00","message":"Service executor failed to execute successfully: exit status 1"}


{"level":"info","version":1,"source":"sas-run-tool","messageKey":"sonder-log-icu.run.tool.waiting.for.service.finish.log","properties":{"logger":"tools/run","caller":"impl/executor.go:263"},"timeStamp":"2023-09-25T12:44:18.433900+00:00","message":"Service successfully launched. Waiting for service to finish."}
{"level":"error","version":1,"source":"sas-aml-tenant-job","messageKey":"aml-tenant-job-log-icu.test.error.log","messageParameters":{},"properties":{"caller":"sdsci/main.go:544"},"timeStamp":"2023-09-25T12:44:18.473596+00:00","message":"No error this is just a test This is an example error."}
{"level":"info","version":1,"source":"sas-aml-tenant-job","messageKey":"'config/application/sas.multi.tenancy.db.mode' key found","properties":{"logger":"aml-tenant-job/database/tpg","caller":"tpg/tpg.go:555"},"timeStamp":"2023-09-25T12:44:18.639834+00:00","message":"'config/application/sas.multi.tenancy.db.mode' key found"}
{"level":"info","version":1,"source":"sas-aml-tenant-job","messageKey":"NOTE: MultiTenancy DB Credentials Mode defaults to 'single'","properties":{"logger":"aml-tenant-job/database/tpg","caller":"tpg/tpg.go:590"},"timeStamp":"2023-09-25T12:44:18.653671+00:00","message":"NOTE: MultiTenancy DB Credentials Mode defaults to 'single'"}
{"level":"fatal","version":1,"source":"sas-aml-tenant-job","messageKey":"Error creating provider HTTP client: error getting access token","properties":{"logger":"aml-tenant-job/main","caller":"sdsci/main.go:602"},"timeStamp":"2023-09-25T12:44:20.093466+00:00","message":"Error creating provider HTTP client: error getting access token"}
{"level":"error","version":1,"source":"sas-run-tool","messageKey":"Tool executor failed starting service: exit status 1","properties":{"logger":"tools/run","caller":"impl/executor.go:67"},"timeStamp":"2023-09-25T12:44:20.096414+00:00","message":"Tool executor failed starting service: exit status 1"}
{"level":"fatal","version":1,"source":"sas-run-tool","messageKey":"Service executor failed to execute successfully: exit status 1","properties":{"logger":"tools/run","caller":"impl/tooling.go:132"},"timeStamp":"2023-09-25T12:44:20.096443+00:00","message":"Service executor failed to execute successfully: exit status 1"}
```


---

[1]: https://pubshelpcenter.unx.sas.com/test/doc/en/compcdc/v_001/amlwlcm/home.htm
[2]: https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-servers

resources where properties matches regex @'[12]\d\d(\.([1-9]?\d|[12]\d\d)){3}' project  name, type, location, resourceGroup, subscriptionId, properties


https://fsipastorage.blob.core.windows.net/function-output/output.csv

github:
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

azure devops:
nmm2n4nt4pwzwcm2u3go2jku6aoptqwb2y5xb6znhhk6reqjlz4a

1. Update mirror codebase
2. Update personal notes location
3. Update 