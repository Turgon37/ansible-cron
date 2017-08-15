Ansible Role Cron
========

This roles configure crontab of the host

## OS Family

This role is available for Debian and CentOS

## Features

At this day the role can be used to configure :

  * Cron environment variables
  * Cron task of the host (main crontab file)

## Configuration

The variables that can be passed to this role and a brief description about them are as follows:

| Name              | Description              |
| ----------------- | ------------------------------------------------------------------- |
| cron__exec_path   | The PATH value for the cron tasks                                   |
| cron__global_envs | List of global cron environment values                              |
| cron__group_envs  | List of group cron environment values (only one group is supported) |
| cron__host_envs   | List of host cron environment values                                |
| cron__global_jobs | List of global cron jobs/tasks                                      |
| cron__group_jobs  | List of group cron jobs/tasks                                       |
| cron__host_jobs   | List of host cron jobs/tasks                                        |

### Example

  * Exemple of specific task

```
cron__host_jobs:
  'ipcheck routine':
    job: /opt/IpCheck/ipcheck.py --no-output --config=/etc/ipcheck.conf
    user: nobody
    minute: '*/5'
```

  * Configure vars globally

```
cron__global_envs:
  MAILTO: admin@domain.net
  PATH: '{{ cron_exec_path }}'
```