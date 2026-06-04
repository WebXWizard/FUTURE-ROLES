# Phase 14: Automation with Ansible (10 Days)

> Manage thousands of servers at once with Ansible. Learn automation for infrastructure scaling and consistent system management.

**Phase Duration**: 10 days

---

## 📋 What You'll Learn

```
├── Ansible Basics
├── Inventory Management
├── Playbooks
├── Modules
├── Variables
├── Handlers
├── Roles
├── Error Handling
├── Conditional Execution
└── Multi-server Deployment
```

---

## 🗓️ गाइड

### **DAY 1-2: Basics**

```bash
# Install:
sudo apt install ansible

# Inventory file (/etc/ansible/hosts):
[webservers]
web1.example.com ansible_user=ubuntu
web2.example.com ansible_user=ubuntu

[databases]
db1.example.com ansible_user=ubuntu

# Test connection:
ansible all -i inventory.ini -m ping
```

---

### **DAY 3-4: Playbooks**

```bash
# site.yml - Basic playbook:
---
- hosts: webservers
  tasks:
    - name: Update packages
      apt:
        update_cache: yes
    
    - name: Install nginx
      apt:
        name: nginx
        state: present
    
    - name: Start nginx
      service:
        name: nginx
        state: started

# Run:
ansible-playbook -i inventory.ini site.yml
```

---

### **DAY 5-6: Roles & Variables**

```bash
# Roles structure:
roles/
├── webserver/
│   ├── tasks/main.yml
│   ├── handlers/main.yml
│   ├── templates/
│   ├── files/
│   └── vars/main.yml
├── database/
└── monitoring/

# Playbook with roles:
---
- hosts: webservers
  roles:
    - webserver
    - monitoring
  vars:
    nginx_port: 80
```

---

### **DAY 7-8: Handlers & Conditionals**

```bash
# Handlers (restart जब file change हो):
---
- hosts: webservers
  tasks:
    - name: Copy config
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: restart nginx
  
  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted

# Conditionals:
---
- hosts: all
  tasks:
    - name: Install Apache
      apt:
        name: apache2
      when: ansible_os_family == "Debian"
```

---

### **DAY 9-10: Real Scenarios**

```bash
# Deployment playbook:
---
- name: Deploy application
  hosts: app_servers
  
  vars:
    app_dir: /opt/myapp
    github_repo: https://github.com/user/repo.git
    
  tasks:
    - name: Clone repository
      git:
        repo: "{{ github_repo }}"
        dest: "{{ app_dir }}"
    
    - name: Install dependencies
      shell: npm install
      args:
        chdir: "{{ app_dir }}"
    
    - name: Build
      shell: npm run build
      args:
        chdir: "{{ app_dir }}"
    
    - name: Restart service
      service:
        name: myapp
        state: restarted
```

---

## 💡 Ansible vs Others

```
Ansible: Agentless, SSH-based, easy
Chef:    Agent-based, powerful
Puppet:  Agent-based, complex
Terraform: IaC (infrastructure provision)
```

---

अगला: **Phase 15: Production Operations**
