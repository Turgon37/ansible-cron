Ansible Role Cron
=========

:grey_exclamation: Before using this role, please know that all my Ansible roles are fully written and accustomed to my IT infrastructure. So, even if they are as generic as possible they will not necessarily fill your needs, I advice you to carrefully analyse what they do and evaluate their capability to be installed securely on your servers.

**This roles configure crontab of the host**

## Features

Currently this role provide the following features :

  * crontabs environment variables
  * support to declare cron job for host

## Requirements

### OS Family

This role is available for Debian and RedHat/CentOS

### Dependencies

--


## Role Variables

The variables that can be passed to this role and a brief description about them are as follows:

| Name              | Types/Values  | Description                                                        |
| ------------------| --------------|------------------------------------------------------------------- |
| cron__exec_path   | String        | The PATH value for the cron tasks                                  |
| cron__global_envs | Dict of String| List of global cron environment values                             |
| cron__group_envs  | Dict of String| List of group cron environment values (only one group is supported)|
| cron__host_envs   | Dict of String| List of host cron environment values                               |
| cron__global_jobs | Dict of String| List of global cron jobs/tasks                                     |
| cron__group_jobs  | Dict of String| List of hostgroup cron jobs/tasks                                  |
| cron__host_jobs   | Dict of String| List of host cron jobs/tasks                                       |

## Facts

No specific facts

## Example Playbook

To use this role create or update your playbook according the following example :


```
    - hosts: servers
      roles:
         - cron
      vars:
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


## License

MIT