Ansible Role: Zimbra zmcontrol
=========

Ansible Role for zimbra mail service operation using zmcontrol command.

Requirements
------------

User used to connect to zimbra hosts should be able to become sudo su to zimbra user.
You can test it using adhoc command:

    [ansible@ansible-box ~]$ ansible -m shell -a "id" zimbra -b --become-user=zimbra
    zimbra | CHANGED | rc=0 >>
    uid=987(zimbra) gid=987(zimbra) groups=987(zimbra),5(tty)
    

Role Variables
--------------

Available vars action: -v, status, start, stop, restart, maintenance, shutdown, startup

zmcontrol command reference: https://zimbra.github.io/documentation/zimbra-10/adminguide.html#_zmcontrol_startstoprestart_service

Dependencies
------------

n/a

Example Playbook
----------------

Playbook example of how to use zmcontrol role

    - hosts: zimbra
      tasks:
      # First method, using "task_from:"
      - name: get zimbra version
        include_role:
          name: ronaldisnt.zmcontrol
          tasks_from: version

      - name: get zimbra service status
        include_role:
          name: ronaldisnt.zmcontrol
          tasks_from: status

      # Second method, using vars: action variable
      # Available vars action: -v, status, start, stop, restart, maintenance, shutdown, startup
      - name: get zimbra service status
        include_role:
          name: ronaldisnt.zmcontrol
        vars:
          action: status
      # Optional if you want the result output    
      - debug:
          var: result.stdout

      - name: start zimbra service
        include_role:
          name: ronaldisnt.zmcontrol
        vars:
          action: start
      - debug:
          var: result.stdout

License
-------

GNU General Public License v3.0

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
