# ansible Role Helm Nginx

[![Ansible Lint](https://github.com/Frantche/ansible_role_helm_nginx/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Frantche/ansible_role_helm_nginx/actions/workflows/ansible-lint.yml)

## Description

Installs nginx ingress helm chart on kubernetes cluster using helm

## Requirements

create a file name "requirements.yml"
```yaml
---
collections:
    - name: kubernetes.core
      version: 2.3.2
    - name: git+https://github.com/Frantche/ansible_collection_helm_nginx_wrapper.git,main
```

## Roles variables

| Name                   | Description                                                                                                         | Value                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| helm_nginx_name              | Release name to manage.                                                                                             | nginx                      |
| helm_nginx_chart_repo_url    | Chart repository URL where to locate the requested chart.                                                           | https://kubernetes.github.io/ingress-nginx |
| helm_nginx_chart_version     | Chart version to install. If this is not specified, the latest version is installed.                                | latest                            |
| helm_nginx_chart_ref         | chart_reference on chart repository.                                                                                | ingress-nginx                              |
| helm_nginx_release_namespace | Kubernetes namespace where the chart should be installed.                                                           | ingress-nginx                     |
| helm_nginx_create_namespace  |                                                                                                                     | True                               |
| helm_nginx_values            | Value to pass to chart.                                                                                             | replicaCount: 2                    |
| helm_nginx_values_files      | Value files to pass to chart. Paths will be read from the target host’s filesystem, not the host running ansible.   | []                                 |
| helm_nginx_wait              | When release_state is set to 'present' wait for minimal readiness if 'absent' wait for all ressources to be deleted | True                               |
| helm_nginx_disable_hook      | Helm option to disable hook on install/upgrade/delete.                                                              | no"                                |
| helm_nginx_force             | Helm option to force reinstall, ignore on new install.                                                              | no"                                |
| helm_nginx_atomic            | If set, the installation process deletes the installation on failure.                                               | no"                                |
| helm_nginx_skip_crds         | Skip custom resource definitions when installing or upgrading.                                                      | no"                                |
| helm_nginx_update_repo_cache | Run helm repo update before the operation. Can be run as part of the package installation or as a separate step     | no"                                |
| helm_nginx_binary_path       | The path of a helm binary to use.                                                                                   | "/usr/local/bin"                   |
| helm_nginx_context           | Helm option to specify which kubeconfig context to use.                                                             | default                            |
| helm_nginx_kubeconfig        | Helm option to specify kubeconfig path to use.                                                                      | ~/.kube/config                     |
| helm_nginx_validate_certs    | Whether or not to verify the API server’s SSL certificates.                                                         | "yes"                              |
| helm_nginx_install_prereq    | Check all pre requisites software are installed on the host who will perform command                                | True                               |


### Playbook example


```yaml
---
- hosts: master[0]
  serial: 1
  roles:
  - role: frantchenco.ansible_role_helm_nginx_nginx_ingress
```