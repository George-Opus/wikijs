<!-- TITLE: Ansible -->
<!-- SUBTITLE: A quick summary of Ansible -->

# Header


```sh
george ➜ ansible-epsi > tree ./                                   git:(master) 
./
├── apache.yaml
├── group_vars
│   └── all.yaml
├── haproxy.yaml
├── host_vars
│   └── db1.yaml
├── inventory
├── mariadb.yaml
├── README.md
├── roles
│   ├── apache
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   │   ├── dummy
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   ├── install_apache.yaml
│   │   │   ├── main.yml
│   │   │   ├── vhost.yaml
│   │   │   └── wordpress.yaml
│   │   ├── templates
│   │   │   ├── site-test.j2
│   │   │   └── wordpress-config-db.j2
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── common
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   │   └── dummy
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── haproxy
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   └── mariadb
│       ├── defaults
│       │   └── main.yml
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── README.md
│       ├── tasks
│       │   ├── create_database.yaml
│       │   ├── create_mariadb_user.yaml
│       │   ├── install_mariadb.yaml
│       │   ├── install_requirements.yaml
│       │   ├── main.yml
│       │   └── mariadb_root_password.yaml
│       ├── tests
│       │   ├── inventory
│       │   └── test.yml
│       └── vars
│           └── main.yml
├── schema_reseau
│   └── test
└── wordpress
    └── wordpress-5.3-fr_FR.tar.gz

36 directories, 54 files
george ➜ ansible-epsi >           
```