
# Openshift template for deployment of Integrator profile of WSO2 Enterprise Integrator with Analytics

## Contents

* [Prerequisites](#prerequisites)
* [Quick Start Guide](#quick-start-guide)

## Prerequisites

1. An already setup OpenShift cluster

2. NFS shares for database storage. For a step by step guide on how to install NFS server refer here. [CentOS](https://www.server-world.info/en/note?os=CentOS_7&p=nfs&f=1), [Ubuntu](https://www.server-world.info/en/note?os=Ubuntu_18.04&p=nfs&f=1)

## Quick Start Guide

1. Create an OpenShift project name `wso2`.

   `oc new-project wso2`

2. Add your subscription details

   `oc create secret docker-registry wso2ei-deployment-creds --docker-server=docker.wso2.com --docker-username=<SUBSCRIPTION_USERNAME> --docker-password=<SUBSCRIPTION_PASSWORD>`

3. Deploy WSO2 Enterprise Integrator Server using the Template.yaml file.

   `oc process -f Template.yaml -p NFS_SERVER_IP=<NFS_SERVER_IP> -p NFS_SHARE_DATABASE=<DATABASE_NFS_SHARE_PATH> -p OPENSHIFT_BASE_DOMAIN=<OPENSHIFT_URL> | oc create -f -`

4. Access product management consoles. Obtain the (HOST/PORT) of the route resource.

   `oc get route -n <NAMESPACE>`
	
Try navigating to `https://<RELEASE_NAME>-integrator/carbon` and `https://<RELEASE_NAME>-analytics-dashboard/portal` from your favorite browser.

## Configuration

The following tables lists the configurable parameters of the template and their default values.

| Parameter                                                                   | Description                                                                               | Default Value               |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|-----------------------------|
|`OPENSHIFT_PROJECT_NAME`|Name of the OpenShift project|wso2|
|`OPENSHIFT_BASE_DOMAIN`|OpenShift base domain|`required`|
|`IMAGE_EI`|WSO2 Enterprice Integrator image name|docker.wso2.com/wso2ei-integrator:6.6.0|
|`IMAGE_EI_BROKER`|WSO2 Enterprice Integrator broker image name|docker.wso2.com/wso2ei-broker:6.6.0|
|`IMAGE_ANALYTICS_WORKER`|WSO2 Analytics Worker image name|docker.wso2.com/wso2ei-analytics-worker:6.6.0|
|`IMAGE_ANALYTICS_DASHBOARD`|WSO2 Analytics dashboard image name|docker.wso2.com/wso2ei-analytics-dashboard:6.6.0|
|`IMAGE_PULL_SECRET`|WSO2 Subscription Credentials|wso2ei-deployment-creds|
|`NFS_SERVER_IP`|NFS Server IP address||
|`NFS_SHARE_DATABASE`|NFS Share Path for database||
|`RESOURCES_LIMITS_CPU`|Set a CPU resource limits for integrator and broker|2000m|
|`RESOURCES_LIMITS_MEMORY`|Set a memory resource limits limits for integrator and broker|2Gi|
|`RESOURCES_REQUEST_CPU`|Set a minimum CPU resource limits limits for integrator and broker|1000m|
|`RESOURCES_REQUEST_MEMORY`|Set a minimum memory resource limits limits for integrator and broker|1Gi|
|`RESOURCES_LIMITS_CPU_ANALYTICS_WORKER`|Set a CPU resource limits for analytics worker|2000m|
|`RESOURCES_LIMITS_MEMORY_ANALYTICS_WORKER`|Set a memory resource limits for analytics worker|4Gi|
|`RESOURCES_REQUEST_CPU_ANALYTICS_WORKER`|Set a minimum CPU resource limits for analytics worker|2000m|
|`RESOURCES_REQUEST_MEMORY_ANALYTICS_WORKER`|Set a minimum memory resource limits for analytics worker|4Gi|
|`RESOURCES_LIMITS_CPU_ANALYTICS_DASHBOARD`|Set a CPU resource limits for analytics dashboard|2000m|
|`RESOURCES_LIMITS_MEMORY_ANALYTICS_DASHBOARD`|Set a memory resource limits for analytics dashboard|4Gi|
|`RESOURCES_REQUEST_CPU_ANALYTICS_DASHBOARD`|Set a minimum CPU resource limits for analytics dashboard|2000m|
|`RESOURCES_REQUEST_MEMORY_ANALYTICS_DASHBOARD`|Set a minimum memory resource limits for analytics dashboard|4Gi|
