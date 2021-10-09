Hello

In this project the goal is to install kubernetes cluster using vagrant and configuration management tool ansible. After that I intructed to set metric server and kubernetes dashboard. Let's begin.


***Installing Vagrant***

Vagrant is insfrastructure provisioing tool which is handy to setup any light weight lab environment easily. For my lab I installed Vagrant on a Arch OS (Kernel - 5.14.9). For installing vagrant follow the below instruction:

sudo pacman -S vagrant

For installing ansible

sudo pacman -S ansible

As a vagrant provider I have used Oracle virtual box. 

 
***Creating a Vagrantfile***

Now create a directory named DevOps and inside it create another directory named Task-2 and created a Vagrantfile there. Now add the below line of code there. 

<Check the vagrant file in the Task-2/kubernetes-installation>

***Now Create an Ansible playbook for Kubernetes master***

Create a directory named kubernetes-setup in the same directory as the Vagrantfile. Create two files named master-node-ansible-playbook.yml and worker-node-ansible-playbook.yml in the directory kubernetes-setup.

In the file master-node-ansible-playbook.yml, add the code below.

<Check the master-node-ansible-playbook.yml file in the folder>


***Create the Ansible playbook for Kubernetes node***

Create a file named worker-node-ansible-playbook.yml in the directory kubernetes-installation.

Add the code below into worker-node-ansible-playbook.yml

<Check the worker-node-ansible-playbook.yml file in the Task-2//kubernetes-installation>



***Upon completing the Vagrantfile and playbooks follow the below steps***

Go to the directory Devops/Task-2/ and then run "vagrant up"

Your 1 master 2 worker node kubernetes cluster will be installed. Now we will install kubernetes dashboard and metric server. 


The version of the kubernetes installed: 1.22.2
Cgroup drive used = systemd

***Dashboard Installaion***
ssh into your masternode by runnig this command vagrant ssh kube-master-node and then run the below snippet.

kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.3.1/aio/deploy/recommended.yaml

After that run "kubectl proxy" command from the node you want to view the dashboash
You can see the Dashboard by this link: 
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/



***Metric server installation***

For this ssh into the master node using "vagrant ssh kube-master-node" and run this command. "git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git"
This will download all the files needed for metric server. 
After that go to the directory named Kubernetes-metrics-server and run "kubectl apply -f ."

This install all the necessary kubernetes objects for metric server. Now create some pods and wait for sometime to load the metric server. 
After a while run "kubectl top pods" to view the resource consumption of your pod and "kubectl top nodes" for node resource consumption. 


Thanks!
