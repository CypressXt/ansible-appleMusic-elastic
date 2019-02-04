# ansible-applemusic-elastic


## What for?
What is this ansible repo for ?

This ansible repo aim to configure an Elastic stack ready to host your [AppleMusic played history](https://github.com/CypressXt/AppleMusic-Elastic). You'll also be able to share it (read-only) publicly if you want to.

At the end you'll get:
 * An Elasticsearch server (admin only)
 * A Kibana web app (admin and read-only)
 * An Nginx with HTTP2 support and an [SSL grade of A](https://www.ssllabs.com/ssltest/analyze.html?d=music.cypress.cyprx.cloud)
 * A restrictive firewall configuration
 * An configured environment able to host your [AppleMusic played history](https://github.com/CypressXt/AppleMusic-Elastic)


## Installation

First you need to install some dependencies:
##### ansible galaxy roles
```bash
ansible-galaxy install geerlingguy.kibana
ansible-galaxy install geerlingguy.nginx
ansible-galaxy install geerlingguy.htpasswd
ansible-galaxy install geerlingguy.certbot
```

##### jmespath
The elasticsearch role uses the json_query filter which [requires jmespath](https://github.com/ansible/ansible/issues/24319) on the local machine.
```bash
sudo apt install python-jmespath
```

## Usage

##### Clone this repo

```bash
git clone https://github.com/CypressXt/ansible-applemusic-elastic.git
```

##### Configuration
Check and edit the [var file](vars/main.yml) with your custom values such as your fqdn, mail address for the [Let's Encrypt cert](https://letsencrypt.org/)...


Configure the [hosts file](hosts) with the proper hosts.
##### 3-2-1 Ignition

```bash
ansible-playbook -i hosts elastic.yml --ask-become-pass
```

## Ansible reporting for duty

Here is your final cheat-sheet:

| Service       | URL                            | PORT | Privileges | basic-auth |
|---------------|--------------------------------|------|------------|------------|
| Kibana        | https://music.mydomain.gg      | 443  | read-only  | ❌         |
| Kibana        | https://music.mydomain.gg:8443 | 8443 | admin      | ✅         |
| Elasticsearch | https://music.mydomain.gg:9200 | 9200 | admin      | ✅         |
