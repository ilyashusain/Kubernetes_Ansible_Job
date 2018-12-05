# Kubernetes_Ansible_Job

Here we create a playbook that integrates Ansible into our Kubernetes nginx pod. Typically on start-up, we would need to edit the nginx.conf file to proxy_pass for the jenkins server. Our ansible playbook automated this process.

Create an ansible role called ```nginx_jenkins``` and create a task that will ssh into the nginx pod and configure the nginx.conf file for us. The script for the role is pasted below:

```
---  

  - name: install git
    shell: kubectl exec nginx-6688cb9fcb-w4srz apt install git
  - name: install vim
    shell: kubectl exec nginx-6688cb9fcb-w4srz apt install vim
  - name: delete current nginx conf
    shell: kubectl exec nginx-6688cb9fcb-w4srz rm /etc/nginx/nginx.conf
  - name: git clone nginx
    shell: kubectl exec nginx-6688cb9fcb-w4srz git clone https://github.com/ilyashusain/nginx_config.git
  - name: mv conf file
    shell: kubectl exec nginx-6688cb9fcb-w4srz mv nginx_config/nginx.conf /etc/nginx/
  - name: reload nginx
    shell: kubectl exec nginx-6688cb9fcb-w4srz service nginx reload  
```
