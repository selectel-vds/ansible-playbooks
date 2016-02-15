## Ansible playbook for basic Django installation

### Usage:

Before you start put your SSH keys (private and public) into credentials folder and edit `all.yml` file 
which contains all needed variables. It is also necessary to define an API key. You can add a key in 
your operating system environment variables, for *nix like systems: `export VS_API_KEY=<your_token>`. 
Or you can put them directly into `all.yml` file: `vscale_token: "<your_token>"`. Also you shoud clone 
ansible-vscale-module into `library` dir:
`git submodule add git@github.com:vscale/ansible-module.git ./library`

##### Example:
```yaml
vscale_token: "{{ lookup('env', 'VS_API_KEY')}}"
key: "{{ lookup('file', 'credentials/ansible.pub') }}"
mysql_packages:
  - mysql-server
  - mysql-client
  - python-mysqldb
db_admin_user: "root"
db_admin_user_pass: "your_pass_here"
django_db_name: "django_test"
django_db_user: "django"
django_db_user_pass: "passW0rD"
django_project_name: "test_django"
```

Also, add the names of the hosts in `inventory` file like this:
```yaml
[django-servers]
django-01

[local]
localhost
```

When everything is ready, just start Ansible:
`ansible-playbook -i inventory vscale_django.yml`

When playbook is finished you can connect to your server via SSH and create Django superuser by typing command:
`django-admin createsuperuser`