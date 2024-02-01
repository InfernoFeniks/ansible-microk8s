# Ansible Role: microk8s
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)

## Description

Deploy [MicroK8S](https://microk8s.io/) is a low-ops, minimal production Kubernetes for building observability pipelines using ansible.

MicroK8s is an open-source system for automating deployment, scaling, and management of containerised applications.
It provides the functionality of core Kubernetes components, in a small footprint, scalable from a single node to a high-availability production cluster.

## Requirements

- Ansible >= 2.11 (It might work on previous versions, but we cannot guarantee it)
- Debian and python on deployer machine.

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `microk8s_user_name` | microk8s | Default user for work to MicroK8S |
| `microk8s_user_group`| microk8s | Default group for work to MicroK8S |
| `microk8s_version`| 1.29/stable | Version to use |
| `microk8s_replace_my_config`| false | WARNING! Rewrite your file if variable `microk8s_local_config_path`==`"~/.kube/config"` |
| `microk8s_local_config_path`| "~/.kube/config" | Path to config file CLI `kubectl` |
| `microk8s_external_fqdn`| "" | External FQND for the server |
| `microk8s_dns_resolvers`| 8.8.8.8,77.88.8.8 | DNS addresses |
| `microk8s_registry_size`| 10Gi | Registry size |
| `microk8s_plugins.*`|  | Enable/disable various plugins. A string will be passed as arg when enabling addon using `name:arg` (bool) |

## Example

### Playbook

```yaml
---
- name: MICROK8S | Install and Config
  hosts: all, !bastions
  roles:
    - role: microk8s
      tags: microk8s
  vars:
    - microk8s_version: "1.28/stable"
    - microk8s_replace_my_config: true
    - microk8s_local_config_path: "~/.kube/config"
    - microk8s_external_fqdn: "microkuber.example.com"
    - microk8s_plugins:
        dns: "1.1.1.1"
        istio: true
        ingress: true


```

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.


## Author Information

[Vector](https://microk8s.io/docs) by [Canonical](https://ubuntu.com/about).

Role by `InfernoFeniks`.