# Introduction to Cloud Computing and AWS

**Understand AWS platform architecture.** AWS divides its servers and storage devices into globally distributed regions and, within regions, into availability zones. These divisions permit replication to enhance availability but also permit process and resource isolation for security and compliance purposes. You should design your own deployments in ways that take advantage of those features.

**Understand how to use AWS administration tools.** While you will use your browser to access the AWS administration console at least from time to time, most of your serious work will probably happen through the AWS CLI and, from within your application code, through an AWS SDK.

**Understand how to choose a support plan.** Understanding which support plan level is right for a particular customer is an important element in building a successful deployment. Become familiar with the various options.

# Amazon Elastic Compute Cloud and Amazon Elastic Block Store

**Understand how to provision and launch an EC2 instance.** You'll need to select the right AMI and instance type, configure a security group, add any extra storage volumes that might be needed, point to any necessary user data and scripts, and, ideally, tag all the elements using descriptive key values.

**Understand how to choose the right hardware/software profile for your workload.** Consider the benefits of building your own image against the ease and simplicity of using a marketplace, community, or official AMI. Calculate the user demand you expect your application to generate so you can select an appropriate instance type. Remember that you can always change your instance type later if necesarry.

**Understand EC2 pricing models and how to choose one to fit your needs.** Know how to calculate whether you'll be best off on the spot market, with on-demand, or with reserve--or some combination of the three.

**Understand how to configure a security group to balance access with security to match your deployment profile.** Security groups act as firewalls, applying policy rules to determine which network traffic is allowed through. You can control traffic based on a packet's protocol and network port and its source and intended destination.

**Know how to access a running instance.** Instance data, including private and public IP addresses, can be retrieved from the AWS Console, through the AWS CLI, and from meta-data queries on the instance itself. You'll need this information so you can log in to administrate the instance or access its web-facing applications.

**Understand the features and behaviour of storage volume types.** SSD volumes can achieve higher IOPS and, therefore, latency byt come at a cost that's higher than traditional hard drives.

**Know how to create a snapshot from a storage volume and how to attach the snapshot to a different instance.** Any EBS drive can be copied and either attached to a different instance or used to generate an image that, in turn, can be made into an AMI and shared or used to launch any number of new instances.

# Amazon Simple Storage Service and Amazon Glacier Storage

**Understand the way S3 resources are organized.** S3 objects are stored in buckets whose names must be globally unique. Buckets are associated with AWS regions. Objects are stored within buckets on a "flat" surface, but prefixes and delimiters can give data the appearance of a folder hierarchy.

**Understand how to optimize your data transfers.** While the individual objects you store within an S3 bucket can be as large as 5 TB, anything larger than 100 MB *should* be uploaded with Multipart Upload, and objects larger than 5 GB *must* use Multipart Upload.

**Understand how to secure your S3 data.** You can use server-side encryption to protect data within S3 buckets using either AWS-generated or your own privately generated keys. Data can be encrypted even before being transferred to S3 using client-side encryption.

**Understand how S3 object durability and availability are measured.** The various S3 classes (and Glacier) promise varying levels of infrastructure reliability, along with data availability.

**Understand S3 object versioning and lifecycle management.** Older versions of S3 objects can be saved even after they've been overwritten. To manage older objects, you can automate transition of objects between more accessible storage classes to less expensive but less accessible classes. You can also schedule object deletion.

**Understand how to secure your S3 objects.** You can control access through the legacy, bucket, and object-based ACL rules or by creating more flexible S3 bucket policies or, at the account level, IAM policies. You can also provide temporary access to an object using a presigned URL.

**Understand how to create a static website.** S3-based HTML and media files can be exposed as a website that, with the help of Route 53 and CloudFront, can even live behind a DNS domain name and use encrypted HTTPS pages.

**Understand the differences between S3 and Glacier.** Glacier is meant for inexpensive long-term storage for data archives that you're unlikely to need often.

# Amazon Virtual Private Cloud

**Be able to determine the correct prefix length for a CIDR block based on the number of IP addresses you need in a VPC or subnet.** Allowed prefix lengths range from /16 to /28. The longer the prefix length, the fewer the number of IP addresses you'll have available.

**Understand the significance of a subnet.** A subnet is a logical container that holds EC2 instances. Each subnet has a CIDR block derived from the CIDR of the VPC that it resides in. An instance in the subnet must take its private IP address from the subnet's CIDR. But AWS reserves the first four and last IP addresses in every subnet.

**Know the impact of availability zone failure.** If a zone fails, every subnet in that zone--and every instance in that subnet--will likewise fail. To tolerate a zone failure, build redundancy into your instance deployments by spreading them across different zones.

**Understand the rules for creating and using elastic network interfaces (ENIs).** Every instance must have a primary network interface with a primary private IP address. Any additional ENI you attach to an instance must be in the same subnet as the primary ENI.

**Be able to create, modify, and use route tables.** Know the purpose of the main route table in a VPC and its relationship to the VPC's subnets. Also understand how to create a public subnet using an Internet gateway and a default route.

**Know the differences between security groups and networks access control lists.** Understand why a stateful security group requires different rules than a stateless NACL to achieve the same result.

**Understand how network address translation works.** Know the difference between NAT that occurs at the Internet gateway and NAT that occurs on a NAT device. Nat that occurs on a NAT device is also called port address translation (PAT). Multiple instances can share a single public IP address using a NAT device.

**Be able to create and configure VPC peering among multiple VPCs.** Know the limitations of VPC peering connections. VPC peering connections do not support transitive routing or IPv6. Inter-region peering is available for some regions.

# Databases

**Understand the differences between relational and nonrelational databases.** A relational database requires you to specify attributes up front when you create a table. All data you insert into a table must fit into the predefined attributes. It uses the Structured Query Language (SQL) to read and write data, and so it's also called a SQL database. A nonrelational database only requires you to specify a primary key attribute when creating a table. All items in a table must include a primary key but can otherwise have different attributes. Nonrelational--also called no-SQL databases--store unstructured data.

**Know the different database engines RDS supports.** RDS supports all of the most popular database engines--MySQL, MariaDB, Oracle, PostgreSQL, Amazon Aurora, and Microsoft SQL Server. Understand the difference between the bring-your-own-license and license-included licensing models. Know which database engines support which licensing models.

**Be able to select the right instance class and storage type given specific storage requirements.** Memory and storage tend to be constraining factors for relational databases, so it's crucial that you know how to choose the right instance class and storage type based on the performance needs of a database. Know the three different instance classes: standard, memory optimized, and burstable. Also know how these relate to the three different storage types: general purpose SSD(gp2), provisioned IOPS SSD (io1), and magnetic.

**Understand the differences between multi-AZ and read replicas.** Both multi-AZ and read replicas involve creating additional database isntances, but there are some key differences. A read replica can service queries, while a standy instance in a multi-AZ deployment cannot. A master instance asynchronously replicates data to read replicas, while in a multi-AZ configuration, the primary instance synchronously replicates data to the standby. Understand how Aurora replicas work and how Aurora multi-AZ differs from multi-AZ with other database engines.

**Be able to determine the appropriate primary key type for a DynamoDB table.** DynamoDB table give you two options for a primary key. A simple primary key consists of just a partition key and contains a single value. DynamoDB distributes items across partitions based on the value in the partition key. When using a simple primary key, the partition key must be unique within a table. A composite primary key consists of a partition key and a sort key. The partition key does not have to be unique, but the combination of the partition key and the sort key must be.

**Know how DynamoDB throughput capacity works.** When you create a table, you must specify throughput capacity in write capacity units and read capacity units. How many read capacity units a read consumes depends on two things: whether the read is strongly or eventually consistent and how much data you read within one second. For an item of up to 4 KB in size, one strongly consistent read consumes one read capacity unit. Eventually consistent reads consume half of that. When it comes to writes, one write capacity unit lets you write up to one 1 KB item per second.

# Authentication and Authorization--AWS Identity

**Understand how to work with IAM policies.** You can build your own custom IAM policies or select preset policies and apply them to identities to control their access to AWS resources.

**Understand how to protect your AWS account's root user.** You should lock down your root user and instead delegate day-to-day tasks to specially defined users.

**Understand how to optimize account access security.** You can use IAM administration tools to enforce the use of strong passwords and MFA, along with properly managed (rotated) access keys and tokens.

**Be familiar with the various AWS authentication and integration tools.** Cognito lets you manage your application's users, and Managed Microsofts AD applies Active Directory domains to compatible applications running in your VPC. Both permit federated identities (where users using external authentication services can be authenticated for AWS resources) through external providers.

# CloudTrail, CloudWatch, and AWS Config

**Know how to configure the different features of CloudWatch.** CloudWatch receives and stores performance metrics from various AWS services. You can also send custom metrics to CloudWatch. You can configure alarms to take one or more actions based on a metric. CloudWatch Logs receives and stores logs from various resources and makes them searchable.

**Know the differences between CloudTrail and AWS Config.** CloudTrail tracks events, while AWS Config tracks how those events ultimately affect the configuration of a resource. AWS Config organizes configuration states amd changes by resource, rather than by event.

**Understand how SNS works.** CloudWatch and AWS Config send notifications to an Amazon SNS topic. The SNS topic passes these notifications on to a subscriber, which consists of a protocol and endpoint. Know the various protocols that SNS supports.

# The Domain Name System and Network Routing

**Understand how DNS services enable predictable and reliable network communication.** DNS registration ensures that domain names are globally unique and accessible. Domain requests are resolved using name servers--both local and remote.

**Understand DNS naming conventions.** You should be familiar with "parsing" domain names. Each of the TLD, SLD, and subdomain/host sections will be read by DNS clients in a predictable way.

**Be familiar with the key DNS record types.** Recognize the function of key record types, including A and AAAAA (address records for IPv4 and IPv6), CNAME (canonical name record or alias), MX (mail exchange record), NS (name server record), and SOA (start of authority record).

**Be familiar with Route 53 routing policies.** Recognize the function of key routing policies, including simple (for single resources), weighted (routing among multiple resources by percentage), latency (low-latency content delivery), failover (incorporate backup resources for higher availability), and geolocation (respond to end user's location).

**Understand how to create a CloudFront distribution.** CloudFront distributions can be configured to deliver content through low-latency, geographically-based content to end users.

# The Reliability Pillar

**Know how to calculate total availability using both hard dependencies and redundant components.** When one resource depends on another, that's a hard dependency. An example would be an application dependent upon a database. When you have resources that don't depend on one another, such as a collection of identical application instances, those components are redundant.

**Understand the difference between traditional and cloud-native applications.** Traditional applications are written to run on Linux or Windows servers and often use a standard database component such as a SQL server or nonrelational database like Redis or MongoDB. Cloud-native applications, on the other hand, use compute, database, or networking resources available only in the cloud, such as Lambda and DynamoDB.

**Be able to configure EC2 Auto Scaling.** Auto Scaling can help you avoid application failures by automatically provisioning new instances when you need them, avoiding instance failures caused by resource exhaustion. When an instance failure does occur, Auto Scaling removes the instance from the associated Elastic Load Balancing target group.

**Understand the different backup and recovery options for S3, EBS, and EFS.** S3 offers versioning and cross-region application. To back up data stored on EBS volumes, you can take manual or automated EBS snapshots. EFS doesn't provide any native backup capability, but you can copy files from one EFS filesystem to another.

# The Performance Efficiency Pillar

**Understand the way EC2 instance types are defined.** Each EC2 instance type is designed to service a different function. You should be familiar with the individual parameters that are used to measure the way each type performs.

**Understand Auto Scaling.** The best way to efficiently meet changing demands on your application is to automate the process of provisioning and launching new resources as demand grows and shutting unused resources down as demand drops. Auto Scaling is the way AWS manages this functionality for EC2.

**Understand the value of serverless and container computing compared with EC2 instances.** By reducing the underlying resource footprint of your service, serverless functions, such as those offered through AWS Lambda, and clusters of Docker containers (offered through AWS ECS) can provide more responsive and cost-effective compute solutions. You should understand which model will work best for a given use case.

**Understand how to optimize storage performance and reliability.** Data stored on EBS volumes (using RAID) or in S3 buckets (using cross-region replication) can be replicated for greater durability and/or performance. You can also enable faster transfers in and out from S3 buckets using S3 transfer acceleration on CloudFront.

**Understand how to optimize database performance.** The performance, reliability, and costs you'll experience running a database on AWS will depend on the choices you make. How should you configure your underlying storage? Should you go with the managed RDS, build your database on an EC2 instance, or choose Redshift or a third-party integration for data warehouse management?

**Understand when and how to use a load balancer.** Load balancers direct incoming client requests among multiple backend servers. This allows for scalable and reliable application delivery, as failing or overloaded instances can be automatically replaced or supported by others. Load balancing of one sort or another is a critical component of many--if not most--EC2 and RDS workloads.

**Understand the value and function of infrastructure and automation tools.** CloudFormation templates can be used to define and then automatically provision and launch complex resource stacks in multiple environments. Similarly, third-party solutions like Chef and Puppet can be deployed through AWS OpsWorks to script environments. Continuous integration and continuous deployment processes can also be managed through AWS developer tools.

**Understand the importance of infrastructure monitoring and the tools available for the job.** It's critically important to stay on top of changes and performance trends within your infrastructure. Active load simulation testing is an important ongoing component of your administration process, as is visualizing the data that's produced using tools like CloudWatch Dashboards.

**Understand how caching can be used to improve performance.** ElastiCache and CloudFront are two services that replicate data and store it to make it quickly available to consuming clients. ElastiCache can use either Memcached or Redis--you should know which will work best for a given workload.

# The Security Pillar

**Be able to configure permission policies.** Permissions policies are the foundation of identity and resource-based policies. Understand the difference betwen these policies and be able to understand and create them. Identity-based policies are attached to an IAM principal such as a user or role. Resource-based policies apply to a resource and don't include the "principal" element.

**Know how permissions boundaries interact with permissions policies.** Permissions boundaries define the maximum permissions an IAM principal can have. You set permissions boundaries on a per-identity basis by attaching a managed policy that defines them.

**Understand roles and trust policies.** A role is set of permissions that an IAM user, AWS service, or federated user can acquire by assuming that role. Trust policies are resource-based policies that define who can assume the role and under what conditions.

**Know your options for collecting, searching, and analyzing logs.** CloudWatch Logs can consolidate logs from multiple sources, including CloudTrail, VPC flow logs, DNS query logs, and logs generated by your application. You can search logs from within CloudWatch Logs using filter patterns. For logs stored in S3, you can use Athena to search them using SQL queries.

**Be able to identify use cases for GuardDuty, Inspector, Shield and WAF.** GuardDuty analyzes various logs looking for signs of an attack. Inspector uses an agent to inspect your EC2 instances for vulnerabilities. Shield identifies and blocks well-known network-based attacks as they occur. WAF allows you to configure custom rules to block suspicious or undesirable traffic.

**Understand how KMS works.** Know how to create customer master keys and set key policies. A key policy defines the key users--IAM principals who can use a key to encrypt and decrypt data. A key policy also defines the administrators of a key--those who can enable and disable a key. Key administrators can also modify the key policy.

# The Cost Optimization Pillar

**Know how to effectively monitor costs incurred by your AWS account resource use.** AWS offers multiple tools to track your billing and usage activity to help you anticipate and prevent overages, spot and understand usage trends, and deeply analyze usage data. Tracking tools include Budgets, Cost Explorer, Cost and Usage Reports, and Trusted Advisor.

**Know how to simulate and anticipate the costs of AWS application stacks.** The Simply Monthly Calculator lets you quickly model multiple alternative resource stacks to accurately estimate and compare costs. The AWS Total Cost of Ownership calculator is built to closely compare the cost of deploying of an application stack on AWS versus the costs you'd face doing it on-premises.

**Understand how to match your application to the right EC2 instance type.** An EC2 instance type is built on a hardware profile that makes it particularly efficient for certain kinds of workloads. You should be familiar with at least the general instance family categories and their use cases.

**EC2 reserved instances can be configured for a wide range of uses.** You can reserve RIs as Convertible to allow you to exchange your instance type with another one during the reservation term or to permit use in any availability zone within your region. You can also schedule recurring time blocks for your RI.

**Spot fleets can be requested to provide multiple concurrent instances.** Complex combinations of multiple customized spot instances can be configured using prebuilt AMIs, durable capacity preferences, and lifecycle behaviour.

# The Operational Excellence Pillar

**Know how to use CloudFormation stacks.** A stack is a collection of AWS resources created by a CloudFormation template. These resources can be created, updated, and deleted as a group. Stacks can also pass information to each other through the use of output exports and nested stacks.

**Understand the use cases for CodeCommit and Git.** CodeCommit offers Git-based repositories for storing files. It provides automatic versioning and differencing, allowing multiple IAM users to collaborate on software development projects, document creation, and more.

**Be able to decide whether to use a blue/green or in-place deployment.** In a blue/green deployment you deploy an application to a new set of instances and then route traffic to them, resulting in minimal downtime. An in-place deployment is appropriate when you're initially deploying an application to existing instances. It's also a good option when you don't want to create new instances but are able to safely take your existing application offline to update it.

**Know how CodePipeline works.** CodePipeline lets you create workflows that define the different stages of software development, all the way from coding to deployment. It can integrate with other AWS and third-party tools to perform builds and unit testing.

**Understand the features of Systems Manager.** Systems Manager lets you automatically or manually take actions against your AWS resources and instances in bulk or individually. It also gives you insights into the state of your resources, such as compliance status and software inventory.

#### Authors: Ben Piper and David Clinton