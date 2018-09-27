##### Description
This role is used by me for small hadoop cluster (mostly learning purposes)  
However with this role you can get simple hadoop cluster up and running in virtually no time  
This includes HDFS, MR and YARN, and can be installed in distributed mode on any amount of machines  
If you intend to use it for production... don't. Seriously, just dont.  
Take a look at ambari/cdh/hortonworks instead.

##### Usage
To install parts of hadoop stack on your machines, use this vars in playbook/hostvars:
```
hadoop_hdfs_namenode: true
hadoop_hdfs_secondarynamenode: true
hadoop_hdfs_datanode: true
hadoop_hdfs_nfs_gateway: true
hadoop_yarn_resourcemanager: true
hadoop_yarn_nodemanager: true
hadoop_mapred_historyserver: true
```

Also make sure to specify hadoop_master_host (where namenode and nodemanager is located).
If you have masters on separate machines, you can override them per-service:
```
hadoop_hdfs_master_host: 127.0.0.1
hadoop_yarn_master_host: 127.0.0.1
hadoop_mapred_master_host: 127.0.0.1
```
By default, those variables are aliased to hadoop_master
Everything else is optional, you can see that params in defaults/main.yml

##### Low spec mode
Setting hadoop_low_settings to true will use very low-end settings for hadoop, allowing you to run hadoop cluster on very low-end VPSes or even stuff like raspberrypi/orangepi and similar boards.

##### Default webui ports

###### hadoop2:

* 50070 - namenode web
* 50090 - secondarynamenode web
* 19888 - MR1 web
* 8088 - YARN web

###### hadoop3:

* 9870 - namenode web
* 9868 - secondarynamenode web

##### TBD:

* HDFS HA
* Multiple disk support for HDFS datanodes

###### Credits
Thanks to [this repo](https://bitbucket.org/lalinsky/ansible-hadoop) for like half of code here, especially systemd units
