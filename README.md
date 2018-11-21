Role Name
=========

Installs and registers the official GitLab runner.

The role is as simple and as future-proof as possible:
* uses dynamic parameters for registration, so all `gitlab-runner` options are supported
* is able to work behind corporate proxy servers

Drawbacks:
* to keep it simple, it does not support reconfiguration of already registered runners - do it manually
* it will not uregister runners if you remove them from the `gitlab_runner_list` - it will only register missing ones

Requirements
------------

Role Variables
--------------

The role takes only one variable: `gitlab_runner_list`
The variable consists of lists of runners and their parameters that should be enabled on a host.
The list of available parameters can be taken from:
* `gitlab-runner register --help`
* [gitlab-ci-multirunner advanced-configuration](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/configuration/advanced-configuration.md)

Dependencies
------------


Example Playbook
----------------

Register two `shell` runners on one host.

Create `host_vars/your-server.yml` with:

```
---
gitlab_runner_list:
  - description: Runner 1 example
    url: https://your-gitlab-server.io
    executor: shell
    registration-token: your-secret-token
    tag-list: tag1,tag2,tag3
  - description: Runner 2 example
    url: https://your-gitlab-server.io
    executor: shell
    registration-token: your-secret-token
    tag-list: tag5,tag6,tag7
```

Then define a role

```
- hosts: your-server
  roles:
    - role: solval.gitlab_runner
  # If you use proxy:
  #vars:
    #proxy_env:
      #http_proxy: 'http://your-proxy:3128'
      #https_proxy: 'http://your-proxy:3128'
```

License
-------

Apache 2.0

Author Information
------------------

Jakub Dlugolecki
