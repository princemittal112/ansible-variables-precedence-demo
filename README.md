# Ansible Project: Variable Precedence Demo

## 🚀 Purpose

This project demonstrates how **Ansible variable precedence** works across different levels — including `defaults`, `vars`, `host_vars`, inventory, playbook-level, and extra-vars.

When the same variable is defined in multiple places, Ansible will use the one with the **highest precedence**.

---

## 📚 General Concept: Ansible Variable Precedence

Ansible resolves variables from **lowest to highest** precedence. Here's a simplified list:

| Precedence (Low ➝ High)     | Scope                             |
| --------------------------- | --------------------------------- |
| `defaults/main.yml`         | Role defaults                     |
| Inventory file/group/host   | `inventory/`, `host_vars/`        |
| `vars/main.yml`             | Role vars                         |
| Playbook `vars:`            | Vars defined directly in playbook |
| `set_fact`                  | Dynamically set in task           |
| Extra Vars (`--extra-vars`) | CLI arguments                     |

> The higher the level, the more it overrides others.

---

## 🗂 Project Structure

```
ansible-precedence-demo/
├── ansible.cfg
├── inventory/
│   └── inventory.ini
├── host_vars/
│   └── localhost.yml
├── roles/
│   └── myrole/
│       ├── defaults/
│       │   └── main.yml         # Low priority
│       ├── vars/
│       │   └── main.yml         # Higher than defaults
│       └── tasks/
│           └── main.yml         # Uses the variable
├── playbook.yml                # Declares vars or calls the role
```

---

## ▶️ How to Run

### 1. Run normally:

```bash
ansible-playbook playbook.yml
```

You’ll see the value from **playbook vars** (unless overridden).

### 2. Run with CLI override:

```bash
ansible-playbook playbook.yml --extra-vars="demo_variable='From CLI'"
```

Highest priority — overrides everything else.

---

## 📚 References

* [Ansible Docs: Variable Precedence](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#understanding-variable-precedence)
* [Ansible Roles Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html)
