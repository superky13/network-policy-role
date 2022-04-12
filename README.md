Role Name
=========

This role deploys a simple httpd Pod and Service as well as NetworkPolicy objects to: deny all traffic (unless explicitly defined as allowed); allow traffic from the ingress controller; allow traffic to a single port (8443) from Pods that have a label of 'app={{ match_label }}'

Requirements
------------

N/A 
This code will run with the default variables in defaults/main.yml

Role Variables
--------------

All variables are defined in defaults/main.yml

```

## namespace
ocp_namespace: 'zerotrust'

## webserver config
httpd_secure_port: 8443
app_name: 'httpd'
httpd_yml_files: ['httpddeployment.yml', 'httpdservice.yml']

## network policy objects
network_policy_yml_files: ['allowfromingress.yml.j2', 'allowsecurehttptraffic.yml', 'defaultdeny.yml.j2']

## matchlabel for ingress traffic (allowsecurehttptraffic policy will only allow secure traffic from pods with the following label)
match_label: 'zerotrustlabel'

```

Dependencies
------------

This role requires the kubernetes.core, cloud.common, and kubernetes (via pip):

```

ansible-galaxy collection install kubernetes.core
ansible-galaxy collection install cloud.common
pip3 install kubernetes

```

Example Playbook
----------------

Example playbook is found in tests (network_policy.yml)


License
-------

BSD
