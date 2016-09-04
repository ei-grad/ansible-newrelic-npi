# ansible-newrelic-npi
Ansible role which installs New Relic Platform Installer (npi) and adds npi ansible module.

#### Requirements & Dependencies
- Tested on Ansible 1.9 and 2.1 (2.0 was broken).


#### Variables

```yaml
newrelic_license_key: YOUR_LICENSE_KEY
newrelic_npi_platform: debian
newrelic_npi_arch: x64
```

### npi - Manages npi packages

#### Synopsis

Manages npi packages.

#### Requirements

* Bash
* npi (installed by newrelic-npi role)

#### Options

 parameter | required | default | choices        | comments
 --------- | -------- | ------- | -------------- | -----------------------------------------------------------
 `name`      | yes      |         |                | npi package name, ex. - com.newrelic.plugins.mysql.instance
 `state`     | no       | present | present,absent | should the package be installed or removed
 `config`    | no       |         |                | package.json config file contents
 `config_file` | no       |         |                | remote(!) file name to be used as package.json

#### Examples

First - run this role to install the npi binary:

```yaml
- name: install newrelic npi
  hosts: mysql
  roles:
  - newrelic-npi
```

Then you could use npi to install and remove newrelic modules:

```yaml
- name: install newrelic mysql module
  hosts: mysql
  tasks:
  - npi: name=com.newrelic.plugins.mysql.instance state=present config='{"agents":[{"name":"My Ansible-managed database","host":"localhost","metrics":"status,newrelic","user":"","passwd":""}]}'
```

```yaml
- name: install newrelic mysql module (using template module to pass package.json)
  hosts: mysql
  tasks:
  - template: src=package.json dest=/tmp/package.json
  - npi: name=com.newrelic.plugins.mysql.instance state=present config_file=/tmp/package.json
```

```yaml
- name: remove newrelic mysql module
  hosts: mysql
  tasks:
  - npi: name=com.newrelic.plugins.mysql.instance state=absent
```

#### License

Licensed under the BSD License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/ei-grad/ansible-newrelic-npi/issues)!
