# ansible
- name: install and start apache
  hosts: webservers
  become: yes
  vars:
   http_port: 80

  tasks:
  - name: httpd package is present
    yum:
     name: httpd
     state: latest
     notify: restart httpd

  - name: latest index.html file is present
    copy:
     src: file/index.html
     dest: /var/www/html/

  handlers:
  - name: restart httpd
    service:
     name: httpd
     state: restarted
