# ansible-newrelic-npi
Ansible role which installs New Relic Platform Installer (npi) and adds npi ansible module.

#### Requirements & Dependencies
- Tested on Ansible 1.9.


#### Variables

```yaml
newrelic_license_key: YOUR_LICENSE_KEY
newrelic_npi_platform: debian
newrelic_npi_arch: x64
```


#### Module npi

Allows to install npi modules in Ansible tasks.

Example usage:

```yaml
- name: install newrelic mysql module
  hosts: mysql
  tasks:
  - npi: name=com.newrelic.plugins.mysql.instance config='{"agents":[{"name":"Staging Database","host":"localhost","metrics":"status,newrelic","user":"","passwd":""}]}'

```

#### License

Licensed under the BSD License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/ei-grad/ansible-newrelic-npi/issues)!
