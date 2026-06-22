# Ansible Practice Playbooks

This repository contains Ansible playbooks created to practice and demonstrate commonly used Ansible concepts.

## Prerequisites

* Ansible installed on Control Node
* Inventory file configured
* SSH connectivity to target hosts
* Sudo privileges (where required)

Run playbooks using:

```bash
ansible-playbook -i hosts <playbook>.yml
```

---

# Playbook 1 - Package Installation + Handlers + Facts

**File:** `clubbed1.yml`

### Concepts Covered

* package module
* service module
* handlers
* notify
* when condition
* facts
* debug
* become

### Purpose

Installs a package based on OS type and restarts the service using handlers when changes occur.

---

# Playbook 2 - Variables + Loops + Register + Until

**File:** `clubbed2.yml`

### Concepts Covered

* variables
* loop
* user module
* register
* retries
* delay
* until
* idempotency

### Purpose

Creates multiple users and demonstrates retry mechanisms using register, retries, delay, and until.

---

# Playbook 3 - Template + File + Copy + Fetch

**File:** `clubbed3.yml`

### Concepts Covered

* file module
* template module
* copy module
* fetch module
* variables
* Jinja2 templates

### Purpose

Creates directories, deploys dynamic content using templates, copies files from the control node to managed nodes, and fetches files back to the control node.

### Template Flow

```text
template.j2
      ↓
template module
      ↓
Remote Server File
```

### Copy vs Fetch

```text
copy  : Control Node → Managed Node
fetch : Managed Node → Control Node
```

---

# Playbook 4 - Stat + Assert + Lineinfile + Blockinfile

**File:** `clubbed4.yml`

### Concepts Covered

* stat module
* register
* assert
* lineinfile
* blockinfile
* become

### Purpose

Validates file existence, updates configuration files, and inserts managed blocks into files.

### Notes

* `assert` stops playbook execution when a condition fails.
* `when` skips execution when a condition fails.
* `blockinfile` requires an existing file or `create: yes`.

---

# Playbook 5 - Roles + Tags + Async + Delegate

**File:** `clubbed5.yml`

### Concepts Covered

* roles
* tags
* async
* poll
* delegate_to
* run_once
* serial
* strategy

### Purpose

Demonstrates role-based execution and advanced task execution controls.

### Role Structure

```text
roles/
└── nginx/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    ├── templates/
    ├── files/
    ├── vars/
    └── defaults/
```

### Role Execution Flow

```text
site.yml
   ↓
roles:
  - nginx
   ↓
roles/nginx/tasks/main.yml
   ↓
Tasks Execute
```

### WSL Note

The service module may fail inside WSL environments because systemd is not running as PID 1.

Example Error:

```text
System has not been booted with systemd as init system
```

For WSL environments, role demonstrations should focus on package installation, register, and debug modules instead of service management.

---

# Important Concepts Practiced

* Ad-hoc Commands
* Idempotency
* Variables
* Loops
* Conditions
* Handlers
* Templates
* Roles
* Serial
* Strategy (Linear vs Free)
* Delegate To
* Run Once
* Async and Poll
* Tags
* Fetch
* Copy
* Stat
* Assert
* Lineinfile
* Blockinfile
* Register
* Debug
* Become
* Facts

---

# Quick Revision

## Serial

Execute hosts in batches.

```yaml
serial: 2
```

## Strategy

Linear:

```yaml
strategy: linear
```

All hosts stay synchronized.

Free:

```yaml
strategy: free
```

Hosts execute independently.

## Assert vs When

```text
when   → Skip Task
assert → Stop Playbook
```

## Register

Stores task output.

```yaml
register: result
```

## Fetch

Copies files from managed node to control node.

```yaml
fetch:
  src: /tmp/file.txt
  dest: /backup/
```

## Template

Generates dynamic files using Jinja2 variables.

```yaml
template:
  src: welcome.j2
  dest: /tmp/welcome.txt
```

---

# Author

Swetha

Ansible Practice Repository for Interview Preparation.
