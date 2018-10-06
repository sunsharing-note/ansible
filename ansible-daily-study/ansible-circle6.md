with_subelements with_dict (with_file with_fileglob针对文件)

```
[root@ansible-k8s1 data]# ansible-playbook --syntax-check circle-test.yaml

playbook: circle-test.yaml
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: task1
    debug:
      msg: "{{ item }}"
    with_dict: "{{ users }}"
  vars:
    users:
      huahua: female
      zhouzhou: male
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [task1] *****************************************************************************************************************************************
ok: [test1] => (item={'value': u'male', 'key': u'zhouzhou'}) => {
    "msg": {
        "key": "zhouzhou",
        "value": "male"
    }
}
ok: [test1] => (item={'value': u'female', 'key': u'huahua'}) => {
    "msg": {
        "key": "huahua",
        "value": "female"
    }
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0
```
```
[root@ansible-k8s1 data]# cat circle-test.yaml
---
- hosts: test1
  remote_user: root
  gather_facts: no
  tasks:
  - name: task1
    debug:
      msg: "username is : { item,key }}, user's gender is: {{ item.value }}"
    with_dict: "{{ users }}"
  vars:
    users:
      huahua: female
      zhouzhou: male
[root@ansible-k8s1 data]# ansible-playbook circle-test.yaml

PLAY [test1] *****************************************************************************************************************************************

TASK [task1] *****************************************************************************************************************************************
ok: [test1] => (item={'value': u'male', 'key': u'zhouzhou'}) => {
    "msg": "username is : { item,key }}, user's gender is: male"
}
ok: [test1] => (item={'value': u'female', 'key': u'huahua'}) => {
    "msg": "username is : { item,key }}, user's gender is: female"
}

PLAY RECAP *******************************************************************************************************************************************
test1                      : ok=1    changed=0    unreachable=0    failed=0

```
