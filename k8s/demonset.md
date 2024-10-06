### DaemonSet
A DaemonSet ensures that a specific pod runs on all (or some) nodes in the cluster. As new nodes are added to the cluster, the DaemonSet automatically schedules pods on them. Similarly, when nodes are removed, the pods running on those nodes are cleaned up. DaemonSets are often used for services that need to run on every node, such as monitoring agents, logging agents, or system utilities.


#### Use Cases for DaemonSets:
1. Log collection: Running a logging agent (e.g., Fluentd or Filebeat) on every node to collect and ship logs.
2. Monitoring: Running monitoring agents (e.g., Prometheus node exporter) on every node to collect metrics.
3. System utilities: Running network or storage utilities on every node, such as network proxies or distributed storage daemons.


#### Example DaemonSet:
Here’s an example of a DaemonSet that runs a Fluentd logging agent on every node to collect logs. 
yml is here,
demonset.yml
