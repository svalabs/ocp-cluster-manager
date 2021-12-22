# OCP Cluster Manager

OCP Cluster Manager is an extensible framework for deployment and management of [Red Hat OpenShift](https://openshift.com/) clusters, powered by [Ansible](https://github.com/ansible/ansible).
It allows to define configuration parameters for multiple OpenShift clusters and therefore is a *multi-cluster* management tool.

## Getting Started

Read the [documentation](https://github.com/svalabs/ocp-cluster-manager/blob/main/ansible/README.md) of this framework.

## Features

### Deployment

For OpenShift deployments the `openshift-install` tool for the desired cluster version will be gathered.
The configuration parameters will be used to generate the OpenShift installation configuration files and start the deployment process.

The predefined values are suitable to deploy OpenShift on VMware vSphere in [IPI mode](https://docs.openshift.com/container-platform/4.9/installing/installing_vsphere/preparing-to-install-on-vsphere.html).

### Management

As soon as the OpenShift cluster is deployed, the post-configuration steps will run.
Some of the post-configuration tasks are:

* Setup NTP in cluster
* Deployment of [vSphere CSI driver](https://docs.vmware.com/en/VMware-vSphere-Container-Storage-Plug-in/index.html) and [Cloud Provider for vSphere](https://cloud-provider-vsphere.sigs.k8s.io/)
* Deployment of [Velero](https://velero.io/) Backup with [MinIO](https://docs.min.io/) backend
* and more to come.

More configuration tasks can be added by the user.
