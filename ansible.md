<!-- TITLE: Ansible -->


# Rôle Ansible

Voici comment ce compose la directorie d'un rôle ansible :


```sh
george ➜ ansible-epsi > tree ./
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
george ➜ ansible-epsi > cat inventory
[lb]
lb1

[web]
web1
web2
 
[db]
db1
```
Dans le dossier : *roles/apache* nous retouvons tous ce qui est lier au rôle apache. 
le dosissier *task* nous mettons les taches a effectuer :

```yaml
---
# tasks file for common
- include_tasks: install_apache.yaml
- include_tasks: vhost.yaml
- include_tasks: wordpress.yaml
```

ici nous séparons les diférente tâche dans diférent fichier yaml.
C'est pour cela que nous utilisons *include_tasks*

dans les autres fichier, nous avons par example :
```yaml
---
- name: install apache2
  apt:
    name: apache2
    state: latest
    update_cache: yes
```

ou bien 

```yaml
---
#créé le fichier de configuration du site grace a un template. 
- name: add template site
  template:
    src: site-test.j2
    dest: "/etc/apache2/sites-available/{{vhost_conf_file}}.conf"
    owner: root
    group: root
    mode: 0644
    backup: yes

#enbled le site si il ne l'ai pas déja.
- name: disable conf
  command: 
    cmd: "a2ensite {{vhost_conf_file}}.conf"
    creates: "/etc/apache2/sites-enabled/{{vhost_conf_file}}.conf"

- name: disable conf
  command: 
    cmd: a2dissite 000-default.conf
    creates: /etc/apache2/sites-enabled/000-default.conf

- name: enable conf
  command: 
    cmd: a2dissite default-ssl.conf
    creates: /etc/apache2/sites-enabled/default-ssl.conf
```
		
Dans le yaml si dessus nous utilison le module template.
Les template son écrit en jinja 2 et ce trouve dans le répertoire : *roles/apache/templates*
		
```jinja
		<VirtualHost *:80>
        ServerAlias {{ vhost_alias }}
        DocumentRoot {{ vhost_root_directory }}
        <Directory />
                Options FollowSymLinks
                AllowOverride none
        </Directory>
        <Directory {{ vhost_root_directory }}>
                Options FollowSymLinks MultiViews
                AllowOverride all
                Order allow,deny
                allow from all
        </Directory>

        ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
        <Directory "/usr/lib/cgi-bin">
                AllowOverride None
                Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
                Order allow,deny
                Allow from all
        </Directory>

        ErrorLog {{ vhost_log }}
        LogLevel warn

        CustomLog {{ vhost_log }} combined

    Alias /doc/ "/usr/share/doc/"
    <Directory "/usr/share/doc/">
        Options Indexes MultiViews FollowSymLinks
        AllowOverride None
        Order deny,allow
        Deny from all
        Allow from 127.0.0.0/255.0.0.0 ::1/128
    </Directory>
RewriteEngine on
</VirtualHost>
```
