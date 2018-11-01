# Installation of filebeat

We install 2 instances for filebeat, one for usual logs goig directly to elasticsearch, 
and one for the specialized mylog that relates on log aggregation in logstash.


## Install filebeat on centos 7

Filebeat from (version should match the versions of the elasticsearch, logshash and kibana)
    https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html

Take the rpm way.

filebeat is installed on system with config in ```/etc/filebeat``` and a `filebeat` daemon in `/etc/init.d/`.


### Install config files

Copy the file in ```etc/filebeat``` to ```/etc/filebeat``` on the servers where filebeat is installed.

### Install service files

copy the files in ```etc/rc.d/init.d``` to ```/etc/rc.d/init.d``` on the servers where filebeat is installed.

### setup files in elasticsearch and kibana

Run the following commands:

    sudo filebeat -c /etc/filebeat/filebeat_logs.yml setup --template -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["elasticsearchhost:9200"]'
    sudo filebeat -c /etc/filebeat/filebeat_logs.yml setup -dashboards
    sudo filebeat -c /etc/filebeat/filebeat_logs.yml setup -e

### Start the services

Run the 2 commands:
   
    sudo service filebeat_logs start
    sudo service filebeat_mylog start

We probably need to investigate whether the services start after boot.


## NOTE

### Wrong timestamp from logfiles

For the system module - make sure Your timestamps are correct from the log files:
e.g. /var/log/messages specifies time as ```Jul  5 10:53:04``` without timezone.

In ```/etc/filebeat/modules.d/system.yml``` You need to enable timezone convert:

Set it to ```var.convert_timezone: true``` and
1.	Stop Filebeat
2.	Enable UTC time conversion in system.yml (see above)
3.	Delete pipelines 
    curl -XDELETE 'http://elasticsearchhost:9200/_ingest/pipeline/filebeat-*'
4.	Restart filebeat

We should probably find a more permanent solution here...


