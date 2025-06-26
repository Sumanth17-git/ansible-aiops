# Ansible AIOps Project

This repository automates L1 operational tasks using Ansible:
- Disk cleanup
- CPU hog killer
- Out-of-memory resolver
- Dynamic service restarts
- Nginx config deployment with restart

Each use case is modular and can be run on-demand.

---

## 🧠 How It Works

### 1. Configuration Files

- **`ansible.cfg`**: Defines inventory, roles path, and disables host key checking.
- **`inventory/prod.ini`**: Lists your target servers (IP, user, SSH key).

### 2. Variables

- **`group_vars/all.yml`**: Central config for all roles (like cleanup path, thresholds).

```yaml
cleanup_paths:
  - path: /tmp
    age: 7
  - path: /var/log
    age: 14
```

### 3. Roles (Modular Use Cases)

- **disk_cleanup**: Deletes old files in /tmp, /var/log.
- **cpu_hog_killer**: Kills top CPU-consuming process.
- **oom_resolver**: Kills top memory-consuming process.
- **service_restart**: Restarts any service dynamically passed as input.
- **nginx_update**: Updates nginx.conf and restarts nginx.

### 4. Playbooks (Entry Points)

Each playbook maps to one role and executes it.

---

## 🚀 Run Examples

```bash
# Run disk cleanup
ansible-playbook playbooks/cleanup_disk.yml

# Kill top CPU-consuming process
ansible-playbook playbooks/kill_cpu_hog.yml

# Resolve OOM issue
ansible-playbook playbooks/resolve_oom.yml

# Restart one or more services dynamically
ansible-playbook playbooks/restart_services.yml --extra-vars='{"affected_services": ["nginx", "apache2"]}'

# Update and deploy nginx config
ansible-playbook playbooks/update_nginx.yml
```

---

## 🔁 Real-Time Example Flow

> 🔴 Alert: "nginx is down on server 10.128.0.47"

Run:
```bash
ansible-playbook playbooks/restart_services.yml --extra-vars='{"affected_services": ["nginx"]}'
```

✅ Ansible connects over SSH and restarts nginx.

---

## ✅ Benefits

| Feature              | Benefit                                      |
|---------------------|-----------------------------------------------|
| Modular roles        | Maintainable and reusable                   |
| Alert-to-action ready| Integrate with Prometheus, Dynatrace, etc.  |
| Fast L1 automation   | Fix issues in seconds                       |
| Secure execution     | No need to manually SSH into servers        |

---

## 🧩 Possible Enhancements

- Slack or email alert after playbook run
- Trigger from Prometheus webhook or Dynatrace
- Add wrapper CLI (`run_issue.sh`) to simplify use
- CI/CD pipeline integration (Jenkins, GitHub Actions)

---

Let this be your **starting point** for building a powerful internal AIOps toolkit with Ansible.
# Ansible AIOps Project

This repository automates L1 operational tasks using Ansible:
- Disk cleanup
- CPU hog killer
- Out-of-memory resolver
- Dynamic service restarts
- Nginx config deployment with restart

Each use case is modular and can be run on-demand.

## Run Examples
```bash
# Run disk cleanup
ansible-playbook playbooks/cleanup_disk.yml

# Kill top CPU-consuming process
ansible-playbook playbooks/kill_cpu_hog.yml

# Resolve OOM issue
ansible-playbook playbooks/resolve_oom.yml

# Restart one or more services dynamically
ansible-playbook playbooks/restart_services.yml --extra-vars='{"affected_services": ["nginx", "apache2"]}'

# Update and deploy nginx config
ansible-playbook playbooks/update_nginx.yml
```
