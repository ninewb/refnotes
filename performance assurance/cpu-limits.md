---
branch: feature/cpu_limits
jira_story: [PERFASSUR-60](https://rndjira.sas.com/browse/PERFASSUR-60)
---

List of parameters we need to alter and make optional in the manifest file:



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

## Testing Scenarios

- scr cpu limit removed
- ode mem limit removed

### 6934

  SCR_POD_REPLICAS=1
  SCR_POD_CPU_LIMITS=1
  SCR_POD_MEM_LIMITS is not defined
  SCR_POD_CPU_REQUESTS=50m
  SCR_POD_MEM_REQUESTS=50Mi
  SCR_POD_MEM_REQUESTS=50Mi
  ODE_POD_CPU_LIMITS is not defined
  ODE_POD_MEM_LIMITS=500Mi
  ODE_POD_CPU_REQUESTS=500m
  ODE_POD_MEM_REQUESTS=500Mi
  ODE_PROC_SLA=85
  ODE_PROC_DIS_METRIC=false