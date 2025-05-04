Great! Here's a similar setup and example for **using Ansible with Azure virtual machines** via **dynamic inventory**, using the `azure.azcollection.azure_rm` plugin.

---

## ✅ Step-by-Step: Dynamic Inventory for Azure VMs

---

### 🔹 1. **Install Required Collections & Dependencies**

You need the Azure Ansible collection and Python SDKs:

```bash
ansible-galaxy collection install azure.azcollection
pip install azure-cli
pip install -r https://raw.githubusercontent.com/ansible-collections/azure.azcollection/main/requirements-azure.txt
```

---

### 🔹 2. **Authentication Options**

You can authenticate using:

* Environment variables (`AZURE_SUBSCRIPTION_ID`, etc.)
* Azure CLI (`az login`)
* A service principal with a credentials file

Certainly! Authentication is a key part of using Ansible with **Azure**. You have several ways to authenticate, depending on whether you’re using the **Azure CLI**, a **Service Principal**, or a **credentials file**. Here are the supported authentication methods:

---

## ✅**Using Azure CLI (Recommended for Local Dev)**

If you've logged in via Azure CLI:

```bash
az login
```

Then in your Ansible inventory plugin file (`azure_rm.yml`), set:

```yaml
auth_source: auto
```

Ansible will automatically pick up the Azure CLI login context.

### ✅ Pros:

* Simple for devs and scripting
* No need to manage credentials
* Works well with `az`-authenticated sessions

---

## ✅**Using Environment Variables (for CI/CD or Automation)**

You can set environment variables to authenticate as a **Service Principal**:

```bash
export AZURE_SUBSCRIPTION_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
export AZURE_CLIENT_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
export AZURE_SECRET="your-client-secret"
export AZURE_TENANT="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

And set `auth_source: auto` or `auth_source: env` in `azure_rm.yml`.

```yaml
auth_source: env
```

### ✅ Pros:

* Secure and script-friendly
* No dependencies on Azure CLI
* Works in CI/CD environments

---

## ✅**Using a Credentials File**

You can also use a credentials profile file (like AWS). Format:

**Location**: `~/.azure/credentials`

**Example**:

```ini
[default]
subscription_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
secret=your-client-secret
tenant=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

In your `azure_rm.yml`, use:

```yaml
auth_source: auto
```

or

```yaml
auth_source: credentials
profile: default
```

---

## ✅**Using a Managed Identity (for VMs or Services in Azure)**

If your playbook runs **from inside an Azure VM with a managed identity**, set:

```yaml
auth_source: msi
```

No credentials are needed in this case.

> Ensure the managed identity has adequate permissions to list/read VM resources.

---

## 🔐 Summary Table

| Method                 | `auth_source` value | Best For               | Requires Azure CLI? |
| ---------------------- | ------------------- | ---------------------- | ------------------- |
| Azure CLI              | `auto`              | Local development      | ✅ Yes               |
| Env Variables          | `env`               | CI/CD or automation    | ❌ No                |
| Credentials File       | `credentials`       | Shared dev/test setups | ❌ No                |
| Managed Identity (MSI) | `msi`               | Inside Azure VMs       | ❌ No                |

---

### 🔹 3. **Create Inventory Plugin File** (`azure_rm.yml`)

```yaml
# azure_rm.yml
plugin: azure.azcollection.azure_rm
include_vm_resource_groups:
  - myResourceGroup
auth_source: auto  # uses az CLI or env vars automatically
```

---

### 🔹 4. **Run Dynamic Inventory Command**

```bash
ansible-inventory -i azure_rm.yml --list
```

### ✅ Sample Output (Simplified JSON)

```json
{
  "_meta": {
    "hostvars": {
      "vm-web-01": {
        "ansible_host": "52.174.34.201",
        "location": "eastus",
        "resource_group": "myResourceGroup",
        "tags": {
          "Name": "webserver"
        }
      }
    }
  },
  "azure": {
    "hosts": [
      "vm-web-01"
    ]
  },
  "tag_Name_webserver": {
    "hosts": [
      "vm-web-01"
    ]
  }
}
```

---

## ✅ Using It in a Playbook

### Example: `setup-nginx.yml`

```yaml
---
- name: Configure Azure Webservers
  hosts: tag_Name_webserver
  become: yes

  tasks:
    - name: Install NGINX
      ansible.builtin.apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Ensure NGINX is running
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: yes

    - name: Show public IP
      ansible.builtin.debug:
        msg: "Host {{ inventory_hostname }} has IP {{ ansible_host }}"
```

---

### 🔹 Run the Playbook

```bash
ansible-playbook -i azure_rm.yml setup-nginx.yml
```
