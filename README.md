# bind-update
Playbook to update ISC BIND using community.general.nsupdate

You'll create two survey questions asking for:

hostname
ip_addr

Once you enter those answers, the execution environment will update
the DNS zone using TSIG. Note that the EE needs to have community.general
included. This is the execution-environment.yml I used to build the EE.

version: 3
images:
  base_image:
    name: registry.redhat.io/ansible-automation-platform-25/ee-minimal-rhel8:latest
dependencies:
  ansible_core:
    package_pip: ansible-core
  ansible_runner:
    package_pip: ansible-runner
  galaxy:
    collections:
      - name: community.general
  python: 
    - dnspython
options:
  tags:
    - ee-minimal-rhel8-nsupdate
  package_manager_path: /usr/bin/microdnf

