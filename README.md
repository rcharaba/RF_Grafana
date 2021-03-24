# RF_Grafana
Robot Framework Grafana Dashboard using Jenkins influxdb plugin as exporter 

![alt text](https://github.com/rcharaba/RF_Grafana/blob/main/Diagram.PNG)   

![alt text](https://github.com/rcharaba/RF_Grafana/blob/main/Grafana_RF_Dashboard.PNG) 

Metrics Covered By Robot Framework Grafana Dashboard :

Execution Status - By build number    
Total Executions - Over Time Period    
Average Pass and Failure Percentage  
EMTE - Equivalent Manual Test Effort    
Top 10 Failed Test Cases    
All Execution Status By build number   
Average Execution Time    
Execution Trend Graph  

REF: https://grafana.com/grafana/dashboards/11541

### Prerequisites
1. Jenkins installed in your DEV environment
2. Grafana/InfluxDB(version: 1.8.3) installed in your DEV environment
3. Install Robot Framework plugin on Jenkins [click here](https://plugins.jenkins.io/robot/)
4. Intall InfluxDB plugin on Jenkins [click here](https://plugins.jenkins.io/influxdb/)

### Configuring InfluxDB (Server side)

Once you have installed InfluxDB, configure the authentication in the server side:
```
$ sudo vim /etc/influxdb/influxdb.conf
[http]
auth-enabled = true
```
Then create a user with an authentication password:
```
curl -XPOST "http://localhost:8086/query" --data-urlencode \
"q=CREATE USER username WITH PASSWORD 'strongpassword' WITH ALL PRIVILEGES"
```
Now to access influxDB using CLI:
```
$ influx -username 'username' -password 'password'
```
Create your database:
```
CREATE DATABASE robotdb
```
Test if it was created properly:
```
> show databases
name: databases
name
----
_internal
robotdb
```

### Configuring InfluxDB (Jenkins side)

Inside Jenkins you have to do 2 configuration:

1. In "Manage Jenkins" > "Configure System"
![alt text](https://github.com/rcharaba/RF_Grafana/blob/main/Jenkins_InfluxDB_general_config.png) 

2. In "Your Robot Job" > "Configure" > "Add post-build action" Select "Publish build data to InfluxDB"
![alt text](https://github.com/rcharaba/RF_Grafana/blob/main/Jenkins_InfluxDB_job_publish.PNG) 


### Configuring Grafana Dashboard
1. In "Configuration" > "Data Source" Adds new influxDB
![alt text](https://github.com/rcharaba/RF_Grafana/blob/main/Grafana_Influx_databse_config.PNG) 

2. Import the Robot Framework dashboad in "Create" > "Import"
3. Copy and paste the [json](https://github.com/rcharaba/RF_Grafana/blob/main/Robot_Framework_Grafana_Dashboard.json) file content and click in "Load"
4. Enjoy! :)

## Authors

* **Rodrigo Charaba** - https://github.com/rcharaba 

