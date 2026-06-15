## Example
To load the extension into Velonetics you need to specify it in the extra_config section of the config:
```
"extra_config":{
...
"github_com/velonetics/velonetics-influx":{
      "address":"http://192.168.99.9:8086",
      "ttl":"25s",
      "buffer_size":0
    },
...
````
The necessary parameters are:

 - address - the url of the influxdb complete with port if different from http/https
 - ttl - expressed as \<value>\<units> , you can find accepted values here https://golang.org/pkg/time/#ParseDuration
 - buffer_size - 0 to send events immediately or the number of points that should be sent together. 

For this to work you need to have velonetics-metric activated as well in extra_config:
```
...
"github_com/velonetics/velonetics-metrics": {
        "collection_time": "30s",
        "listen_address": "127.0.0.1:8090"
    }
...
```  
The collection_time and ttl parameters are strongly linked. The module velonetics-metrics collects the metrics every **collection_time**, while velonetics-influxdb checks every **ttl** if there are collected points to be sent.

You can find an example configuration in this folder as well as a dashboard JSON file for Grafana 5.0+.
 