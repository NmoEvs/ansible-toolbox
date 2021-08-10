# [Inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

```ini
mail.example.com

[webservers]
localhost              ansible_connection=local
other1.example.com     ansible_connection=ssh        ansible_user=myuser
other2.example.com     ansible_connection=ssh        ansible_user=myotheruser

[dbservers]
one.example.com
two.example.com
three.example.com

```

or

```yaml
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
    atlanta:  
        host1:
            http_port: 80
            maxRequestsPerChild: 808
        host2:
            http_port: 303
            maxRequestsPerChild: 909
```

## Inheriting variables values

```ini
[atlanta]
host1
host2

[raleigh]
host2
host3

[southeast:children]
atlanta
raleigh

[southeast:vars]
some_server=foo.southeast.example.com
halon_system_timeout=30
self_destruct_countdown=60
escape_pods=2

[usa:children]
southeast
northeast
southwest
northwest

```
