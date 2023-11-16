
## Roles

Roles are a collection of tasks that are grouped together to achieve a specific task, such as installing software or configuring a service. Roles are a powerful way to organize your Ansible playbooks and make them easier to maintain.

### Role Structure

An Ansible role is organized into three main directories:

* **tasks:** This directory contains the tasks that will be executed to achieve the role's task.
* **handlers:** This directory contains handlers, which are tasks that are executed in response to an event, such as an error or a state change.
* **vars:** This directory contains variables that can be used by tasks and handlers.

### Role Example

Here is an example of an Ansible role that installs the Apache web server:


roles/apache
├── tasks
│   └── main.yml
└── handlers
    └── restart_apache.yml


The `tasks` directory contains the `main.yml` file, which contains the tasks that will be executed to install Apache. This file contains the following tasks:


- name: Install Apache
  apt:
    name: apache2
    state: present

- name: Enable Apache
  service:
    name: apache2
    state: started
    enabled: yes


The `handlers` directory contains the `restart_apache.yml` file, which contains the handler that will be executed in response to an event, such as an error or a state change. This file contains the following task:


- name: Restart Apache
  service:
    name: apache2
    state: restarted


## Playbooks

Playbooks are documents that describe how to execute roles on a set of systems. Playbooks are a powerful way to automate a wide variety of tasks, such as deploying software, configuring services, and managing infrastructure.

### Playbook Structure

An Ansible playbook is organized into three main sections:

* **hosts:** This section specifies the systems on which the playbook should be executed.
* **vars:** This section defines the variables that will be used by tasks and handlers.
* **roles:** This section specifies the roles that should be executed.

### Playbook Example

Here is an example of an Ansible playbook that uses the Apache role:


---
- hosts: all
  vars:
    apache_version: 2.4.5

  roles:
    - apache


This playbook specifies that the Apache role should be executed on all systems. It also defines the `apache_version` variable to the 2.4.5 version of Apache.

## Calling a Role

To call an Ansible role, you must specify the role name in the `roles` section of a playbook. The specified role will be executed on all systems specified in the `hosts` section of the playbook.

### Role Calling Diagram


playbooks
├── playbook.yml
└── roles
    └── apache


In this diagram, the `playbook.yml` playbook specifies that the `apache` role should be executed on all systems. The `apache` role contains the tasks and handlers necessary to install and configure the Apache web server.
