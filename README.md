# RedHatAMQBrokerHACluster

Configuring leader-follower broker deployments that use a shared journal 

You can configure leader-follower broker deployments that persist messages to a journal on a volume that is shared by both broker instances.

Prerequisite

You created a Persistent Volume Claim (PVC) to request a shared volume to store messaging data for both brokers. Give careful consideration to ensure that the capacity you request is sufficient to store the messaging data on the shared volume. In the following PVC example, 2 gigabytes storage capacity is requested.






After deploying Master/Slave Cluster 
only Master  will be in Ready State.Slave will remain in Not Ready State Untill Slave Became master 
NAME                 READY   STATUS             RESTARTS         AGE
peer-broker-a-ss-0   1/1     Running            0                72m
peer-broker-b-ss-0   0/1     Running            0                72m
peer-broker-c-ss-0   0/1     Running            0                72m

Configuring data mirroring for disaster recovery 

Mirroring is the process of copying data from a broker to one or more other brokers for disaster recovery. The source and target brokers in a mirror can be on separate OpenShift clusters in different data centers to protect against a data center outage. Mirroring can also be used for data backup or to create a failover broker for use during maintenance windows. Messages that existed before a mirror is created are not mirrored.
