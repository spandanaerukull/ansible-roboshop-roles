What Are Ansible Tags?

Tags in Ansible are labels you assign to tasks (or plays, roles, etc.) so that you can run or skip specific parts of your playbook.

Instead of executing all tasks every time, you can choose which ones to run — by using tags on the command line.

Think of it like bookmarks 🔖 in your playbook.

💡 Why Use Tags?

Imagine you have a big playbook with 20 tasks — installing software, copying configs, restarting services, etc.

If you just want to restart a service (not reinstall everything), tags let you do only that part:

✅ Saves time
✅ Avoids re-running unnecessary tasks
✅ Makes debugging or partial deployment easy

⚙️ Example: Using Tags in a Playbook
---
- hosts: web
  become: yes
  tasks:
    - name: Install nginx
      ansible.builtin.package:
        name: nginx
        state: present
      tags:
        - install
        - webserver

    - name: Copy nginx config
      ansible.builtin.copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
      tags:
        - config

    - name: Restart nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
      tags:
        - restart

🚀 How to Run Playbooks Using Tags
✅ Run only specific tags:
ansible-playbook site.yml --tags "install"


👉 Only tasks tagged with install will run.

🚫 Skip specific tags:
ansible-playbook site.yml --skip-tags "config"


👉 All tasks except config will run.

🧩 Multiple tags:
ansible-playbook site.yml --tags "install,restart"


👉 Runs both install and restart tagged tasks.

💬 Tagging Whole Plays or Roles

You can apply tags not just to tasks, but also to entire plays or roles.

Example — Tagging a Role:
- hosts: web
  roles:
    - role: nginx
      tags: 
        - web


Now you can run only that role:

ansible-playbook site.yml --tags "web"

⚡ Common Use Cases
Use Case	Example
Rerun only configuration tasks	--tags "config"
Skip time-consuming installations	--skip-tags "install"
Run cleanup tasks only	--tags "cleanup"
Limit playbook to one component	--tags "database"
🧠 Pro Tips

✅ Use consistent tag names (like install/config/restart/deploy/test).
✅ You can use multiple tags per task.
✅ Combine with conditionals for even finer control.
✅ Use --list-tags to see all tags available in a playbook:

ansible-playbook site.yml --list-tags

🏁 Summary
Feature	Description
Purpose	Run or skip selected tasks
Defined In	Tasks, plays, or roles
Syntax	tags: ["tag1", "tag2"]
Run with	ansible-playbook --tags "tagname"
Benefits	Saves time, improves flexibility, easy debugging

🧩 In short:

Tags make your playbooks modular, faster, and easier to test.