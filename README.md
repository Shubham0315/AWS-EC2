# AWS-EC2

The project contains EC2, its types, Regions and Availability Zones in AWS with detailed practical on EC2 instance creation

- Most widely used and most popular AWS Service

Elastic Cloud Compute (EC2)
-
- Compute means we request AWS to provide compute instance which is combo of CPU, RAM and disk space. So we're basically asking AWS to provide Virtual Server. 
  - **Virtual Machine** :- Laptop is a physical server which we use. This laptop has to be used by multiple people. So we can install hypervisor on our physical machine and create logically isolated VMs so that other people can use laptop. Virtualization means using physical machines and hypervisors, share the machine across multiple people.
- AWS has multiple physical servers across world.
  When we request AWS for EC2 instance in specific region of the world (Asia pacific, Eu), it takes the request to hypervisor and gives us VM which is our EC2 instance.
- Cloud means AWS is public cloud platform. So EC2 is cloud compute instance we're getting.

- Elastic (many AWS services has this prefix) as any service can be scaled up and scaled down(increase resources/decrease them) Elastic in nature.
  - e.g:- EC2, EKS, ELB, EBS
- In short EC2 means we request public cloud provider like AWS to give a Compute engine(VM) on my cloud platform which is elastic in nature

-------------------------------------------------------------------------------------------------

Why EC2 is used?
-
- As a devops engineer we start creating instances, install hypervisor after buying physical servers. On top of physical servers we'll install hypervisor and start creating VMs and provide them to team for use.
- If there're 100 requests and we've to create 1000 VMs using Shell scripts. Here creation is easy but then we've to timely upgrade, verify vulnerabilities, server issue. To manage 1000's of such servers is huge headache for devops engineer/sys admin. So major advantage moving to public cloud platform is to get rid of this maintenance.
- So we need to move to public cloud platform to get rid of maintenance, cost and management of resources
- Here we dont need dedicated people for timely upgrade, verify vulnerabilities, server issue, etc. AWS takes care of these. Here management effort has gone down and cost as well.

- As AWS has very huge network of resources, they get them at very low cost and we use these resources from AWS in "Pay as you Go" manner. So if we dont want these servers to be up during the night, or any time, we can shut them down and AWS wont charge.
- Thats why people are moving towards EC2 instances

- Main reasons for moving towards EC2/public cloud :-
  - Get rid of maintenance overhead
  - Cost effectiveness
  - Elastic nature

-------------------------------------------------------------------------------------------------

Types of EC2 Instances
-
- There are 5 types of EC2 instances
  - General Purpose
  - Compute Optimised
  - Memory Optimised
  - Storage Optimised
  - Accelerated Compute

- **Compute** :- provides higher ratio of compute power(RAM) compared to memory. Used in machine learning models or gaming instance
- **Memory** :- provides high memory and handles intensive workloads. Used in case of high performance computing apps.

- When we request for EC2 from AWS, it asks which type of instance is required. Depending upon application, we can choose EC2 instance required. AWS charges for the instance types accordingly.
  - Memory optimised instance price will be higher than general purpose
 
-------------------------------------------------------------------------------------------------

Regions and Availability Zones
-
- AWS have their data centers over the world like US, Europe, Asia. These are Regions in AWS.

- Lets assume we're working for European client who wants their data to be sensitive and close to their location. So as DevOps engineer, we will create EC2 instance close to client location in Europe region, they dont want to put their data outside their country. If for client in Europe we create EC2 in India, there will be latency problem .
- So when client makes request for info or data, there is latency
- Latency means time taken for the request to reach app and for app to send response back. If there is delay means high latency, if no delay means low latency.

- Inside regions we have multiple availability zones. In India region, AWS has data centers in multiple zones
- If our application is down in region due to some reasons customer will face downtime. To avoid this AWS provides Zones in regions (us-east-1a and us-east-1b) (they dont reveal serevr and data centre's exact location). So even if one of the zone goes down, customer will access it from other available zone in that region. This is done to have High Availability for our application.
- Both zones will be identical in nature to have similar application interface.

-------------------------------------------------------------------------------------------------

Practical Demo
-
- AWS have its data centres in the below regions. Its on us where in which region we've to create resources.
- Our client might want their data to be within their country only, so we create instance in that region. So to have low latency, we create instances in appropriate region.

![image](https://github.com/user-attachments/assets/4097a0e3-7b6b-43b6-ad88-e7249a0e91d3)

- To create EC2 instance
  - Go to EC2 service - Go to instance - Click "Launch Instance"
 
![image](https://github.com/user-attachments/assets/945958ed-5e75-43a5-9b18-6414fc6a4964)

  - Provide Instance name - Choose OS (Heart of our VM) distribution - Provide free tier version (To avoid being charged) - Select Instance type "t2.micro"

![image](https://github.com/user-attachments/assets/d4eaa56b-b7ac-4560-9203-20ecf45f3f4e)
![image](https://github.com/user-attachments/assets/190861f5-7e39-49fd-a596-f91f186e7e08)

  - Now we've to create key-value pair to help us login to instance. If we've instance in "North-virginia", to connect to that instance we use "key-value" pair. By default while creating instance, AWS doesnt provide any password, means password authentication to instance is disabled by default. Thats why key-value pair is used which is combo of public and private key.
  - Create new key-value pair - Provide name - Click RSA token

![image](https://github.com/user-attachments/assets/68a356e2-baa8-4f23-9ba7-22f852f47020)
![image](https://github.com/user-attachments/assets/1768d8e4-bb62-42af-bfbd-7382336277bc)

  - After all is done, launch the instance. We can see our instance is launched
  
![image](https://github.com/user-attachments/assets/dca70951-974e-4edd-ab7c-35c5dfca58fb)

  - Clicking on instance, we get all its information like public IP (to login the instance from outside world, app inside instance can be accessed),

![image](https://github.com/user-attachments/assets/4ee50971-151a-4963-91ed-b5f2df850ae1)
 
  - By default, our EC2 have only 8GB RAM (very less).
  - Once the work is done, we need to turn off the instance to avoid being charged

- To login EC2 using local, use mobaxterm. Take session - provide Public IP and EC2 name with .pem file.

![image](https://github.com/user-attachments/assets/786d3f68-4bbb-496c-b7b7-26ad246f7c48)

- Another way to connect we can do using EC2 UI only

<img width="959" alt="image" src="https://github.com/user-attachments/assets/15a5e122-c637-43d0-bb4a-b16018d04e5e" />

![image](https://github.com/user-attachments/assets/f845232f-c2a1-4711-9207-f8c59cec0516)

- Another way using putty is open the terminal. To connect use below command
  - **Command** :- ssh -i /download/aws-login.pem ubuntu@PublicIP
  - Make sure the .pem file has 600 permissions.
  - This command says ssh to EC2 and use the .pem file to connect to ubuntu instance created in AWS using public IP
  - Now after running the command, we'll get logged into the instance and do the required tasks onto it.

- If we're on ubuntu user we need to update the packages :- **sudo apt update**
  - Its recommended to update the packages whenever we login to EC2.

![image](https://github.com/user-attachments/assets/f5ac653a-e946-4a14-b4a0-033b18dfbb33)


1. Now lets deploy application on EC2. Jenkins install and access from browser
  - Search for Jenkins install on Google to get commands to run on EC2.
  - Login to root :- **sudo su -**
  - Pre requisites are Java :- **apt install openjdk-11-jdk**

![image](https://github.com/user-attachments/assets/559eb1fa-aafe-44d1-aaee-60b781b52612)
![image](https://github.com/user-attachments/assets/ed4e4367-545c-40c5-9903-fbe9c3e7c60a)

  - To verify java installed :- **java --version**

![image](https://github.com/user-attachments/assets/090747c6-1cfa-4d89-9355-db10a7c4fac9)

2. Now install Jenkins
  - Command :- sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

![image](https://github.com/user-attachments/assets/0e84068a-7afc-406c-b1cf-25b99bac8208)

  - Now check if jenkins server is up and running. By default it will not be accessible
  - Command :- **systemctl status jenkins**
  - By default our jenkins run on port 8080. So to access jenkins :- http://publicIP:8080
  - To expose this port - Security groups - Inbound traffic rules - Edit Inbound traffic rules - Add rule providing port accessible from anywhere (IpV4) - Save rule

![image](https://github.com/user-attachments/assets/f45eaae1-f356-4b00-84e8-48eea6c0c2a4)
![image](https://github.com/user-attachments/assets/be4c60f0-cea3-4fd7-b711-9830861c125a)

  - Now we can see our jenkins console is accessible from outside world

![image](https://github.com/user-attachments/assets/aa17f699-175f-4674-8510-0761ae66205e)

