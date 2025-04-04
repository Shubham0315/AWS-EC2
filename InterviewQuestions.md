Explain the difference between On-Demand, Reserved, and Spot instances.
-
- On demand
  - It is pay as you go.
  - Used for short term, unpredictable workloads (test/dev, prod)
  - Flexible but most expensive
 
- Reserved
  - 75% cheaper than on demand
  - Used for predictable/steady workloads (DB, backend apps)
  - Less flexible but cost effective

- Spot
  - 90% cheaper than on demand
  - Fault tolerant, stateless workloads (CICD, image/video rendering)
  - Extremely cost effective but can be interrupted anytime

--------------------------------------------------------------------------------------------- 

What is the role of a security group in EC2 in short 
-
- SG is virtual firewall that controls inbound and outbound traffic to our instances
- It defines which traffic is allowed from and to instance at instance level.
- It is stateful so return traffic is auto allowed

---------------------------------------------------------------------------------------------

What is EBS volume in EC2?
-
- EBS - Elastic Block store
- It is durable, block level storage device that we can attach to our EC2
- Used to store data like OS files, databases, app data
- Persists independently of EC2 - data is not lost even if EC2 stops or terminates
- Can be attached to one EC2 at a time and to other instances in same AZ
- GP2, GP3 - Balanced performance EBS

---------------------------------------------------------------------------------------------

How do you attach and detach an EBS volume from an EC2 instance?
-
- To prepare volume - EC2 - Volumes - Our Volume - Actions - Set device name - Attach

![image](https://github.com/user-attachments/assets/788ce1c6-91c7-4e1b-bbc8-4fd96cbf20a8)

- Same for detach

---------------------------------------------------------------------------------------------

What is the difference between public IP, private IP, and Elastic IP in EC2?
-
- Public IP
  - Auto assigned to instances in public subnets
  - Used for internet communication (SSH, HTTP)
  - Changes when we start/stop instance
  - Dynamic internet address
 
- Private IP
  - Assigned inside VPC
  - Used for internal communication between EC2 instances
  - Doesnt change
  - Permanent like LAN address
 
- Elastic IP
  - Static IP we allocate to our AWS account
  - Can be attached/detached to/from any instance in same region
  - Stays same, no change

---------------------------------------------------------------------------------------------

How can you access a Linux EC2 instance if you’ve lost the key pair?
-
- Use EC2 instance connect
- Create new key pair and attach to instance by first stopping instance, detach root EBS volume, modify keys and start EC2
- Use Systems manager - If EC2 has SSM enabled and IAM role has proper permissions, we can connect instance using session manager

---------------------------------------------------------------------------------------------

Explain EBS volume types: gp2, gp3, io1, st1, sc1, etc.
-
- gp2 :- Genereal purpose SSD. Used for general workloads like databases, dev/test env.Size upto 1TB to 16TB
- gp3 :- General purpose SSD- Next generation. Better performance and lower cost than gp2. Ideal for workloads with moderate to high performance requirements.. Cheaper than gp2. Size upto 1TB to 16TB
- standard :- Legacy HDD storage for apps requiring lower cost and less demanding performance. Size upto 1 TB

---------------------------------------------------------------------------------------------

How do you configure Auto Scaling for EC2 instances?
-
- Configuring Auto scaling for EC2 ensures your app auto adjusts no of running instances based on demand,

- Go to EC2 dashboard - Launch template with AMI ID, Instance type, key pair, SG
- Ctreate auto scaling group - Configure subnets
- Set scaling policies- Define capacity, min and max instances. Add policies like target tracking, step scaling
- Add cloudwatch alarms for metrics like CPU Utilization, network In/Out, Request count
