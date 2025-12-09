# RedHatAMQBrokerHACluster
This procedure shows how to use OperatorHub to deploy the latest version of the Operator for AMQ Broker to a specified OpenShift project.

Note
In OperatorHub, you can install only the latest Operator version that is provided in each channel. If you want to install an earlier version of an Operator, you must install the Operator by using the CLI. For more information, see Section 3.2, “Installing the Operator using the CLI”.

Prerequisites




The Red Hat Integration - AMQ Broker for RHEL 9 (Multiarch) Operator must be available in OperatorHub.
You have cluster administrator privileges.
Procedure

Log in to the OpenShift Container Platform web console as a cluster administrator.
In left navigation menu, click menu:Operators[OperatorHub].
On the Project drop-down menu at the top of the OperatorHub page, select the project in which you want to deploy the Operator.
On the OperatorHub page, use the Filter by keyword…​ box to find the Red Hat Integration - AMQ Broker for RHEL 9 (Multiarch) Operator.


also add view role to default service account :::
oc policy add-role-to-user view -z default


Configuring leader-follower broker deployments that use a shared journal 

You can configure leader-follower broker deployments that persist messages to a journal on a volume that is shared by both broker instances.

Prerequisite

You created a Persistent Volume Claim (PVC) to request a shared volume to store messaging data for both brokers. Give careful consideration to ensure that the capacity you request is sufficient to store the messaging data on the shared volume. In the following PVC example, 2 gigabytes storage capacity is requested.






After deploying Master/Slave Cluster 
only Master  will be in Ready State.Slave will remain in Not Ready State Untill Slave Became master  



 
   NAME                 READY   STATUS            
   peer-broker-a-ss-0   1/1     Running           
   peer-broker-b-ss-0   0/1     Running            
   peer-broker-c-ss-0   0/1     Running            

Configuring data mirroring for disaster recovery 

Mirroring is the process of copying data from a broker to one or more other brokers for disaster recovery. The source and target brokers in a mirror can be on separate OpenShift clusters in different data centers to protect against a data center outage. Mirroring can also be used for data backup or to create a failover broker for use during maintenance windows. Messages that existed before a mirror is created are not mirrored.


Test Message:


oc rsh peer-broker-a-ss-0

cd amq-broker
./bin/artemis

Red Hat AMQ Broker 7.13.2.GA >      producer --url tcp://172.16.1.76:61616 --user admin --password admin --destination myqueue --message-count 10 --message  "hello from prod master "




Configuring authentication and authorization:

oc create secret generic custom-jaas-config --from-file=login.config --from-file=new-users.properties --from-file=new-roles.properties


The secret name must have a suffix of -jaas-config so the Operator can recognize that the secret contains login module configuration and propagate any updates to each broker Pod.

The Operator mounts the login.config file in the secret in a /amq/extra/secrets/secret name directory on each Pod and configures the broker JVM to read the mounted login.config file instead of the default login.config file. If the login.config file contains a properties login module, the referenced users and roles properties file are also mounted on each Pod.


