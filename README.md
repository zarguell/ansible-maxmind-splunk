# Ansible Playbook Maxmind GeoLite2-City 

Goal: Check if Splunk needs a Maxmind update, get the latest .mmdb, and apply across a distributed environment.

While [apps](https://splunkbase.splunk.com/app/5482/) and [utilities](https://github.com/maxmind/geoipupdate) exist for updating directly, I specifically wanted a centrally managed way to check and deploy this.