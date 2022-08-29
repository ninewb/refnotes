# Set environments to communicate with the API

source /opt/sas/viya/config/consul.conf
export CONSUL_TOKEN=$(sudo cat /opt/sas/viya/config/etc/SASSecurityCertificateFramework/tokens/consul/default/client.token)

# Query Postges Information

export PGHOST=$(/opt/sas/viya/home/bin/sas-bootstrap-config kv read config/postgres/sas.dataserver.pool/common/backend_hostname0)
export PGPORT=$(/opt/sas/viya/home/bin/sas-bootstrap-config kv read config/postgres/sas.dataserver.pool/common/backend_port0)
export PGPASSWORD=$(/opt/sas/viya/home/bin/sas-bootstrap-config kv read config/application/sas/database/postgres/password)

# Print to the Screen

echo Postgres Hostname: ${PGHOST}
echo Postgres Port: ${PGPORT}
echo Postgres Password: ${PGPASSWORD}