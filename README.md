iptables-dcos
=========

This ansible can be used to secure a Mesosphere DCOS cluster using iptables. This role can prevent the cluster from malicious attack. So this role will help us to filter the incooming traffic so that unwanted traffic can be dropped. This role can setup iptables at each node with different rules. A cluster can have different types of nodes, so iptables rules has to be different for each type of nodes. A mesosphere DCOS cluster can have three types of nodes: Masters, Public agents, Private agents
 
So Here are multiple scenerios which we want to achieve:

1. All the nodes of the cluster should be able to communicate with each other on all the ports.
2. SSH and Ping must be allowed on all the nodes from everywhere.
3. Only basic ports should be opened for incoming traffic such as 22, 80, 443, 53 etc.
4. None of the private nodes should be able to communicate directly from outside of the cluster.
5. As there are Docker containers running on each node of DCOS cluster so these rules should also take care of Docker communication. 


Requirements
------------

OS- CentOS

As we know that there are 3 types of nodes in a DCOS cluster, So we have to define different groups in inventory file. Here is the example of inventory file. 

NOTE : Group names must be same as below.

[dcos-cluster]
mesos-agent
mesos-master

[mesos-master]
#List of all the masters

[mesos-agent]
#List of all agents, Note: public and private both

[public-agent]    
#List of only public agents


Role Variables
--------------

iptables_allowed_tcp_ports_public  #Array of basic ports to be opened over public agents for the traffic coming from outside of cluster 
iptables_allowed_tcp_ports_master  #Array of basic ports to be opened over masters for the traffic coming from outside of cluster
iptables_confdir                   #iptables configuration directory over CentOS  
iptables_rules_path                #path of iptables configuration file 

Dependencies
------------

No dependency

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

   - hosts: dcos_cluster
     gather_facts: True
     become: yes
     roles:
       - iptables-dcos      



