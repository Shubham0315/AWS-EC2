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
- Here we dont need dedicated people for timely upgrade, verify vulnerabilities, server issue, etc. AWS takes careof these. Here management effort has gone down and cost as well.

- As AWS has very huge network of resources, they get them at very low cost and we use these resources from AWS in "Pay as you Go" manner. So if we dont want these servers to be up during the night, or any time, we can shut them down and AWS wont charge.
- Thats why people are moving towards EC2 instances

- Main reasons for moving towards EC2/public cloud :-
  - Get rid of maintenance overhead
  - Cost effectiveness
  - Elastic nature

-------------------------------------------------------------------------------------------------

Types of EC2 Instances
-
- 
