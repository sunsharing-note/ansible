```
ansible1 ansible_ssh_host=192.168.40.200 ansible_ssh_user=root
ansible2 ansible_ssh_host=192.168.40.201 ansible_ssh_user=root
ansible3 ansible_ssh_host=192.168.40.202 ansible_ssh_user=root
[A]
192.168.40.201
[B]
192.168.40.202
[C]
192.168.40.20[1:2]
[D]
192.168.40.201
[E]
192.168.40.202
[F:children]
D
E
```
