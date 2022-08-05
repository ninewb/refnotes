The following are some recommended performance tuning gathered across projects.

## CONSUL KEYS

The following consul keys should be adjusted for peak performance.  The inline keys are associated with various microservices on the platform.  Keys can be edited using the sas-bootstrap-config or directly through SAS Environment Manager.  When initiating a key update, you would execute in the folowing fashion:

## How To

```
. /opt/sas/viya/config/consul.conf
export CONSUL_HTTP_TOKEN=$(sudo cat /opt/sas/viya/config/etc/SASSecurityCertificateFramework/tokens/consul/default/client.token)

/opt/sas/viya/home/bin/sas-bootstrap-config kv write --force [key_location] [value]

# Check entry
/opt/sas/viya/home/bin/sas-bootstrap-config kv read --recurse config/ | grep [key]
```

<details><summary>Keys To Modify</summary>

svi-alert

    ```other
    config/svi-alert/jvm/java_option_xmx=-Xmx12g
    ```

#### svi-datahub

    ```other
    config/svi-datahub/jvm/java_option_xmx=-Xmx12g
    config/svi-datahub/spring.datasource.tomcat.maxActive=200 
    ```

#### svi-indexer

    ```
    config/svi-indexer/jvm/java_option_xmx=-Xmx12g
    ```

#### files

    ```
    config/files/jvm/java_option_xmx=-Xmx12g
    config/files/sas.files/maxFileSize=1073741824
    config/files/spring.datasource.tomcat.maxActive=100 (Default)
    ```

#### folders

    ```
    config/folders/jvm/java_option_xmx=-Xmx12g
    config/folders/spring.datasource.tomcat.maxActive=100 (Default)
    ```

#### cacheserver

    ```
    config/cacheserver/jvm/java_option_xms=-Xms2g
    config/cacheserver/jvm/java_option_xmx=-Xmx8g
    ```

#### saslogon

    ```
    config/SASLogon/jvm/java_option_xmx=-Xmx1024m
    ```
</details>
  
## Deployment / Config File


#### ElasticSearch

The elasticsearch heap size can be directly applied during a deployment within the inventory.ini file on the `ElasticSearch_HeapSize` propery.  If this requires tuning post-deployment, the property gets adjusted in the `jvm.options` file under `/opt/sas/viya/config/etc/elasticsearch/default` .  The property adjustment is at the top for `-Xmx` and `-Xms`.  The desired setting is 16G.
