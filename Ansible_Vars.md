### Ansible_Vars

Ansible variables are crucial for making your playbooks more flexible and reusable. They allow you to store values that can be used throughout your playbooks and roles, adapting configurations based on different environments or conditions.

### Defining and Using Variables

Variables in Ansible can be defined in several places and ways, each with different precedence levels. Here’s an overview of how to define and use variables, along with their precedence and examples.

#### 1. **Defining Variables**

Variables can be defined in various places, each serving different purposes and having different scopes and precedence. Here are some common places to define variables:

1. **Playbook Variables**: Defined directly in the playbook.
2. **Inventory Variables**: Defined in inventory files or inventory scripts.
3. **Host Variables**: Defined in host_vars files.
4. **Group Variables**: Defined in group_vars files.
5. **Role Variables**: Defined in roles under `defaults` or `vars` directories.
6. **Command-Line Variables**: Passed directly via the command line using `-e`.
7. **Environment Variables**: Defined in the environment and accessed via `env`.

#### 2. **Variable Precedence**

Ansible has a specific order of precedence for variables. The higher a variable is in the list, the higher its priority. Here’s the order of precedence (highest to lowest):

1. **Extra Vars** (`-e` on the command line)
2. **Task vars (set_facts)**
3. **Role vars (vars/main.yml)**
4. **Playbook vars (vars in the playbook)**
5. **Inventory vars (host_vars and group_vars)**
6. **Facts (gathered facts)**
7. **Defaults (role defaults)**

### Examples and Usage

#### 1. **Playbook Variables**

You can define variables directly in your playbook:

```yaml
---
- hosts: webservers
  vars:
    nginx_port: 8080
    nginx_server_name: example.local
  tasks:
    - name: Install nginx
      ansible.builtin.yum:
        name: nginx
        state: present
    - name: Configure nginx
      ansible.builtin.template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
```

#### 2. **Inventory Variables**

You can define variables in your inventory file:

```ini
# inventory.ini
[webservers]
web1 ansible_host=192.168.1.10 nginx_port=8080
web2 ansible_host=192.168.1.11 nginx_port=8081
```

You can also define group variables:

```ini
# inventory.ini
[webservers:vars]
nginx_server_name=example.local
```

#### 3. **Host Variables**

Host-specific variables can be defined in `host_vars` directory:

```yaml
# host_vars/web1.yml
nginx_port: 8080
nginx_server_name: web1.local
```

#### 4. **Group Variables**

Group-specific variables can be defined in `group_vars` directory:

```yaml
# group_vars/webservers.yml
nginx_server_name: example.local
```

#### 5. **Role Variables**

Variables can be defined in roles:

- **Defaults** (`roles/role_name/defaults/main.yml`):

  ```yaml
  # roles/webserver/defaults/main.yml
  nginx_port: 80
  ```

- **Vars** (`roles/role_name/vars/main.yml`):

  ```yaml
  # roles/webserver/vars/main.yml
  nginx_server_name: example.local
  ```

#### 6. **Command-Line Variables**

Variables can be passed via the command line using `-e`:

```bash
ansible-playbook playbook.yml -e "nginx_port=8080 nginx_server_name=example.local"
```

#### 7. **Environment Variables**

You can access environment variables using `env`:

```yaml
- name: Print environment variable
  ansible.builtin.debug:
    msg: "The value of HOME is {{ lookup('env', 'HOME') }}"
```

### Summary of Usage

#### **Example Playbook Using Various Variables**

Here’s a playbook that demonstrates using variables from different sources:

```yaml
---
- hosts: webservers
  become: yes
  vars:
    nginx_port: 8080 # Playbook variable
  roles:
    - role: webserver
      vars:
        nginx_server_name: example.local # Role-specific variable

- hosts: dbservers
  become: yes
  vars_files:
    - vars/db_config.yml # Variables from an external file
  tasks:
    - name: Print database host
      ansible.builtin.debug:
        msg: "Database host is {{ db_host }}"
```

In this example:

- `nginx_port` is defined directly in the playbook.
- `nginx_server_name` is defined within the role-specific variables.
- Database host is pulled from an external variables file (`vars/db_config.yml`).

### Conclusion

Ansible variables provide flexibility and control over your playbooks and roles. Understanding where and how to define variables, and knowing their precedence, helps you manage and customize your Ansible configurations efficiently. By using variables, you can make your playbooks reusable and adaptable to different environments.
