# Ansible Playbook Maxmind GeoLite2-City 

Goal: Check if Splunk needs a Maxmind update, get the latest .mmdb, and apply across a distributed environment.

While [apps](https://splunkbase.splunk.com/app/5482/) ([another example](https://github.com/georgestarcher/TA-geoip)) and [utilities](https://github.com/maxmind/geoipupdate) exist for updating directly, I specifically wanted a centrally managed way to check and deploy this.

## Dependencies:
- ansible
- rsync
- gnu-tar

## Deployment Instructions

1. Create an inventory file, either in yaml or ansible hosts file. For this example, I'll create a ```servers.yml``` to contain a single splunk instance, and assume that I have ssh key access.

servers.yml:
```
all:
  vars:
    ansible_connection: ssh
    ansible_user: {{ INSERT YOUR ANSIBLE USER }}
    ansible_python_interpreter: /usr/bin/python3
    maxmind_key: {{ INSERT YOUR MAXMIND KEY HERE }}
  hosts:
    splunk:
      ansible_host: {{ DEFINE YOUR HOST(S) HERE }}
```

If you do not have, or want to sign up for a maxmind key, a good option is to retrieve the latest release from [P3TERX/GeoLite.mmdb](https://github.com/P3TERX/GeoLite.mmdb), which has automated github actions publishing the mmdb to a release.

2. In the main.yml, review the variables to ensure:
- geoip_dir matches directory to sync GeoLite db to
- geoip_name matches destination name
- local_download_directory matches a directory on your ansible control host (localhost) to save the initial downloads to

the other variables are static or placeholder at this time


3. Run playbook:

```
ansible-playbook -i servers.yml main.yml
```