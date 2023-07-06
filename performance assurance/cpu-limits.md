---
branch: feature/cpu_limits
jira_story: [PERFASSUR-60](https://rndjira.sas.com/browse/PERFASSUR-60)
---

List of parameters we need to alter and make optional in the manifest file:

   #sed -i 's|{{ SCR_POD_REPLICAS }}|'"${SCR_POD_REPLICAS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ SCR_POD_CPU_LIMITS }}|'"${SCR_POD_CPU_LIMITS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ SCR_POD_MEM_LIMITS }}|'"${SCR_POD_MEM_LIMITS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ SCR_POD_CPU_REQUESTS }}|'"${SCR_POD_CPU_REQUESTS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ SCR_POD_MEM_REQUESTS }}|'"${SCR_POD_MEM_REQUESTS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_POD_CPU_LIMITS }}|'"${ODE_POD_CPU_LIMITS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_POD_MEM_LIMITS }}|'"${ODE_POD_MEM_LIMITS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_POD_CPU_REQUESTS }}|'"${ODE_POD_CPU_REQUESTS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_POD_MEM_REQUESTS }}|'"${ODE_POD_MEM_REQUESTS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_PROCESSING_SLA }}|'"${ODE_PROCESSING_SLA}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ ODE_PROCESSING_DISABLEMETRICS }}|'"${ODE_PROCESSING_DISABLEMETRICS}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml

    #sed -i 's/{{ ORG_CONTAINER }}/'"${ORG_CONTAINER}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's/{{ ORG_REPOSITORY }}/'"${ORG_REPOSITORY}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's/{{ ORG_TAG }}/'"${ORG_TAG}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml

    #sed -i 's|{{ VIYA_CONTAINER }}|'"${VIYA_CONTAINER}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ VIYA_REPOSITORY }}|'"${VIYA_REPOSITORY}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ VIYA_REPOSITORY_DIR }}|'"${VIYA_REPOSITORY_DIR}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's|{{ VIYA_TAG }}|'"${VIYA_TAG}"'|g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml

    #sed -i 's/{{ REDIS_HOST }}/'"${TKDETECTION_REDIS_HOST}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's/{{ KAFKA_SVC_HOST }}/'"${SAS_DETECTION_KAFKA_SERVER}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml
    #sed -i 's/{{ HOSTNAME }}/'"${ENVHOST}"'/g' ${ODE_DEPLOY_DIR}/sda-scr-runtime.yaml

yq e -i '(.spec.template.spec.containers[] | select(.name == "sas-detection") | .resources.limits.cpu) = env(ODEPODCPULIMITS)' scr-deployment.yaml

yq e '(.spec.template.spec.containers[].env[] | select(.name == "SAS_DETECTION_PROCESSING_SLA") | .value)' scr-deployment.yaml

## SCR Resources

``` bash
export SCRPODCPULIMITS=$(jq -r '.build.sfdruntime.pod_services.scr_resources.scr_pod_cpu_limits' ${ASSETS}/parameters.json)
if [[ ! -z "${SCRPODCPULIMITS}" ]]
then
  yq e -i '.spec.template.spec.containers[0].resources.limits.cpu = env(SCRPODCPULIMITS)' scr-deployment.yaml
fi

export SCRPODMEMLIMITS=$(jq -r '.build.sfdruntime.pod_services.scr_resources.scr_pod_mem_limits' ${ASSETS}/parameters.json)
if [[ ! -z "${SCRPODMEMLIMITS}"]]
then
  yq e -i '.spec.template.spec.containers[0].resources.limits.memory = env(SCRPODMEMLIMITS)' scr-deployment.yaml
fi
```


## ODE Resources

``` bash
export ODEPODCPULIMITS=$(jq -r '.build.sfdruntime.pod_services.ode_resources.ode_pod_cpu_limits' ${ASSETS}/parameters.json)
if [[ ! -z "${ODEPODCPULIMITS}" ]]
then
  yq e -i '.spec.template.spec.containers[1].resources.limits.cpu = env(ODEPODCPULIMITS)' scr-deployment.yaml
fi

export ODEPODMEMLIMITS=$(jq -r '.build.sfdruntime.pod_services.ode_resources.ode_pod_mem_limits' ${ASSETS}/parameters.json)
if [[ ! -z "${ODEPODMEMLIMITS}"]]
then
  yq e -i '.spec.template.spec.containers[1].resources.limits.memory = env(ODEPODMEMLIMITS)' scr-deployment.yaml
fi
```
