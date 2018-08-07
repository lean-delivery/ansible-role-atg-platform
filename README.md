atg-platform
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-atg-platform/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-atg-platform.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-atg-platform)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-atg-platform/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-atg-platform)

## Summary
--------------

This role installs the Oracle ATG Web Commerce platform (ATG platform) on Linux platforms, which is a highly customizable, configurable framework for building and supporting Web sites, particularly sites used for e-commerce.


Requirements
--------------

 - Minimal Version of the ansible for installation: 2.5
 - **Supported ATG versions**:
   - 10.x
   - 11.0
   - 11.1
   - 11.2
   - 11.3
   - _lower and higher versions should be retested_
 - **Supported application servers**
   - JBoss
 - **Supported OS**:
   - CentOS
     - 6
     - 7

For more information regarding support matrix please visit <https://support.oracle.com>

Java and application server should be installed preliminarily:
  - lean_delivery.java
  - lean_delivery.jboss


```
For test scenarios atg-platform/requirements.yml is used  
If another roles/versions are required, put requirements.yml to molecule/<scenario_name> and remove in molecule.yml lines  
  options:  
    role-file: requirements.yml
```


Role Variables
--------------

  - `atg_user` - user for installing atg (best practice is to use the same user as for installed application server, e.g. jboss)
  - `atg_group` - group for atg user

  - `transport` - artifact source transport  
     Available:
      - `web` - fetch artifact from custom web uri
      - `local` - local artifact

  - `transport_web` - URI for http/https artifact  e.g. "http://my-storage.example.com/V78217-01.zip"
  - `transport_local` - path for local artifact e.g. "/tmp/V78217-01.zip"

  - `download_path` - local folder for downloading artifacts  
    default: `/tmp/`

  - `atg_version` - ATG Platform version

  - `dynamo_root` - where ATG Platform should be installed  
    default: `/opt/atg/ATG{{ atg_version }}`

  - `app_server` - selected application server  
    default: `jboss`

  - `atg_listen_port` - listen port for silent install properties file  
    default: `8080`

  - `atg_rmi_port` - rmi port for silent install properties file  
    default: `8860`


Example Playbook
----------------

### Installing ATG from local:
```yaml
- name: "Install ATG 11.3 from local"
  hosts: all

  roles:
    - role: lean_delivery.java
      java_major_version: 7
      java_minor_version: 80
      transport: "local"
      transport_local: "/tmp/jdk-7u80-linux-x64.tar.gz"
    - role: lean_delivery.jboss
      transport: "local"
      transport_local: "/tmp/jboss-eap-6.1.0.zip"
    - role: lean_delivery.atg-platform
      atg_version: "11.3"
      transport: "local"
      transport_local: "/tmp/V861209-01.zip"
```

## License

Apache2

## Authors

  - Anastacia Maletskaya  
    <anastacia_maletskaya@lean-delivery.com>
