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
- Create auto scaling group - Configure subnets
- Set scaling policies- Define capacity, min and max instances. Add policies like target tracking, step scaling
- Add cloudwatch alarms for metrics like CPU Utilization, network In/Out, Request count


<img width="1890" height="676" alt="image" src="https://github.com/user-attachments/assets/f10b6d2e-bf86-4bd7-8dff-e5ded7ebf86f" />

---------------------------------------------------------------------------------------------

What is the difference between stopping and terminating an EC2 instance?
-
- STOP - Instance shuts down. EBS volume remains intact. We can start it again
- TERMINATE :- Permenant deletion. EBS volume also deleted. Need to re launch instance

---------------------------------------------------------------------------------------------

How do you attach and detach Elastic IPs? What happens if you restart the instance?
-
- Allocate new elastic IP from console. Associate with EC2 so it becomes public IP of instance unless we detach it
- If we restart the EC2, only public IP changes, EIP remains same even after restart
- EIP is static public IP basically

---------------------------------------------------------------------------------------------

How can you resize or change the instance type of an EC2 without downtime?
-
- Put EC2 behind ALB/NLB to ensure traffic is distributed and we can add/remove instances without affecting users
- Launch new EC2 template
- Use auto scaling groups
- Wait for health checks as ELB ensure new instances are healthy before accepting traffic
- ASG/ELB auto routes traffic to new instances. Once stable, reduce desired capacity to remove old instace type

---------------------------------------------------------------------------------------------

Explain the difference between EBS, Instance Store, and EFS with EC2
-
- EBS :- Network attached block storage. Persistent. To store data like OS files, app data
- EFS :- Network file system. Shared across multiple EC2 instances. Scales automatically and good for microservices

---------------------------------------------------------------------------------------------

How do you increase the size of an EBS volume attached to an EC2 instance? Steps involved?
-
- Identify volume IDof EBS attached to EC2
- Select volume - Modify in UI - Increase size, change volume type if needed - Modify
- Chack status as volume goes to modifying state, wait until its available
- Extend file system on EC2

---------------------------------------------------------------------------------------------

Difference between Elastic Load Balancer (ELB) and Auto Scaling? How do they work together with EC2?
-
- ELB distributes traffic across multiple instances. Used for traffic management HTTP/S/TCP. Ensures HA
- ASG auto adjusts no of EC2 instances based on demand. Used for scaling instances for performance and cost efficiency. Used to launch or terminate EC2 auto

- ELB receives traffic and distributes to healthy instances. ASG monitors metrics and adds/removes EC2 as needed
- ELB auto includes new EC2 in target group and stops sending traffic to terminated or unhealthy instances

---------------------------------------------------------------------------------------------

You deployed an application on an EC2 instance but it’s not reachable from the internet. How would you troubleshoot?
-
- Check security groups, inbound rules allowing traffic
- Check NACLs
- Check public/Elastic IP, for private only IPs, instance sont be accessible from internet
- Check instance state running, verify app is listening on correct port
- Check LB if used
- Check connectivity and logs

---------------------------------------------------------------------------------------------

Your EC2 instance is taking too long to boot. What steps would you take to debug?
-
- Check system logs, look for errors during boot like mounting volumes, services failing
- Ensure root volume is not corrupted
- Check instance type has enough resources
- Check for misconfigured AMI

---------------------------------------------------------------------------------------------

Your application needs to persist logs even if the EC2 instance is terminated. How would you design this?
-
- Use EBS volumes with "Delete on Termination = false"
- Use S3 for centralized logging
- Stream cloudwatch logs  for real time monitoring

---------------------------------------------------------------------------------------------

A dev team requests access to EC2 instances without sharing PEM keys. How would you manage this securely?
-
- I would use IAM roles with AWS Systems Manager Session Manager to grant developers secure, auditable access to EC2 instances without sharing PEM keys
- Optionally using Secrets Manager for any temporary credentials
