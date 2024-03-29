# Onboard Non-operator

1. Configure Cluster Role on post-config namespace

```
kubectl -n postconfig apply -f cluster-role.yaml
```

2. Copy files

```
export deploy=/sas/viya4-deployment/deployments/nick-aml-19562-aks/sas-aml

cd ${deploy}/sas-aml/site-config/multi-tenant
mkdir -p tenant1

cp ${deploy}/sas-bases/examples/multi-tenant/sas-programming-environment/* ${deploy}/site-config/multi-tenant/tenant1

sed “{{ SAS-TENANT-ID }}” with “tenant1”

sed -i 's|{{ SAS-TENANT-ID }}|'tenant1'|g' *.yaml

```

Edit sas-bases/kustomization.yaml

```
resources:
- site-config/multi-tenant/tenant1
```

```
kubectl -n sas-aml apply -f $deploy-sasdeployment.yaml
```

```
sed -i 's|{{ SAS-TENANT-ID }}|'tenant1'|g' ${deploy}/site-config/multi-tenant/tenant1/*.yaml

kubectl -n sas-aml apply -f ${deploy}/sasdeployment.yaml

cp ${deploy}/sas-bases/examples/sas-tenant-job/* ${deploy}/site-config/sas-tenant-job/.
chmod -R 775 ${deploy}/site-config/sas-tenant-job/

sed -i 's|{{ VIYA-DEPLOYMENT-NAMESPACE }}|'sas-aml'|g' ${deploy}/site-config/sas-tenant-job/tenant-job-service-account-role.yaml
sed -i 's|{{ VIYA-DEPLOYMENT-NAMESPACE }}|'sas-aml'|g' ${deploy}/site-config/sas-tenant-job/kustomization-onboard.yaml
sed -i 's|{{ VIYA-DEPLOYMENT-NAMESPACE }}|'sas-aml'|g' ${deploy}/site-config/sas-tenant-job/kustomization-offboard.yaml

cd ${deploy}/site-config/sas-tenant-job/
mv tenant-onboard-job.yaml tenant-onboard-job-tenant1.yaml

sed "{{ SAS-TENANT-IDS }}" with "tenant1" tenant-onboard-job-tenant1.yaml

kustomize build . -o site-onboard.yaml --load-restrictor LoadRestrictionsNone
kubectl get secrets -n sas-aml | grep sas-image-pull-secrets

sed sas-image-pull-secrets with "output from above" site-onboard.yaml 

kubectl create -f site-onboard.yaml
```


Namespace
postconfig
Owner
Job sas-sfd-post-config
Pod
sas-sfd-post-config-xdqc9
Container
post-config
Search...
Deployment Post-Config: sasaml
+ Initiating Readiness Probe
Waiting on cluster readiness... 0 minutes elapsed.
Waiting on cluster readiness... 2 minutes elapsed.
Waiting on cluster readiness... 4 minutes elapsed.
Waiting on cluster readiness... 6 minutes elapsed.
Waiting on cluster readiness... 8 minutes elapsed.
Waiting on cluster readiness... 10 minutes elapsed.
Waiting on cluster readiness... 12 minutes elapsed.
Waiting on cluster readiness... 14 minutes elapsed.
Waiting on cluster readiness... 16 minutes elapsed.
Waiting on cluster readiness... 18 minutes elapsed.
Waiting on cluster readiness... 20 minutes elapsed.
cp: cannot stat '/sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/sas-bases/examples/multi-tenant/sas-programming-environment/*': No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/multi-tenant/tenant1/*.yaml: No such file or directory

Error: stat /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/kustomization.yaml: no such file or directory
error: the path "/sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/sasdeployment.yaml" does not exist
cp: cannot stat '/sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/sas-bases/examples/sas-tenant-job/*': No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/tenant-job-service-account-role.yaml: No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/kustomization-onboard.yaml: No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/kustomization-offboard.yaml: No such file or directory
error: the path "/sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/tenant-job-service-account-role.yaml" does not exist
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/tenant-onboard-job.yaml: No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/tenant-onboard-job.yaml: No such file or directory
sed: can't read /sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job/tenant-onboard-job.yaml: No such file or directory
cp: cannot stat 'kustomization-onboard.yaml': No such file or directory
Error: unable to find one of 'kustomization.yaml', 'kustomization.yml' or 'Kustomization' in directory '/sas/viya4-deployment/deployments/nick-aml-21696-aks/sas-aml/site-config/sas-tenant-job'
Error from server (Forbidden): secrets is forbidden: User "system:serviceaccount:postconfig:default" cannot list resource "secrets" in API group "" in the namespace "sas-aml"
Error: stat site-onboard.yaml: no such file or directory
sed: can't read site-onboard.yaml: No such file or directory
error: the path "site-onboard.yaml" does not exist
Pausing while the Tenant Job initiates


/sas/viya4-deployment/deployments/nick-aml-24823-aks/sas-aml/sas-bases/examples/cas/create
chmod +x create-cas-server.sh
./create-cas-server.sh -t tenant1 -o /sas/viya4-deployment/deployments/nick-aml-24823-aks/sas-aml/site-config -b 0 -w 2

Error: accumulating resources: accumulation err='accumulating resources from 'generation': '/tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation' 

must resolve to a file': recursed accumulation of path '/tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation': 

accumulating resources: accumulation err='accumulating resources from 'sas-bases/overlays/sas-workload-orchestrator': evalsymlink failure on '/tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation/sas-bases/overlays/sas-workload-orchestrator' : lstat /tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation/sas-bases/overlays/sas-workload-orchestrator: no such file or directory': must build at directory: not a valid directory: evalsymlink failure on '/tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation/sas-bases/overlays/sas-workload-orchestrator' : lstat /tmp/ansible.06n_4ncp/orchestration/work/deploy/resources/generation/sas-bases/overlays/sas-workload-orchestrator: no such file or directory
    The deploy command failed

    TASK [vdm : Deploy - Deploy SAS Viya] ******************************************
task path: /viya4-deployment/roles/vdm/tasks/deploy.yaml:51
failed: [localhost] (item={'path': '/tmp/ansible.fmt1e619/orchestration/manifests/sas-aml-sasdeployment.001.yaml', 'mode': '0644', 'isdir': False, 'ischr': False, 'isblk': False, 'isreg': True, 'isfifo': False, 'islnk': False, 'issock': False, 'uid': 1001, 'gid': 127, 'size': 219483, 'inode': 4979818, 'dev': 45, 'nlink': 1, 'atime': 1695818807.9141467, 'mtime': 1695818807.9141467, 'ctime': 1695818807.9141467, 'gr_name': '', 'pw_name': 'viya4-deployment', 'wusr': True, 'rusr': True, 'xusr': False, 'wgrp': False, 'rgrp': True, 'xgrp': False, 'woth': False, 'roth': True, 'xoth': False, 'isuid': False, 'isgid': False}) => changed=true 
  ansible_loop_var: item
  cmd:
  - orchestration
  - deploy
  - --namespace
  - sas-aml
  - --sas-deployment-cr
  - /tmp/ansible.fmt1e619/orchestration/manifests/sas-aml-sasdeployment.001.yaml
  delta: '0:00:27.638354'
  end: '2023-09-27 12:47:19.555731'
  invocation:
    module_args:
