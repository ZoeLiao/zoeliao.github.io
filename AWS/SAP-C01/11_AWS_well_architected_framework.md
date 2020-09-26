# 01. AWS Well-Architected Framework
- Reference:
    - [AWS Well-Architected Framework - 2020/07](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)
    - [Cloud Native](https://www.oreilly.com/library/view/cloud-native/9781492053811/)


## The five pillars of the AWS Well-Architected Framework 
The five concepts are ubiquitous, you can find them in the documentations of GCP and Azure.
- GCP: [https://cloud.google.com/architecture/framework](https://cloud.google.com/architecture/framework)
- Azure: [https://docs.microsoft.com/zh-tw/azure/architecture/framework/](https://docs.microsoft.com/zh-tw/azure/architecture/framework/) 

| Name | Description|
|------|------------|
|Operational Excellence (卓越營運)|The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.|
|Security (安全)|The security pillar encompasses the ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security.|
|Reliability (可靠性)|The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle. This paper provides in-depth, best practice guidance for implementing reliable workloads on AWS.|
|Performance Efficiency (效能效率)|The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.|
|Cost Optimization (成本最佳化)|The ability to run systems to deliver business value at the lowest price point.|

- Architecture: being how components (code, configuration, AWS Resources) work together in a workload (identify a set of components that together deliver business value). How components communicate and interact is often the focus of architecture diagrams.
- When architecting workloads, you make trade-offs between pillars based on your
business context.

---

## 1. Operational Excellence (卓越營運)
### Design Principles
- Perform operations as code, such as infrastructure as code (IaC), e.g., AWS Cloud Formation
- Make frequent, small, reversible changes
- Refine operations procedures frequently
- Anticipate failure
- Learn from all operational failure

### Whitepaper
- [Operational Excellence Pillar](https://d1.awsstatic.com/whitepapers/architecture/AWS-Operational-Excellence-Pillar.pdf)

---

## 2. Security (安全)
### Design Principles
- Implement a strong identity foundation:
    - Implement the principle of least privilege and enforce separation of duties with appropriate authorization for each interaction with your AWS resources. Centralize identity management, and aim to eliminate reliance on long-term static credentials.
- Enable traceability:
    - Monitor, alert, and audit actions and changes to your environment in real time. Integrate log and metric collection with systems to automatically investigate and take action. 
- Apply security at all layers:
    - Apply a defense in depth approach with multiple security controls. Apply to all layers (for example, edge of network, VPC, load balancing, every instance and compute service, operating system, application, and code).
- Automate security best practices:
    - Automated software-based security mechanisms improve your ability to securely scale more rapidly and cost-effectively. Create secure architectures, including the implementation of controls that are defined and managed as code in version-controlled templates
- Protect data in transit and at rest:
    - Classify your data into sensitivity levels and use mechanisms, such as encryption, tokenization, and access control where appropriate.
- Keep people away from data:
    - Use mechanisms and tools to reduce or eliminate the need for direct access or manual processing of data. This reduces the risk of mishandling or modification and human error when handling sensitive data.
- Prepare fore securiy events:
    - Prepare for an incident by having incident management and investigation policy and processes that align to your organizational requirements. Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery. 

### Definition
- Security
- Identity and Access Management
- Detection
- Infrastructure Protection
- Data Protection
- Incident Response

### Security
- To operate your workload securely, you must apply overarching best practices to every area of security.
- In AWS, segregating different workloads by account, based on their function and compliance or data sensitivity requirements, is a recommended approach.

### Identity and Access Management
- How to:
    - Identity and access management are key parts of an information security program, ensuring that only authenticated (signed in) and authorized (has permissions) users and components are able to access your resources, and only in a manner that you intend.
    - For example, you should define principals (that is, accounts, users, roles, and services that can perform actions in your account), build out policies aligned with these principals, and implement strong credential management. These privilege-management elements form the core of authentication and authorization.
- Identity
    - Human Identity
    - Machine Identity
- Credentials must not be shared between any user or system. User access should be granted using a least-privilege approach with best practices including password re- quirements and MFA enforced. Programmatic access including API calls to AWS ser- vices should be performed using temporary and limited-privilege credentials such as those issued by the AWS Security Token Service.

### Detection
- You can use detective controls to identify a potential security threat or incident.
- You can also use internal auditing, an examination of controls related to information systems, to en- sure that practices meet policies and requirements and that you have set the correct automated alerting notifications based on defined conditions.

### Infrastructure Protection
- Infrastructure protection encompasses control methodologies, such as defense in depth, necessary to meet best practices and organizational or regulatory obligations.
- For example: VPC

### Data Protection
- In AWS, the following practices facilitate protection of data:
    - As an AWS customer you mainta in full control over your data.
    - AWS makes it easier for you to encrypt your data and manage keys,including regular key rotation, which can be easily automated by AWS or maintained by you.
    - Detailed logging that contains important content, such as file access and changes, is available.
    - AWS has designed storage systems for exceptional resiliency. For example, Amazon S3 Standard, S3 Standard–IA, S3 One Zone-IA, and Amazon Glacier are all designed to provide 99.999999999% durability of objects over a given year. This durability level corresponds to an average annual expected loss of 0.000000001% of objects.
    - Versioning, which can be part of a larger data life cycle managementprocess, can protect against accidental overwrites, deletes, and similar harm.
    - AWS never initiates the movement of data between Regions. Content placed in a Region will remain in that Region unless you explicitly enable a feature or leverage a service that provides that functionality.
- The following questions focus on these considerations for security:
    - How do you classify your data?
    - How do you protect your data at rest?
    - How do you protect your data in transit?

### Incident Response
- Preparation is critical to timely and effective investigation, response to, and recovery from security incidents to help minimize disruption to your organization.
- In AWS, the following practices facilitate effective incident response:
    - Detailed logging is available that contains important content, such as file access and changes.
    - Event scan be automatically processed and trigger tools that automate responses through the use of AWS APIs.
    - You can pre-provision tool in ganda “clean room” using AWS CloudFormation. This allows you to carry out forensics in a safe, isolated environment.

### Whitepaper
- [Security Pillar whitepaper](https://d1.awsstatic.com/whitepapers/architecture/AWS-Security-Pillar.pdf)

---

## 3. Reliability (可靠性)
- The Reliability pillar includes the reliability pillar encompasses the ability of a work- load to perform its intended function correctly and consistently when it’s expected to. this includes the ability to operate and test the workload through its total lifecycle.

### Design Principles
- 1.Automatically recover from failure
- 2.Test recovery procedures
- 3.Scale horizontally to increase aggregate workload availability
- 4.Stop guessing capacity
- 5.Manage change in automation 

### Whitepaper
- [Reliability Pillar whitepaper](https://d1.awsstatic.com/whitepapers/architecture/AWS-Reliability-Pillar.pdf)
