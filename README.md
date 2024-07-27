Ansible Role: Zimbra zmcontrol
=========

Ansible Role for zimbra mail service operation using zmcontrol command.

ref: https://zimbra.github.io/documentation/zimbra-10/adminguide.html#_zmcontrol_startstoprestart_service

Requirements
------------

User to connect zimbra hosts should be able to become sudo su to zimbra user.
You can test it using adhoc command:

ansible -m shell -a "id" zimbra -b --become-user=zimbra
zimbra | CHANGED | rc=0 >>
uid=987(zimbra) gid=987(zimbra) groups=987(zimbra),5(tty)

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Playbook example of how to use zmcontrol role

    - hosts: zimbra
      tasks:
      # First method, using "task_from:"
      - name: get zimbra version
        include_role:
          name: zmcontrol
          tasks_from: version

      - name: get zimbra service status
        include_role:
          name: zmcontrol
          tasks_from: status

      # Second method, using vars: action variable
      # Available var action: -v, status, start, stop, restart, maintenance, shutdown, startup
      - name: get zimbra service status
        include_role:
          name: zmcontrol
        vars:
          action: status
      # Optional if you want the result output    
      - debug:
          var: result.stdout

      - name: start zimbra service
        include_role:
          name: zmcontrol
        vars:
          action: start
      - debug:
          var: result.stdout

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
