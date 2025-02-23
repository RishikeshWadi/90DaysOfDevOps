# Week 1: Networking Challenge
## Task 3
---
## What are Security Groups?
- Security Groups (SGs) are virtual firewalls that control inbound and outbound traffic to cloud resources like virtual machine, databases, and containers. They define what kind of network communication is allowed to and from an instance.

## How AWS Security Groups Work
- Security Groups are attached to EC2 instances, not the entire network.
- Each instance can have multiple security groups.
- Security Groups operate at the instance level (not at the subnet level like Network ACLs).
- They allow only explicitly defined traffic and block everything else by default.
- Any changes to a security group take effect immediately.

## Security Groups consist of two types of rules:

### Inbound Rules
    - These rules control incoming traffic to the instance.
    Example: If you want to allow SSH access to an EC2 instance, you define an inbound rule allowing TCP traffic on port 22 from a specific IP address.

### Outbound Rules
    - These rules control the traffic leaving the instance. (By default, AWS allows all outbound traffic unless explicitly restricted.)
    Example: Allow HTTP and HTTPS Access
    Protocol: TCP
    Port: 80 (HTTP) & 443 (HTTPS)
    Destination: 0.0.0.0/0 (all IPs)
---

# Steps for Creating and Configuring Security Groups

Security Groups are essential for controlling inbound and outbound traffic to resources in a cloud environment, 
---
## **Step 1: Access the AWS Management Console**
- Log in to your AWS account.
- Navigate to the **EC2 Dashboard**.
- In the left navigation pane, click on **Security Groups** under "Network & Security".
---
## **Step 2: Create a Security Group**
- Click the **Create Security Group** button.
- Enter a **Name** and **Description** for the security group.
- Select the **VPC** where you want the security group to be associated.
---
## **Step 3: Configure Inbound Rules**
Inbound rules define what kind of traffic is allowed to reach the instance.
- Click on the **Inbound Rules** tab.
- Click **Add Rule**.
- Choose a **Type** (e.g., SSH, HTTP, HTTPS, Custom TCP, etc.).
- Select a **Protocol** (automatically filled based on the type).
- Enter the **Port Range** (e.g., 22 for SSH, 80 for HTTP, 443 for HTTPS).
- Choose a **Source**:
   - **My IP**: Restrict access to your specific IP address.
   - **Custom**: Specify an IP address or another security group.
   - **Anywhere (0.0.0.0/0)**: Open to all IP addresses (not recommended for SSH or other sensitive ports).
- Click **Save Rules**.
---
## **Step 4: Configure Outbound Rules**
Outbound rules define what kind of traffic is allowed to leave the instance.
- Click on the **Outbound Rules** tab.
- Click **Add Rule**.
- Select a **Type**, **Protocol**, and **Port Range** (similar to inbound rules).
- Choose a **Destination**:
   - **Custom**: Specify an IP address or another security group.
   - **Anywhere (0.0.0.0/0)**: Allows all outgoing traffic.
- Click **Save Rules**.
---
## **Step 5: Associate the Security Group with an Instance**
- Navigate to the **EC2 Instances** page.
- Select the instance you want to associate with the security group.
- Click on **Actions > Networking > Change Security Groups**.
- Select the desired security group from the list.
- Click **Assign Security Groups**.
---
## **Step 6: Test the Security Group Rules**
- Try connecting to the instance using SSH, RDP, or a web browser, depending on the rules you configured.
- Use tools like `telnet`, `ping`, or `curl` to verify connectivity.
- Modify rules if needed to ensure proper access control.

---

# IAM (Identity and Access Management)

## What is  IAM?
- Identity and Access Management (IAM) is a service that enables you to securely manage access to AWS resources. 
- It allows you to create and control users, roles, and policies to define who can access what within your AWS environment.
---
## Key Components of IAM:
### Users: 
    - Represents individual people or applications needing access to AWS resources.
### Groups: 
    - Collections of users that share the same permissions.
### Roles: 
    - Used to grant permissions to AWS services or external entities (e.g., AWS Lambda, EC2, or other AWS accounts).
### Policies:
    - JSON-based documents that define permissions (who can access what and with what level of permission).
### Access Keys & MFA:
    - Provides authentication methods, including Multi-Factor Authentication (MFA) for extra security.

---