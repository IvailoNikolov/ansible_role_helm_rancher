# ansible Role Helm Rancher Backup

[![Ansible Lint](https://github.com/Frantche/ansible_role_helm_rancher/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/Frantche/ansible_role_helm_rancher/actions/workflows/ansible-lint.yml)

## Description

Installs Rancher Backup helm chart on kubernetes cluster using helm.

[The official rancher documentation for Install & Upgrade process](https://docs.ranchermanager.rancher.io/v2.6/pages-for-subheaders/installation-and-upgrade)

## Roles variables

| Name                           | Description                                                                                                         | Value                                                                                                                                                    |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| helm_rancher_name              | Release name to manage.                                                                                             | rancher                                                                                                                                                  |
| helm_rancher_chart_repo_url    | Chart repository URL where to locate the requested chart.                                                           | https://releases.rancher.com/server-charts/latest                                                                                                        |
| helm_rancher_chart_version     | Chart version to install. If this is not specified, the latest version is installed.                                | latest                                                                                                                                                   |
| helm_rancher_chart_ref         | chart_reference on chart repository.                                                                                | rancher                                                                                                                                                  |
| helm_rancher_release_namespace | Kubernetes namespace where the chart should be installed.                                                           | cattle-system                                                                                                                                            |
| helm_rancher_create_namespace  |                                                                                                                     | True                                                                                                                                                     |
| helm_rancher_values            | Value to pass to chart.                                                                                             | hostname: to.be.defined.com<br>ingress.tls.source: letsEncrypt<br>letsEncrypt.ingress.class: nginx<br>letsEncrypt.email: john.d@gmail.com<br>replicas: 1 |
| helm_rancher_values_files      | Value files to pass to chart. Paths will be read from the target host’s filesystem, not the host running ansible.   | []                                                                                                                                                       |
| helm_rancher_wait              | When release_state is set to 'present' wait for minimal readiness if 'absent' wait for all ressources to be deleted | True                                                                                                                                                     |
| helm_rancher_disable_hook      | Helm option to disable hook on install/upgrade/delete.                                                              | "no"                                                                                                                                                      |
| helm_rancher_force             | Helm option to force reinstall, ignore on new install.                                                              | "no"                                                                                                                                                      |
| helm_rancher_atomic            | If set, the installation process deletes the installation on failure.                                               | "no"                                                                                                                                                      |
| helm_rancher_skip_crds         | Skip custom resource definitions when installing or upgrading.                                                      | "no"                                                                                                                                                      |
| helm_rancher_update_repo_cache | Run helm repo update before the operation. Can be run as part of the package installation or as a separate step     | "no"                                                                                                                                                      |
| helm_rancher_binary_path       | The path of a helm binary to use.                                                                                   | "/usr/local/bin"                                                                                                                                         |
| helm_rancher_context           | Helm option to specify which kubeconfig context to use.                                                             | default                                                                                                                                                  |
| helm_rancher_kubeconfig        | Helm option to specify kubeconfig path to use.                                                                      | ~/.kube/config                                                                                                                                           |
| helm_rancher_validate_certs    | Whether or not to verify the API server’s SSL certificates.                                                         | "yes"                                                                                                                                                    |




## Requirements

create a file name "requirements.yml"
```yaml
---
collections:
    - name: kubernetes.core
      version: 2.3.2
    - name: git+https://github.com/Frantche/ansible_collection_helm_wrapper.git,main
roles:
  - name: frantchenco.ansible_role_helm_rancher
    type: git
    src: https://github.com/Frantche/ansible_role_helm_rancher.git
    version: main
```

Install requirements with the Ansible Galaxy CLI:

```bash
ansible-galaxy install -r ./requirements.yml
```

## Playbook example


```yaml
---
- hosts: master[0]
  serial: 1
  roles:
  - role: frantchenco.ansible_role_helm_rancher
```