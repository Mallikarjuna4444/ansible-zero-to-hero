Ansible facts are a way of gathering detailed information about the target machines or hosts in your infrastructure. When you run a playbook, Ansible collects various pieces of information from the hosts before executing tasks. This information is stored in a variable called `ansible_facts`.

Here’s a quick overview of what you can find in `ansible_facts` and how you might use them:

### Common Facts Collected

1. **System Information**
   - `ansible_facts['distribution']`: The Linux distribution (e.g., Ubuntu, CentOS).
   - `ansible_facts['distribution_version']`: The version of the Linux distribution.
   - `ansible_facts['hostname']`: The hostname of the machine.
   - `ansible_facts['kernel']`: The kernel version.

2. **Hardware Information**
   - `ansible_facts['processor_cores']`: Number of processor cores.
   - `ansible_facts['processor']`: Information about the processors.
   - `ansible_facts['memtotal_mb']`: Total memory in MB.

3. **Network Information**
   - `ansible_facts['default_ipv4']`: Default IPv4 address.
   - `ansible_facts['interfaces']`: Network interfaces on the machine.
   - `ansible_facts['hostname']`: The hostname of the machine.

4. **Filesystem Information**
   - `ansible_facts['mounts']`: Details about the mounted filesystems.
   - `ansible_facts['disk_io']`: Disk I/O statistics.

5. **Package Information**
   - `ansible_facts['packages']`: Information about installed packages.

### How to Use Ansible Facts

1. **Accessing Facts in Playbooks**
   You can use facts directly in your playbooks and roles. For example:
   ```yaml
   - name: Print the hostname
     debug:
       msg: "The hostname is {{ ansible_facts['hostname'] }}"
   ```

2. **Conditional Statements**
   Facts are useful for making decisions based on the environment. For instance:
   ```yaml
   - name: Install package on Ubuntu
     apt:
       name: vim
       state: present
     when: ansible_facts['distribution'] == 'Ubuntu'
   ```

3. **Setting Facts**
   You can also set custom facts using the `set_fact` module:
   ```yaml
   - name: Set a custom fact
     set_fact:
       my_custom_fact: "Hello World"
   
   - name: Use the custom fact
     debug:
       msg: "{{ my_custom_fact }}"
   ```

4. **Gathering Facts**
   By default, Ansible gathers facts at the start of the playbook. If you want to skip this, you can disable fact gathering with `gather_facts: no`. If you want to explicitly gather facts later, you can use the `setup` module:
   ```yaml
   - name: Gather facts
     setup:
   ```

### Customizing Facts Collection

You can customize which facts are gathered by modifying the `setup` module’s arguments. For example:
```yaml
- name: Gather only network-related facts
  setup:
    filter: 'ansible_network*'
```

This will gather only network-related facts, which can be useful to reduce the amount of information collected and speed up your playbook runs.

Ansible facts are a powerful feature for making your playbooks dynamic and responsive to the specific characteristics of your infrastructure.
