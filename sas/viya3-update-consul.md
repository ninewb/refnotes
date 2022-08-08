# Query/Update Consul

[Consul](https://www.consul.io) is a third-party product used in SAS Viya 3.x.  It serves many functions from service discovery to handling of key-value-pairs.  Sometimes we need to access content in Consul, but also update some values. 

## Read Values

    source /opt/sas/viya/config/consul.conf
    export CONSUL_TOKEN=$(sudo cat /opt/sas/viya/config/etc/SASSecurityCertificateFramework/tokens/consul/default/client.token)

    /opt/sas/viya/home/bin/sas-bootstrap-config kv read --recurse config/

## Update Values

    source /opt/sas/viya/config/consul.conf
    export CONSUL_TOKEN=$(sudo cat /opt/sas/viya/config/etc/SASSecurityCertificateFramework/tokens/consul/default/client.token)

    /opt/sas/viya/home/bin/sas-bootstrap-config kv write --force config/path/to/key VALUE
