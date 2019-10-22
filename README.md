# Pipelines
By standardising our environments, we can speed up the process of project delivery and deployment using the following techniques to automate our pipeline procedure:

![CICD_pipeline](https://www.edureka.co/blog/content/ver.1531719070/uploads/2018/07/Asset-33-1.png)

## Continuous Integration: CI

CI is the process of automating your environments in a pipeline to a point where a push on git or similar action can initiate a build (using Jenkins automation server) to test codes in the same environment as the where code was developed, informing us of how the code performed in the tests.

## Continuous Delivery: CD#1

CD#1 means automating your environments up to the CI stage where the tests are performed on the code, but once it has passed said tests, it is now ready to be used on the project or application. It then might be put in another (standardised) _staging_ environment, where it is ready to be rolled out on a larger scale, but is awaiting authorisation to do so. Alternatively, it might also wish to be carried out by only letting small numbers of users onto that environment to use the application at a time, so it can be tested in a real situation.

## Continuous Deployment: CD#2

CD#2 pipelining is achieved when both CI and CD#1 are completed, that being the code developed has passed the tests and is ready to be used. Then, when it is fully deployed to its are of usage in one automated procedure via testing in CI and perhaps staging in CD#1, the pipeline is said to be using Continuous Deployment.

###### Utilizing these three methods in a pipeline procedure can fully automate the testing, staging and deployment of code using standardised environments to minimise downtime and maximise delivery ability across a projects new development areas.

# Amazon Web Services (AWS) Functionality

![AWS_network](https://docs.aws.amazon.com/vpc/latest/userguide/images/security-diagram.png)

## Region
This is simply the region you specify when working with AWS, it specifies where the servers your using to host cloud services exist. We typically only operate in one region, as it can be hard to communicate between regions without using wider internet bandwidth.

## Virtual Private Cloud (VPC)
This is the first step towards working in AWS. You define a VPC to host all of your machine environments, and that can be further segmented into other useful functions.

We must define an IP address for our VPC, so that we can decide what small pieces of it can be a part of its network. For example, 10.10.0.0/16 has a CIDR block of 16, allowing us a load of other networks connected to it, as long as they have an IP address that starts with _10.10._, e.g. _10.10.10.0_.

Multiple different VPCs can exist in the same region, with their own unique ID, given to them at inception.

## Availability Zone
Availability Zones are used to keep the network up and running. Typically, each region will have 3 of these, so that if one were to fail, then the structures running on it can move to another and hosting services won't fail.

## Subnets
Subnets are sub-areas of your VPC, that are on the same network. They are given their own security rules (NACLs, which we'll come to later) and exist within the VPC. We are therefore able to set our own restrictions on them and how each subnet interacts with other subnets, and the VPC around it. It is a great way to compartmentalise what is happening inside your VPC, and separate concerns. This is a good way to escape from monolithic structures that fail if one component fails.

## Route Tables
Route tables tell the traffic in a VPC where to go. They tell traffic to pass from subnets in a VPC to elsewhere, be that other subnets, or most commonly, to the wider internet.

## Internet Gateway
This is a function that, when attached to our VPC, allows it to communicate with the wider internet. This is done through route tables directing subnets to the gateway.

We can also specify network access rules here, but since that will likely be done to a stronger degree in the other security settings, it might be practical to allow all traffic into this cloud and restrict unwanted access in other places.

## Network Access Control Lists (NACL)
These are a set of security restraints associated with a given _subnet_ (or the entire _VPC_ itself, although this is not common). They are rules provided that define which IP addresses can access the subnet through which ports. For instance, port 80 might be open to all IPs to allow HTTP traffic through. You might open port 22 on your IP so only you can access the SSH of your machine. This is the first line of security in stopping unwanted things coming into your machine and causing problems. We usually set up NACLs around our subnets to define what can go in or out from the internet, but we can also set them up to only allow traffic from other subnets, making that subnet well protected from the world.

## Machine instance
A Machine Instance is what you set up to be able to develop, test and generally maintain code. This is the environment where your functionality is carried out, and they are usually strategically placed within subnets, depending on their security requirements. It is one of the first steps towards standardisation of environments. This might be made on _EC2_, perhaps. You can _SSH_ into that machine to set up and/or run your desired programs.

## Security Groups
Security Groups are the next layer of security after NACLs. They are given to _each machine instance_ made in the VPC/subnet, providing more specific security to the instances that might be provided by an NACL, depending on whether you're considering inbound or outbound traffic. Again, they are usually a list of allowed ports from varying IP addresses, such as allowing GitHub access to your machine through certain ports to utilise a webhook. Together with NACLs, you can design a secure network with the correct capabilities to connect with the wider web (leaving yourself open to an external threat, maybe) or only allow internal access, for the likes of a secure database with customers' personal data.

For example, rules might be:

![security_rules_example](https://media.amazonwebservices.com/blog/2017/sg_rules_desc_3.png)
