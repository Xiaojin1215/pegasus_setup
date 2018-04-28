# pegasus_setup

Reference to: https://docs.google.com/document/d/1InLxbu-FH2nyd0NuJ3ewdvAt0Ttk_bNUwlQop38lq0Q/edit#
and : https://github.com/InsightDataScience/data-engineering-ecosystem/wiki/hadoop-intro

1. Make sure to terminate the extra instances of EC2
1. Download pegasus folder
2. Follow the Google Document to set up everything. Change the content in master.yml file and workers.yml file.
3. peg up master.yml
4. peg up workers.yml
5. After this, we can see those instances are active on the AWS console.
---
6. Follow the git readme hadoop-intro file.
7. Copy AWS pem-key from localhost to namenode 
  replace ~/.ssh/personal-aws.pem with your AWS account pem key
  replace namenode-public-dns with your namenode public-dns (can't use IP address, it should looks like: ubuntu@ec2-51-141-153-211.us-west-2.compute.amazonaws.com), which can be found in the AWS console. EC2 - instances -  select one node - we can find it at the bottom, named "Public DNS". 
8. Still follow the hadoop-intro file, ssh into the master machine. Generate an authorizaiton key for the master machine.
   Using ssh localhost to test if we can ssh to the local without password.
9. Follow the file, Copy the namenode's id_rsa.pub to the datanodes' authorized_keys
   Remember to replace the "datanode-public-dns" to all of the public dns you are going to set as your worker machine.
10. Try "peg fetch spark-cluster". 
11. If there is some error exists, like "Pseudo-terminal will not allocated because stdin is not a terminal. "
    Or "ssh: could not resolve hostname blahblah.compute-1blahblah". Then log into that machine. Repeat the "Generate an authorization key for the namenode" part in the hadoop-intro file, and copy this node's id_rsa.pub to other nodes' authorized_keys. Try Step 10 again.
12. If there is no error anymore. Although output of "peg fetch spark-cluster" is just one line "pem key *** found locally", is also ok.
13. Using "peg describe spark-cluster" to see if the nodes are set correctly.
14. Using "peg ssh spark-cluter 1/2/3/4" to ssh to those nodes.
15. After that, Follow the pegasus file to install some software. 
    For example, "peg install <cluster name> ssh" 
    If there is still some error like "permission denied!", that's because the key file!
    Log in to some machines, repeat the "Generate an authorization key for the namenode" and copy the id_rsa.pub to other nodes' authorized keys. After that, try "peg install <cluster name> ssh" again. 
16. Install Hadoop and Spark. 
  When you installed hadoop, and spark. If you see "Hadoop is missing.. Hadoop is installing...", this is normal! Because it is checking if you installed Hadoop in your machine before.
  If there is other errors, trying install it one more time. It the error keeps appear, you need to check the verion of your hadoop or spark is exist anymore. 
  
In my case: 
Spark Cluster WebUI is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:8080
Spark Job WebUI is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:4040
Spark Jupyter Notebook is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:8888
HDFS WebUI is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:50070
Hadoop Job Tracker WebUI is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:8088
Hadoop Job History WebUI is running at:
http://ec2-34-196-110-104.compute-1.amazonaws.com:19888


For Further using, we can change the instance_type in workers.yml and master.yml
For now, it is "m4.large", it can be changed to "c4.large, r3.large or p2.xlarge".
We can check the options in IAM Concole -- Policies -- InsightEC2Sandbox -- Permissions -- "ec2:InstanceType"

Hope everything goes well in the future! Au ma mi ma mi bei mei ho~~~~
