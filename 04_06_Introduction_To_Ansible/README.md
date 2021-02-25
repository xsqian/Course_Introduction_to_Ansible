ansible -m service -a "name=httpd state=stopped" --become loadbalancers
[WARNING]: Platform linux on host lb1 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python
interpreter could change the meaning of that path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more
information.
lb1 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": true,
    "name": "httpd",
    "state": "stopped"
}
(base) xsqian@[21:52:41]<04_06_Introduction_To_Ansible>% 

(base) xsqian@[21:52:41]<04_06_Introduction_To_Ansible>% ansible-playbook playbooks/check-status.yml 

PLAY [webservers:loadbalancers] *************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************
[WARNING]: Platform linux on host lb1 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python
interpreter could change the meaning of that path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more
information.
ok: [lb1]
[WARNING]: Platform linux on host app1 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python
interpreter could change the meaning of that path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more
information.
ok: [app1]
[WARNING]: Platform linux on host app2 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python
interpreter could change the meaning of that path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more
information.
ok: [app2]

TASK [Check status of apache] ***************************************************************************************************************************
[WARNING]: Consider using the service module rather than running 'service'.  If you need to use command because service is insufficient you can add
'warn: false' to this command task or set 'command_warnings=False' in ansible.cfg to get rid of this message.
fatal: [lb1]: FAILED! => {"changed": true, "cmd": ["service", "httpd", "status"], "delta": "0:00:00.017511", "end": "2021-02-17 05:53:31.880378", "msg": "non-zero return code", "rc": 3, "start": "2021-02-17 05:53:31.862867", "stderr": "", "stderr_lines": [], "stdout": "httpd is stopped", "stdout_lines": ["httpd is stopped"]}
changed: [app2]
changed: [app1]

PLAY RECAP **********************************************************************************************************************************************
app1                       : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
app2                       : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
lb1                        : ok=1    changed=0    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   

(base) xsqian@[21:53:32]<04_06_Introduction_To_Ansible>% 

ansible -m service -a "name=httpd state=started" --become loadbalancers

(base) xsqian@[21:54:20]<04_06_Introduction_To_Ansible>% ansible -m service -a "name=httpd state=started" --become loadbalancers
[WARNING]: Platform linux on host lb1 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python
interpreter could change the meaning of that path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more
information.
lb1 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": true,
    "name": "httpd",
    "state": "started"
}
(base) xsqian@[21:54:29]<04_06_Introduction_To_Ansible>% 

ansible-playbook playbooks/check-status.yml 

LAY RECAP **********************************************************************************************************************************************
app1                       : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
app2                       : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
lb1                        : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

