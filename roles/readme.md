# Ansible roles #
ansible roles is a dry principle we can reuse it multiple time 

# What is an Ansible Role? #

A role in Ansible is a structured way to organize your playbooks and reuse automation code.

Instead of writing everything (tasks, handlers, variables, templates, files) in one long playbook, roles divide them into separate directories.

Think of roles like “folders of reusable automation units.”
Each role is designed to perform a specific function — for example:

Install and configure Nginx

Set up MongoDB

Deploy a Node.js app

🧱 # Example — Without Roles #

Normally, you might have one big playbook like this:

- name: Setup web server
  hosts: web
  become: yes
  tasks:
    - name: Install Nginx
      yum:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started


That works fine, but as your project grows, it becomes hard to manage.

🧩 With Roles (Clean & Organized)

You can structure your Ansible project like this:

roles/
 └── webserver/
     ├── tasks/
     │   └── main.yml
     ├── handlers/
     │   └── main.yml
     ├── templates/
     │   └── nginx.conf.j2
     ├── files/
     │   └── index.html
     ├── vars/
     │   └── main.yml
     └── defaults/
         └── main.yml


Then your playbook becomes short and clean:

- name: Configure web server
  hosts: web
  become: yes
  roles:
    - webserver

📁 Role Directory Explanation
Folder	Purpose
tasks/	Contains main tasks to execute (main.yml)
handlers/	Contains service restart/reload handlers
templates/	Contains Jinja2 templates (like nginx.conf.j2)
files/	Contains static files to copy
vars/	Defines variables for this role
defaults/	Default variables with lower priority
meta/	Role dependencies or metadata info
🧠 Why Roles Are Useful

Reusable — You can use the same role across many projects.

Organized — Keeps code clean and modular.

Scalable — Perfect for large environments.

Easier collaboration — Each team member can manage a separate role.

🧩 Example in Real Project (like Roboshop)

In your Roboshop project:

You can have roles such as:

role: catalogue

role: user

role: cart

role: mongodb

Each role manages only its service.

✅ In short:

Ansible Roles = A reusable and organized structure for automation tasks.
They make playbooks modular, clean, and easy to maintain.