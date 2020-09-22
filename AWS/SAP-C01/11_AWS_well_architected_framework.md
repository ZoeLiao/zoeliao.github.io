# 01. AWS Well-Architected Framework
- [Official Guide - 2020/07](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)

## The five pillars of the AWS Well-Architected Framework  

| Name | Description|
|------|------------|
|Operational Excellence |The ability to support development and run workloads effectively, gain insight into their operations, and to continuously improve supporting processes and procedures to deliver business value.|
|Security |The security pillar encompasses the ability to protect data, systems, and assets to take advantage of cloud technologies to improve your security.|
|Reliability |The reliability pillar encompasses the ability of a workload to perform its intended function correctly and consistently when it’s expected to. This includes the ability to operate and test the workload through its total lifecycle. This paper provides in-depth, best practice guidance for implementing reliable workloads on AWS.|
|Performance Efficiency |The ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.|
|Cost Optimization |The ability to run systems to deliver business value at the lowest price point.|

- Architecture: being how components (code, configuration, AWS Resources) work together in a workload (identify a set of components that together deliver business value). How components communicate and interact is often the focus of architecture diagrams.
- When architecting workloads, you make trade-offs between pillars based on your
business context.

---

## Operational Excellence
### Design Principles
- Perform operations as code
- Make frequent, small, reversible changes
- Refine operations procedures frequently
- Anticipate failure
- Learn from all operational failure

### Whitepaper
- [Operational Excellence Pillar](https://d1.awsstatic.com/whitepapers/architecture/AWS-Operational-Excellence-Pillar.pdf)

---

## Security
### Design Principles
- Implement a strong identity foundation:
    - Implement the principle of least privilege and enforce separation of duties with appropriate authorization for each interaction with your AWS resources. Centralize identity management, and aim to eliminate reliance on long-term static credentials.
    - the principle of least privilege: 用戶創建時都無權限，需要再開。
    - eliminate reliance on long-term static credentials: 盡量不要用 AWS access key & access ID，可用 AWS STS (AWS Security Token Service)
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

### Whitepaper
- [Security Pillar whitepaper](https://d1.awsstatic.com/whitepapers/architecture/AWS-Security-Pillar.pdf)
