Examples

```yaml
---
- hosts: all
  vars:
    configRepoUrl: https://github.com/OutsideContextSolutions/ServerConfig.git
    baseDomain: outsidecontext.solutions

  # upstream: https://github.com/thefinn93/ansible-letsencrypt
  roles:
   - role: letsencrypt
     letsencrypt_email: root@outsidecontext.solutions
     letsencrypt_cert_domains:
       - outsidecontext.solutions
       - mail.outsidecontext.solutions
       - mailtesting.outsidecontext.solutions
       - newaeanalysis.outsidecontext.solutions
       - newae.outsidecontext.solutions
       - example-cms.outsidecontext.solutions
     letsencrypt_renewal_command_args: '--renew-hook "systemctl restart nginx"'
     letsencrypt_webroot_path: /var/www/html

   - role: uwsgiWebservice
     virtualenv_command: virtualenv -p /usr/bin/python3.4
     django: True
     user: example-cms
     plugin: python34
     branch: cmsConfig
     repo: git@github.com:OutsideContextSolutions/django-base.git
     module: wsgi:application
     domain: example-cms.outsidecontext.solutions
     templates:
         - source: Settings/settings.template.py
           destination: Settings/settings.py

```
