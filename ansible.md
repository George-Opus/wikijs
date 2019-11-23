<!-- TITLE: Ansible -->


# Rôle Ansible

Voici comment ce compose la directorie d'un rôle ansible :


```sh
george ➜ ansible-epsi > tree ./                                   git:(master) 
./
├── apache.yaml
├── inventory
├── group_vars
│   └── all.yaml
├── host_vars
│   └── db1.yaml
└── roles
         └── apache
                  ├── defaults
                  │   └── main.yml
                  ├── files
                  │   └── main.yml
                  ├── handlers
                  │   └── main.yml
                  ├── meta
                  │   └── main.yml
                  ├── README.md
                  ├── tasks
                  │   ├── install_apache.yaml
                  │   ├── main.yml
                  │   ├── vhost.yaml
                  │   └── wordpress.yaml
                  ├── templates
                  │   ├── site-test.j2
                  │   └── wordpress-config-db.j2
                  ├── tests
                  │   ├── inventory
                  │   └── test.yml
                  └── vars
													└── main.yml         
```
Nous allons donc voir étape par étape a quoi serve c'est différent fichier. 

Dans un premier temps nous avons le fichier : '*apache.yaml*'
```yaml
---
- hosts: web
  roles:
    - apache
```

Nous pouvons voir que nous definisson les hôtes sur lesquel nous allons installer apache ainsi que les role ici nommé *apache*
les hôtes son défini dans le fichier inventory 

```sh
george ➜ ansible-epsi > cat inventory                                                                                                                       git:(master) 
[lb]
lb1

[web]                                                                                                                                                                                          
web1
web2
 
[db]
db1
```