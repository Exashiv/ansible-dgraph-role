# ansible-dgraph-role
## An ansible role to install dgraph

This role will configure a running instance of Dgraph

### How to use:

``` yaml
- name: MyPlaybook
  hosts: my_host
  roles:
    - role: dgraph
```

### Considerations:
This playbook requires python 2.7, for Ubuntu Xenial. The default is Python 3. So consider adding the following lines to the playbook.

```yaml
  pre_tasks:
    - name: Install ansible dependencies
      raw: test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
      become: yes
    - name: Gathering facts
      setup:
```


### Variables

#### Dgraph Zero Variables
This is the command to which will be used to run it
```sh
dgraph_zero_command: "dgraph zero"
```

This is the file and path where the logs are gonna be located
```sh
dgraph_zero_log_path: "/tmp/dgraph-zero.log"`
```
#### Dgraph Server Variables
This is the command to which will be used to run it
```sh
dgraph_server_command: "dgraph server --lru_mb {{ dgraph_server_memory }} --zero {{ dgraph_server_zero_location }}"
```

This the loction of the zero which will manage this server
Format: `[ip:port]`

```sh
dgraph_server_zero_location: localhost:5080
```

This is the assigned usage of memory to the server process
Recommended 1/3 of the total memory of the system
```sh
dgraph_server_memory: 1024
```

This is the file and path where the logs are gonna be located
```sh
dgraph_server_log_path: "/tmp/dgraph-server.log"
```
### Dgraph Ratel defaults
This is the command to which will be used to run Ratel

```sh
dgraph_ratel_command: "dgraph-ratel"
```
 This is the file and path where the logs are gonna be located
```sh
dgraph_ratel_log_path: "/tmp/dgraph-ratel.log"
```
### Future work:

* Add all configuration parameters of dgraph to the role.
* Add task to install an specific version, and checksum.
* Add a dedicated install.yml file
* Add tags to each task, example [server, zero, ratel]
