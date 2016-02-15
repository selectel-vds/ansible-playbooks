## Ansible playbook for Ajenti control panel installation

### Usage:

Before you start put your SSH keys (private and public) into credentials folder and edit `all.yml` file 
which contains all needed variables. It is also necessary to define an API key. You can add a key in 
your operating system environment variables, for *nix like systems: `export VS_API_KEY=<your_token>`. 
Or you can put them directly into `all.yml` file: `vscale_token: "<your_token>"`. Also you shoud clone 
ansible-vscale-module into `library` dir:
`git submodule add git@github.com:vscale/ansible-module.git ./library` and add public and private SSH keys into
`credentials` directory.

##### Example:
```yaml
vscale_token: "{{ lookup('env', 'VS_API_KEY')}}"
key: "{{ lookup('file', 'credentials/ansible.pub') }}"
```

Also, add the names of the hosts in `inventory` file like this:
```yaml
[ajenti-servers]
ajenti

[local]
localhost
```

When everything is ready, just start Ansible:
`ansible-playbook -i inventory vscale_ajenti.yml`