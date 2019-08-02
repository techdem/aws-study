# Introduction to Cloud Computing and AWS

- Cloud computing is built on the ability to efficiently divide physical resources into smaller but flexible virtual units. Those units can be "rented" by businesses on a pay-as-you-go basis and used to satisfy just about any networked application and/or workflow's needs in an affordable, scalable, and elastic way.
- Amazon Web Services provides reliable and secure resources that are replicated and globally distributed across a growing number of regions and availability zones. AWS infrastructure is designed to be compliant with best-practice and regulatory standards--although the Shared Responsability Model leaves you in charge of what you place *within* the cloud.
- The growing  family of AWS services covers just about any digital needs you can imagine, with core services addresing compute, networking, database, storage, security, and application management and integration needs.
- You manage your AWS resources from the management console, with the AWS CLI, or through code generated using an AWS SDK.
- Technical and account support is available through support plans and through documentation and help forums. AWS also makes white papers and user and developer guides available for free as Kindle books. You can access them at this address: `https://www.amazon.com/default/e/B007R6MVQ6/ref=dp_byline_cont_ebooks_1?redirectedFromKindleDbs=true`

# Amazon Elastic Compute Cloud and Amazon Elastic Block Store

- The base software stack that runs on an EC2 instance is defined by your choice of Amazon Machine Image and any scripts or user data you add at launch time, and the hardware profile is the product of an instance type. A tenancy setting determines whether your instance will share a physical host with other instances.
- As with all your AWS resources, it's important to give your EC2 instances easily identifiable tags that conform to a system-wide naming convention. There are limits to the number of resources you'll be allowed to launch within a single region and account-wide. Should you hit your limit, you can always request access to additional resources.
- If you plan to run an instance for a year or longer, you can save a significant amount of money over paying for on-demand by purchasing a reserve instance. If your workload can withstand unexpected shutdowns, then a spot instance could also make sense.
- There are four kinds of Elastic Block Store volumes: two high IOPS and low-latency SSD types and two traditional hard drives. Your workload and budget will inform your choice. In addition, some EC2 instance types come with ephemeral instance store volumes that offer fast data access but whose data is lost when the instance is shut down.
- All EC2 instances are given at least one private IP address, and should they require Internet access, they can also be given a nonpermanent public IP. Should you require a permanent public IP, you can assign an Elastic IP to the instance.
- You secure access to your EC2 instances using software firewalls known as security groups and can open up secure and limited access through IAM roles, NAT instances or NAT gateways, and key pairs.

# Amazon Simple Storage Service and Amazon Glacier Storage

- Amazon S3 provides reliable and highly available object-level storage for low-maintenance, high-volume archive and data storage. Objects are stored in buckets on a "flat" surface but, through the use of prefixes, can be made to appear as though they're part of a normal file system.
- You can--and usually should--encrypt your S3 data using either AWS-provided or self-serve encryption keys. Encryption can take place when your data is at rest using either server-side or client-side encryption.
- There are multiple storage classes within S3 relying on varying degress of data replication that allow you to balance durability, availability, and cost. Lifecycle management lets you automate the transition of your data between classes until it's not longer needed and can be deleted.
- You can control who and what get access to your S3 bucket--and when--through legacy ACLs or through more powerful S3 bucket policies and IAM policies. Presigned URLs are also a safe way to allow temporary and limited access to your data.
- You can reduce the size and cost of your requests against S3 and Glacier-based data by leveraging the SQL-like Select feature. You can also provide inexpensive and simple static websites through S3 buckets.
- Amazon Glacier stores your data archives in vaults that might require hours to retrieve but that cost considerably less than the S3 storage classes.

# Amazon Virtual Private Cloud

- The Virtual Private Cloud service provides the networking foundation for EC2 and other AWS services. AWS abstracts some networking components in such a way that their configuration is easier than in a traditional network, but you still need to have a solid grasp of networking fundamentals to architect VPCs.
- In each region, AWS automatically provides a default VPC with default subnets, a main route table, a default security group, and a default NACL. Many use a default VPC for a long time without ever having to configure a VPC from scratch. This makes it all the more important that you as an AWS architect understand how to configure a virtual network infrastructure from scratch. There's a good chance you won't be allowed to modify an infrastructure that was built on top of a default VPC. Instead, you may be tasked with replicating it from the ground up--troubleshooting various issues along the way. Practice what you've learned in this chapter until creating fully functional VPCs becomes second nature to you.
- In a traditional network, you're free to reconfigure server IP addresses, move them to different subnets, and even move them to different physical locations. You have tremendous flexibility to change your plans midstream. When creating a VPC, you don't have that luxury. You must carefully plan your entire application infrastructure up front, not just your network. It's therefore crucial that you understand how all of the VPC and EC2 components fit together.
- You begin by defining a contiguous IP address range for the VPC and representing it as a CIDR. The primary CIDR should ideally be sufficiently large to accommodate all of your instances, but small enough to leave room for a secondary CIDR.
- After that, you have to divvy up your VPC CIDR into subnets. Because a subnet is a container that resides in only one availability zone, you must make up-front decisions about where to place your instances. Once you create an instance in a subnet, you can't move it.
- Prior to launching instances, you need to configure security groups, as every instance's ENI must have at least one attached. One area where you do have some flexibility is with network access control lists. You can associate a NACL with a subnet at any time or forego NACLs altogether.
- If you want your instances to be accessible from the Internet, you must provision an Internet gateway, create a default route, and assign public IP addresses. Those are the basics. If you choose to use a NAT gateway or instance or a VPC peering connection, you'll have to modify multiple route tables.

# Databases

- Whether you implement a relational or nonrelational database depends solely on the application that will use it. Relational databases have been around a long time, and many application developers default to modeling their data to fit into a relational database. Appplications use database-specific SDKs to interact with the database, so often the needs of the application mandate specific database engine required. This is why AWS RDS offers six of the most popular database engines and sports compatibility with a wide range of versions. The idea is to let you take an existing database and port it to RDS without having to make any changes to the application.
- The nonrelational database is a more recent invention. DynamoDB is Amazon's proprietary nonrelational database service. Unlike applications designed for relational databases, an application designed for a nonrelational database generally cannot be ported from an on-premises deployment to DynamoDB without some code changes. You're therefore more likely to find cloud-native applications using DynamoDB. When developing or refactoring an application to use DynamoDB, there's a good chance that developers will need to consult with you regarding how to design the database. It's critical in this case that you understand how to choose partition and sort keys and data types and how to allocate throughput capacity to meet the performance needs of the application.
- Regardless of which database you use, as with any AWS service, you as an AWS architect are responsible for determining your performance and availability requirements and implementing them properly.

# Authentication and Authorization--AWS Identity

- The IAM root user that's automatically enabled on a new AWS account should ideally be locked down and not used for day-to-day account operations. Instead, you should give individual users the precise permissions they'll need to perform their jobs.
- All user account should be protected by strong passwords, multifactor authentication, and the use of encryption certificates and access keys for resource access.
- Once authenticated, a user can be authorized to access a defined set of AWS resources using IAM policies. It's a good practice to associate users with overlapping access needs into IAM groups, where their permissions can be centrally and easily updated. Users can also be assigned temporary IAM roles to give them the access they need, when they need it.
- Access keys should be regularly audited to ensure that unused keys are deleted and active keys are rotated at set intervals.
- Identities (including users, groups, and roles) can be authenticated using a number of AWS services, including Cognito, Managed Microsoft AD, and single sign-on. Authentication secrets are managed by services such as AWS Key Management Service (KMS), AWS Secrets Manager, and AWS CloudHSM.

# CloudTrail, CloudWatch, and AWS Config

- You must configure CloudWatch and AWS Config before they can begin monitoring your resources. CloudTrail automatically logs only the last 90 days of management events even if you don't configure it. It's therefore a good idea to configure these services early on in your AWS deployment.
- CloudWatch, CloudTrail, and AWS Config serve different purposes, and it's important to know the differences among them and when each is appropriate for a given use case.
- CloudWatch tracks performance metrics and can take some action in response to those metrics. It can also collect and consolidate logs from multiple sources for storage and searching, as well as extract metrics from them.
- CloudTrail keeps a detailed record of activities performed on your AWS account for security or auditing purposes. You can choose to log read-only or write-only management or data events.
- AWS Config records resource configurations and relationships past, present, and future. You can look back in time to see how a resource was configured at any point. AWS Config can also compare current resource configurations against rules to ensure that you're in compliance with wathever baseline you define.

# The Domain Name System and Network Routing

- The DNS system manages Internet resource addressing through two top-level name spaces: the Internet Protocol (IP addresses) and the domain name hierarchy. The Internet Corporation for Assigned Names and Numbers (ICANN) administrates name servers and domain name registrars (like Route 53) through registry operators (like VeriSign).
- A fully qualified domain name consists of a TLD (like org or com) and an SLD (like amazon). FQDNs are also often given a trailing dot representing "root".
- DNS configuration details are organized as hosted zones, where resource record sets are created to control the way you want inbound domain traffic to be directed. That behaviour can be defined through any one of a number of record types like A, CNAME, and MX.
- A newly created Route 53 hosted zone will contain a start of authority (SOA) record set and a list of name servers to which requests can be directed. You'll need to create at least one record set so Route 53 will know from which domain name to expect requests.
- Route 53 can be configured to regularly monitor the run status of your resources using health checks. Besides alerting you to problems, health checks can also be integrated with Route 53 routing policies to improve application availability.
- Weighted routing policies let you direct traffic among multiple parallel resources proportionally according to their availability to handle it.
- Latency routing policies send traffic to multiple resources to provide the lowest-latency service possible.
- Failover routing monitors a resource and, on failure, reroutes subsequent traffic to a backup resource.
- Geolocation routing assess the location of a request source and directs responses to appropriate resources.
- Amazon CloudFront is a CDN that caches content at edge locations to provide low-latency delivery of websites and digital media.

# The Reliability Pillar

- When it comes to maximizing availability, avoiding failure in the first place is job one. To avoid catastrophic application failures, run your application on multiple EC2 instances in different availability zones and distribute the load across those instances as much as possible using an application load balancer. If one instance or even an entire availability zone fails, ALB will route users away from the failed instances, and your application will continue to be available.
- Another way to avoid application failures is to not overload individual instances. This is where EC2 Auto Scaling comes in. By implementing dynamic scaling policies, you can ensure you always have enough instances to handle increased demand.
- But failures are inevitable, so the next highest priority is to recover from them quickly when they occur. When you create an Auto Scaling group, Auto Scaling will ensure you always have a minimum number of healthy instances. When an instance becomes unhealthy, Auto Scaling will terminate and replace it.
- One potential cause of application failures is lost or corrupt data. Take advantage of automatic S3 versioning, cross-region replication, and EBS snapshots to keep backups of your application's important data. For the database, use multi-AZ RDS and automated database instance snapshots to keep up-to-date copies of your database stored safely across multiple availability zones.

# The Performance Efficiency Pillar

- The performance and availability of EC2 instances can be managed by choosing the right instance type and by provisioning as many isntances as necesarry through Auto Scaling. Compute workloads can sometimes be more effectively delivered through serverless (Lambda) or container (Docker/ECS) models.
- Access to EBS volume-based data and data reliability can be enhanced by configuring RAID arrays. Cross-region replication and S3 transfer acceleration can improve S3 data administration.
- Carefully configuring details such as schemas, indexes, views, option groups, and parameters groups can improve the performance of your RDS databases. For manually hosted databases, latency issues can be addressed through volume class (magnetic versus SSD) and IOPS level; durability is improved through replication; and scalability can be manually configured.
- Load balancers listen for incoming requests and distribute them intelligently among all available backend resources. This allows for automated health checks and request routing policies that make the best use of your resources and provide the best end-user experience possible.
- Scripting resource provisioning using AWS-native tools like CloudFormation or third-party infrastructure automation tools like Chef and Puppet (working through AWS OpsWorks) can make it easy to quickly launch complicated resource stacks. This can make it possible to maintain multiple on-demand environments for testing, staging, and production.
- AWS Developer Tools (AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, and AWS CodePipeline) support continuous integration and continuous deployment environments including source code version control, application builds and testing, and deployment.
- You can monitor the state and performance of your resources using CloudWatch, CloudTrail, and AWS Config. It's important to incorporate load testing and report visualization (through CloudWatch Dashboards) into your administration cycles.
- You can decrease data response times by replication through caching, improve data processing performance through partitioning (sharding), and transfer large data stores more quickly through compression.

# The Security Pillar

- Effective security controls necessarily add more complexity to your deployment and will occasionally cause things to break. But by implementing security at every level, you can resolve those issues as you go along. Then by the time you're done, you'll be starting with an effective security posture. From that point on, it will be much easier to mitigate vulnerabilities and threats as they trickle in.
- It's fine to be a little lax when initially configuring a service just to make sure everything works as expected, but as soon as you do, be sure to implement your security controls. Follow the principle of least privilege, using IAM and resource-based policies and network-based controls. Configure logging early on to make troubleshooting easier. Set up encryption prior to going live so that your data is never sent or stored in the clear. Implement notifications for key events so you know immediately when a misconfiguration, attack, or error occurs. Finally, automate as much as possible using Auto Scaling, CloudFormation, and preconfigured AMIs. Automation allows you to recover more quickly from an incident. It also reduces human intervention, thus minimizing the chances of mistakes.

# The Cost Optimization Pillar

- AWS budgets can be created to watch all or selected areas of your account usage and alert you when costs approach specified tresholds. You can use cost allocation tags to efficiently focus your budgets on subsets of your running resources.
- You can track historical billing costs, rates, and product attributes using both Cost Explorer and Cost and Usage Reports. Reports, however, is designed for the kind of big data analytics needed by particular large-scale operations.
- You can consolidate billing and access management administration of multiple accounts belonging to a single owner using AWS Organizations.
- AWS Trusted Advisor monitors and reports on your account configuration status as it relates to best practices and account limits. The Simple Monthly Calculator and AWS Total Cost of Ownership are important tools for helping you find the most cost-effective and efficient way to build your application stack.
- Matching the right EC2 instance type and, where appropriate, running container workloads, are effective ways to maximize your use--and minimize the costs--of server resources.
- Your use of EC2 reserved instances can be optimized by selecting a convertible RI for greater long-term flexibility and by scheduling reserve availability for recurring blocks of time.
- Spot instances can be requested individually or as a fleet and can be set to react to shutdowns in ways that best fit your specific applications needs.

# The Operational Excellence Pillar

- Automation is certainly nothing new. System administrators have been writing scripts for decades to automate common (and often mundane) tasks. But in the cloud, automation can be extended to infrastructure deployments as well. Because of the flexibility of cloud infrastructure, the line between infrastructure--which has traditionally been static--and operations is becoming more blurred. In the cloud, deploying infrastructure and operating it are essentially the same thing.
- Despite this, there are some differences to keep in mind. Because the infrastructure belongs to AWS, you have to use the AWS web console, CLI, or SDKs to configure it. You can automate this using CloudFormation, or you can write your own scripts. Conversely, when it comes to configuring the operating system and applications running on instances, you can write scripts and use your own tooling, or you can use the services AWS provides, namely, the AWS Developer Tools and Systems Manager. The combination of scripts, tools, and services you use is up to you, but as an AWS architect, you need to understand all options available to you and how they all fit together.

#### Authors: Ben Piper and David Clinton