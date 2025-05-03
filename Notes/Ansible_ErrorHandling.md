Error handling in Ansible is essential for managing playbook execution when tasks fail, ensuring that your playbooks can handle unexpected issues gracefully. Ansible provides several mechanisms for error handling, including ignoring errors, custom failure conditions, and structured error recovery.

### Error Handling Mechanisms with Examples

#### 1. **Ignoring Errors with `ignore_errors`**

The `ignore_errors` directive allows a task to fail without stopping the entire playbook. This is useful when you want to continue execution regardless of whether a specific task succeeds or fails.

**Example**

```yaml
- name: Install a package that might not be available
  ansible.builtin.yum:
    name: non_existent_package
    state: present
  ignore_errors: yes
```

In this example, if `non_existent_package` cannot be installed, the playbook will continue executing the subsequent tasks.

#### 2. **Custom Failure Conditions with `failed_when`**

The `failed_when` directive lets you define custom conditions for when a task should be considered failed. This allows more control over how failures are detected.

**Example**

```yaml
- name: Check for file existence
  ansible.builtin.stat:
    path: /path/to/file
  register: file_stat
  failed_when: file_stat.stat.exists == False
```

Here, the task will be marked as failed if `/path/to/file` does not exist, even if the `stat` module's return code is zero.

#### 3. **Handling Errors with `block`, `rescue`, and `always`**

The `block` directive allows you to group tasks together and handle errors using `rescue` and `always` blocks. This provides a way to recover from errors and ensure that certain tasks run regardless of success or failure.

**Example**

```yaml
- name: Handle errors in a block
  block:
    - name: Run a command that might fail
      ansible.builtin.command:
        cmd: /bin/false

    - name: This will not run if the previous task fails
      ansible.builtin.command:
        cmd: /bin/true
  rescue:
    - name: Handle failure
      ansible.builtin.debug:
        msg: "A task in the block failed"

  always:
    - name: Always run this
      ansible.builtin.debug:
        msg: "This task always runs, regardless of success or failure"
```

In this example:
- The `block` contains tasks that might fail.
- The `rescue` block runs if any task within the `block` fails.
- The `always` block executes regardless of whether the `block` succeeded or failed.

#### 4. **Using `register` and `when` for Conditional Execution**

You can use the `register` directive to capture the output of a task and then use the `when` clause to conditionally execute tasks based on the result.

**Example**

```yaml
- name: Try to start a service
  ansible.builtin.service:
    name: my_service
    state: started
  register: service_status
  ignore_errors: yes

- name: Notify if the service failed to start
  ansible.builtin.debug:
    msg: "The service failed to start"
  when: service_status.failed
```

In this example:
- The result of starting `my_service` is captured in `service_status`.
- The `debug` task only runs if `service_status.failed` is `true`.

#### 5. **Validating Results with `assert`**

The `assert` module can be used to validate conditions and provide meaningful failure messages.

**Example**

```yaml
- name: Validate the configuration file
  ansible.builtin.assert:
    that:
      - "'expected_value' in config_content"
    fail_msg: "The configuration file does not contain 'expected_value'"
  vars:
    config_content: "{{ lookup('file', '/path/to/config') }}"
```

Here:
- `assert` checks if `expected_value` is present in the configuration file.
- The playbook fails with a custom message if the condition is not met.

#### 6. **Using `try` in a `block`**

Starting from Ansible 2.8, `block` has enhanced capabilities to handle exceptions and perform cleanup actions using `rescue` and `always`.

**Example**

```yaml
- name: Example with block, rescue, and always
  block:
    - name: Run a potentially failing task
      ansible.builtin.command:
        cmd: /bin/false
    - name: This will not run if the previous task fails
      ansible.builtin.command:
        cmd: /bin/true
  rescue:
    - name: Handle task failure
      ansible.builtin.debug:
        msg: "An error occurred in the block"
  always:
    - name: Cleanup tasks
      ansible.builtin.debug:
        msg: "Cleanup tasks run regardless of block success or failure"
```

In this example:
- The `block` directive contains tasks that might fail.
- If any task in the `block` fails, the `rescue` block executes.
- The `always` block runs no matter the outcome of the `block`.

### Summary

- **`ignore_errors`**: Allows tasks to fail without stopping the entire playbook.
- **`failed_when`**: Defines custom conditions for task failures.
- **`block`, `rescue`, `always`**: Provides structured error handling with recovery options.
- **`register` and `when`**: Captures task results and executes subsequent tasks based on conditions.
- **`assert`**: Validates conditions and provides custom failure messages.

By implementing these error-handling techniques, you can create robust and resilient playbooks that handle failures gracefully and ensure that critical tasks are always executed.
