### Ansible Conditionals and Loops

Ansible conditionals and loops are powerful features that allow you to control the flow of execution in your playbooks. They enable you to execute tasks based on certain conditions or iterate over lists or dictionaries to perform repetitive tasks.

### Conditionals in Ansible

Conditionals are used to execute tasks only when certain conditions are met. This is typically done using the `when` clause.

#### Syntax

```yaml
- name: Task name
  ansible.builtin.module:
    key: value
  when: condition
```

#### Examples

1. **Basic Conditional**

   Execute a task only if a variable `nginx_installed` is `true`:

   ```yaml
   - name: Install Nginx
     ansible.builtin.yum:
       name: nginx
       state: present
     when: nginx_installed
   ```

2. **Using Conditional with Comparison**

   Execute a task based on the comparison of variables:

   ```yaml
   - name: Ensure Nginx is installed if port is 80
     ansible.builtin.yum:
       name: nginx
       state: present
     when: nginx_port == 80
   ```

3. **Multiple Conditions**

   Combine multiple conditions using `and` or `or`:

   ```yaml
   - name: Install Nginx if not installed and port is 80
     ansible.builtin.yum:
       name: nginx
       state: present
     when: not nginx_installed and nginx_port == 80
   ```

4. **Conditional on Host Facts**

   Use facts gathered by Ansible to make decisions:

   ```yaml
   - name: Check if operating system is Ubuntu
     ansible.builtin.debug:
       msg: "This is an Ubuntu system"
     when: ansible_facts['os_family'] == 'Debian'
   ```

### Loops in Ansible

Loops allow you to perform a task multiple times with different inputs. Ansible supports several looping constructs.

#### 1. **Using `loop` Keyword**

The `loop` keyword is used to iterate over a list or dictionary.

**Example with List**

```yaml
- name: Install multiple packages
  ansible.builtin.yum:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - vim
    - git
```

**Example with Dictionary**

```yaml
- name: Create multiple users
  ansible.builtin.user:
    name: "{{ item.name }}"
    state: present
    uid: "{{ item.uid }}"
  loop:
    - { name: 'alice', uid: 1001 }
    - { name: 'bob', uid: 1002 }
```

#### 2. **Using `with_items` Keyword**

`with_items` is an older way to loop over a list but is still widely used.

**Example**

```yaml
- name: Install packages with with_items
  ansible.builtin.yum:
    name: "{{ item }}"
    state: present
  with_items:
    - nginx
    - vim
    - git
```

#### 3. **Using `with_dict` Keyword**

`with_dict` is used to loop over a dictionary.

**Example**

```yaml
- name: Configure users
  ansible.builtin.user:
    name: "{{ item.key }}"
    state: present
    uid: "{{ item.value.uid }}"
  with_dict:
    alice:
      uid: 1001
    bob:
      uid: 1002
```

#### 4. **Using `with_subelements` Keyword**

`with_subelements` is useful when you have nested lists.

**Example**

```yaml
- name: Configure services
  ansible.builtin.systemd:
    name: "{{ item.item.service }}"
    state: started
  with_subelements:
    - "{{ services }}"
    - tasks
  vars:
    services:
      - name: web
        tasks:
          - { service: apache2 }
          - { service: nginx }
```

#### 5. **Looping with Conditionals**

You can also combine loops with conditionals.

**Example**

```yaml
- name: Install packages only if the system is CentOS
  ansible.builtin.yum:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - vim
    - git
  when: ansible_facts['os_family'] == 'RedHat'
```

### Combining Conditionals and Loops

You can combine conditionals and loops to execute tasks conditionally for each item in a list.

**Example**

```yaml
- name: Configure services based on a condition
  ansible.builtin.template:
    src: "{{ item.template }}"
    dest: "{{ item.dest }}"
  loop:
    - { template: 'nginx.conf.j2', dest: '/etc/nginx/nginx.conf', apply: true }
    - { template: 'httpd.conf.j2', dest: '/etc/httpd/httpd.conf', apply: false }
  when: item.apply
```

### Summary

- **Conditionals** (`when`) allow you to execute tasks based on conditions.
- **Loops** (`loop`, `with_items`, `with_dict`, etc.) enable you to iterate over lists or dictionaries.
- Combining conditionals with loops provides flexibility for executing tasks based on dynamic conditions.

By using conditionals and loops effectively, you can create more flexible and powerful playbooks that adapt to different environments and requirements.
