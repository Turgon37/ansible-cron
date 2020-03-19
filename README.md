Ansible Role Cron
========

[![Build Status](https://travis-ci.com/Turgon37/ansible-cron.svg?branch=master)](https://travis-ci.com/Turgon37/ansible-cron)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-Turgon37.cron-blue.svg)](https://galaxy.ansible.com/Turgon37/cron/)

## Description

:grey_exclamation: Before using this role, please know that all my Ansible roles are fully written and accustomed to my IT infrastructure. So, even if they are as generic as possible they will not necessarily fill your needs, I advice you to carrefully analyse what they do and evaluate their capability to be installed securely on your servers.


This roles install and configure cron daemon and host crontabs.

## Requirements

Require Ansible >= 2.4

### Dependencies

## OS Family

This role is available for Debian and CentOS

## Features

At this day the role can be used to :

  * install and configure cron daemon
  * setup crontabs environment variables
  * declare cron jobs on host

## Configuration

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below. To see default values please refer to this file.

| Name              | Types/Values  | Description                                                        |
| ------------------| --------------|------------------------------------------------------------------- |
| cron__exec_path   | String        | The PATH value for the cron tasks                                  |
| cron__global_envs | Dict of String| List of global cron environment values                             |
| cron__group_envs  | Dict of String| List of group cron environment values (only one group is supported)|
| cron__host_envs   | Dict of String| List of host cron environment values                               |
| cron__global_jobs | Dict of String| List of global cron jobs/tasks                                     |
| cron__group_jobs  | Dict of String| List of hostgroup cron jobs/tasks                                  |
| cron__host_jobs   | Dict of String| List of host cron jobs/tasks                                       |

## Example

### Playbook

Use it in a playbook as follows:

```yaml
- hosts: all
  roles:
    - turgon37.cron
```

### Inventory

```
cron__global_envs:
  MAILTO: 'admin@example.com'
  PATH: '/sbin:/bin:/usr/sbin:/usr/bin'
cron__host_jobs:
  docker_clean_dangling_images:
    minute: 5
    hour: 0
    weekday: mon
    user: root
    job: >-
      imgs=$(docker images -f 'dangling=true' -q);
      if [ -n $imgs ]; then
      docker rmi $imgs 1>/dev/null;
      fi
```
