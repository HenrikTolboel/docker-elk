# Installation of metricbeat

We install one instance of metricbeat.

## Install metricbeat on centos 7

Metricbeat from (version should match the versions of the elasticsearch, logshash and kibana)
    https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-installation.html

take the rpm way

filebeat is installed on system with config in ```/etc/metricbeat```


### Install config files

Copy the file in ```etc/metricbeat``` to ```/etc/metricbeat``` on the servers where metricbeat is installed.

### setup files in elasticsearch and kibana

Run the following commands:

    sudo metricbeat setup --template -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["elasticsearchhost:9200"]'
    sudo metricbeat setup -dashboards
    sudo metricbeat setup -e

### Start the services

Run the command:
   
    sudo service metricbeat start

We probably need to investigate whether the services start after boot.

