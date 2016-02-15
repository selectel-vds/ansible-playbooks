## Ansible playbook for basic Wordpress installation with Nginx + php-fpm

### Usage:

Before you start put your SSH keys (private and public) into credentials folder and edit `all.yml` file 
which contains all needed variables. It is also necessary to define an API key. You can add a key in 
your operating system environment variables, for *nix like systems: `export VS_API_KEY=<your_token>`. 
Or you can put them directly into `all.yml` file: `vscale_token: "<your_token>"`. If you want add SSH keys
to account - fill `key_name` and `key` strings. Also you shoud clone 
ansible-vscale-module into `library` dir:
`git submodule add git@github.com:vscale/ansible-module.git ./library` and add public and private SSH keys into
`credentials` directory.

##### Example:
```yaml
vscale_token: "{{ lookup('env', 'VS_API_KEY')}}"
key: "{{ lookup('file', 'credentials/ansible.pub') }}"
mysql_packages:
  - mysql-server
  - mysql-client
  - python-mysqldb
db_admin_user: "root"
db_admin_user_pass: "pAsSw0rd"
wp_db_name: "vscale_wp"
wp_db_user: "wp_db_admin"
wp_db_user_pass: "nimda_bd_pw"
wp_site_directory: "/var/www"
key_name: "Ansible"
key: |
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDLkxZXIe5Is5
/Ohx1W+m30UPtIAJ7BskLqGV/8mykPH6sX4KUpzlBA1eXs+oyJ
8RVWp23MqC6d8JBDP1uSf32hF/hSTcCH69jZAArzgERsvxLTH0
Mjif2KGxxBGQTEz67mT+5qsv4r64MSM1jgUES6ZMQC6LVHKbDJ
piqvXnQAhRYwgmADXq8vOTV6GzJ1I79iHhJfhU1zxpGKg3DisH
v9Oqf9xNl31v1X7hNz3BYQjFBNyY1Gyu6+0zRyBwRT2Vsgrt2r
WURWYMDO/l1CVQqIZ6ahuRvvNZaX5J1ocSM8NbaFo3W+2bFZSA
LmLaT+BB3FXkhoYcK7K/4i+elJBPdL ansible@key
```

Also, add the names of the hosts in `inventory` file like this:
```yaml
[wp-servers]
wp-01
wp-02

[local]
localhost
```

When everything is ready, just start Ansible:
`ansible-playbook -i inventory vscale_wp.yml`