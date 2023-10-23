# SAS Viya AML

## Fly DDL's

The DDL's are stored on the `sas-aml-core` container and database objects created during post-config with the `sas-aml-provisoning` container.  The DDL's can be obtained from the following location:

```
export KUBECONFIG=<path/to/kubeconfig>
export NAMESPACE=sas-aml
export AML_POD=$(kubectl get pod -n ${NAMESPACE} -o name -l app=sas-aml-core | awk -F "/" '{print $2}')
echo ${AML_POD}
kubectl cp -n ${NAMESPACE} -c sas-aml-core ${AML_POD}:opt/sas/viya/home/libexec .

# DDL path
# BOOT-INF/classes/db
```

## Configuration ZIP's

```
export PROV_POD=$(kubectl get pod -n ${NAMESPACE} -o name -l job-name=sas-aml-provisioning-job | awk -F "/" '{print $2}')
echo ${PROV_POD}
kubectl cp -n ${NAMESPACE} -c sas-aml-provisioning-job ${PROV_POD}:opt/sas/viya/home/share/sas-aml-provisioning-job .
```