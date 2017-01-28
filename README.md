radamanth.redmine-ansible
=========

This role install Redmine and set the default root passwd.
It also set an https reverse proxy with apache2 

Requirements
------------

Target platform should be an ubuntu with apt-get capabilities

Role Variables
--------------

# Mysql user for redmine

    redmine_db_login: redmine

# Password of redmine_db_login

    redmine_db_passwd: "redminedbpasswd"

# Database name for redmine

     redmine_db_name: redmine_yourcompany

# The default admin user that will be set on your redmine installation

    redmine_admin_login: admin
    redmine_admin_passwd: "redmine"
    redmine_admin_mail: youradmin@yourdomain.com

# Recommended in hosts_vars/host
## Mail that will be set on the from field whend Redmine send notificaitons

    redmine_mail_from: yourmailfrom@yourdomain.com
    redmine_domain: "redmine.yourdomain.com"

    # You could also use a domain set in your inventory file, 
    # ex : redmine_domain: "{{ hostvars[groups['redmine_server'][0]]['red_domain'] }}"
    # will use the red_domain property of the first host defined in a group remdine_server

## Setup your emails to receive from: 

    redmine_email_receive:
      enabled: false
      username: emailuser
      password: emailpassword
      default_project: defaultprojecttoassignnew
      server: imap_server
      port: 993
      ssl: SSL
      allow_override: project,tracker,status,priority,category,assigned_to,fixed_version,start_date,due_date,estimated_hours

# Backup server

    redmine_backup_user: "sysuser"
    redmine_backup_password: "password"
    redmine_backup_server: "ssh_user"

    redmine_custom_shared_dir: "/usr/local/share/redmine_custom"
    usr_local_bin: "/usr/local/bin"

# Repositories to clone 

    redmine_repositories:
      reponame:
        project: "project_name_to_associate"
        repositoryurl: "git@server:repo/name.git"
        repositorydir: "name.git"

# plugins for redmine

    redmine_plugins_dir: "/usr/share/redmine/plugins"
    redmine_dir: "/usr/share/redmine"

# User to clone git-repositories

    redmine_git_repos: "/opt/repositories"
    redmine_git_user: "www-data"
    redmine_git_user_home: "/var/www"
    redmine_git_user_password: "generate it with normal mkpasswd"

### After installing redmine go to admin / settings / repositories

    # Enable: Enable WS for repository management
    # Paste here your key
    redmine_api_key: "somecode"
    gitlab_server: "gitserverip"

Adding repositories
==================

To clone a repositories you must edit redmine_repositories var as shown in Vars. 
Also, you must add to deploy keys the public key used for redmine_git_user. 

You must also have to enable the WS redmine_api_key and it must be configured on this role. 

Finally add to the web hooks:

http://redmineuy.group.upm.com/gitlab_hook?project_id=yourassociatedprojectforthisrepo&key=yourredmine_api_key

(don't use ssl verification for this case)

Add the repository to your project in redmine /projects/projectname/settings/repositories


Dependencies
------------

Galaxy role : ANXS.mysql

Example Playbook
----------------


    - hosts: servers
      roles:
         - { role: radamanth.redmine-ansible }

License
-------

GPLV2

Author Information
------------------
Radamanth:
I've been a computer science engineer for more than 10 years now, I've discovered Ansible in 2014, and fell in love with it. I use it in my company to manage different server since then. Feel free to visit our site www.neovia.fr

I'm also one of the founder of Immozeo, where Ansible is also greatly used. ( www.immozeo.com)


