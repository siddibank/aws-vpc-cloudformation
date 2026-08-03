# AWS VPC Deployment Using AWS CloudFormation

## Project Overview

This project demonstrates how to automate the deployment of an AWS Virtual Private Cloud (VPC) using AWS CloudFormation.

Rather than manually provisioning networking resources through the AWS Management Console, the entire infrastructure is deployed from a single YAML template using Infrastructure as Code (IaC). This approach improves consistency, reduces manual effort, and makes the infrastructure easier to manage and reproduce.

The CloudFormation template provisions a complete networking environment, including a VPC, Internet Gateway, Public and Private Subnets, Route Table, Internet Route, and Route Table Association, following AWS networking best practices.

---

## Project Objectives

This project was completed to achieve the following objectives:

- Understand Infrastructure as Code (IaC) using AWS CloudFormation.
- Automate the deployment of AWS networking resources.
- Create and configure an Amazon VPC.
- Deploy both Public and Private Subnets.
- Configure Internet connectivity using an Internet Gateway.
- Implement routing using Route Tables.
- Gain practical experience deploying AWS infrastructure from a YAML template.

---

## AWS Services Used

- AWS CloudFormation
- Amazon VPC
- Internet Gateway
- Route Tables
- Public Subnet
- Private Subnet

---

## Technologies Used

- AWS CloudFormation
- YAML
- AWS Management Console

---

## Resources Created

The CloudFormation template automatically provisions the following AWS resources:

- Amazon VPC
- Internet Gateway
- Internet Gateway Attachment
- Public Route Table
- Internet Route
- Public Subnet
- Private Subnet
- Route Table Association

---

## Deployment Steps

1. Sign in to the AWS Management Console.
2. Open the **AWS CloudFormation** service.
3. Select **Create Stack**.
4. Choose **With new resources (Standard)**.
5. Upload the `vpc_template.yaml` file.
6. Provide a stack name (for example, `first-vpc-stack`).
7. Configure any required stack options or tags.
8. Review the configuration.
9. Click **Submit** to begin deployment.
10. Wait until the stack status changes to **CREATE_COMPLETE**.

---

## Verification

After the deployment completed successfully, the following resources were verified:

- The VPC was created successfully.
- The Internet Gateway was attached to the VPC.
- The Public and Private Subnets were created.
- The Route Table contains:
  - `10.0.0.0/16 → Local`
  - `0.0.0.0/0 → Internet Gateway`
- The Public Subnet is associated with the Public Route Table.
- The CloudFormation stack status is **CREATE_COMPLETE**.

---

# CloudFormation Deployment

The screenshots below illustrate the complete CloudFormation deployment process, from uploading the template to successfully provisioning the infrastructure.

## Step 1 – Create the Stack

The CloudFormation template (`vpc_template.yaml`) was uploaded to begin the deployment.

![Create Stack](stack_1.png)

---

## Step 2 – Configure the Stack

The stack name and deployment settings were configured before starting the deployment.

![Configure Stack](stack_2.png)

---

## Step 3 – Deployment Completed

The deployment completed successfully with a **CREATE_COMPLETE** status, confirming that all resources defined in the template were provisioned successfully.

![Stack Created Successfully](stack_3.png)

---

# CloudFormation Resources

Once deployment was complete, CloudFormation created all the resources defined in the template.

The **Resources** tab provides information about each deployed resource, including its Logical ID, Physical ID, resource type, and deployment status.

## Resources Created

The screenshot below displays all resources created during deployment.

![CloudFormation Resources](cloudformation_resources.png)

---

## Resource Details

This view provides additional information about each deployed resource, confirming that every resource was created successfully.

![CloudFormation Resources Details](cloudformation_resources2.png)

---

# Stack Outputs

The **Outputs** section displays values exported by the CloudFormation template after deployment.

These outputs provide quick access to important resource information and can also be referenced by other CloudFormation stacks when building larger infrastructures.

![Stack Outputs](cloudformation-output.png)

---

# Resource Verification

## Amazon VPC

The Amazon Virtual Private Cloud (VPC) forms the foundation of the networking infrastructure.

It was created with the CIDR block **10.0.0.0/16**, providing a private IP address range that can be divided into multiple subnets. DNS Resolution and DNS Hostnames were enabled to support name resolution and hostname assignment within the VPC.

### VPC Overview

The screenshot below shows the VPC created by the CloudFormation template.

![Amazon VPC](cloudformation-vpc.png)

---

### VPC Details

The following screenshot confirms the VPC configuration, including its CIDR block, DNS settings, and associated resource information.

![VPC Details](cloudformation-vpc2.png)

---

## Internet Gateway

The Internet Gateway provides connectivity between the VPC and the public Internet.

It was attached to the VPC using a **VPC Gateway Attachment**, allowing resources in the Public Subnet to communicate with external networks through the configured Route Table.

### Internet Gateway Overview

The screenshot below shows the Internet Gateway created by CloudFormation.

![Internet Gateway](cloudformation-igw.png)

---

### Internet Gateway Details

The following screenshot confirms that the Internet Gateway was successfully attached to the VPC.

![Internet Gateway Details](cloudformation-igw2.png)

---

## Public Route Table

A custom Public Route Table was created to control network traffic for the Public Subnet.

It contains the routing rules that allow communication within the VPC and outbound Internet connectivity through the Internet Gateway.

### Public Route Table

The screenshot below shows the Public Route Table created by CloudFormation.
![Route Table](cloudformation-RT.png)

---

## Route Table Routes

The Route Table contains the following routes:

- **10.0.0.0/16 → Local** for communication between resources inside the VPC.
- **0.0.0.0/0 → Internet Gateway** for outbound Internet traffic.

The screenshot below shows the routing configuration.

![Public Route Table](cloudformation-PublicRT.png)


---

## Public and Private Subnets

The CloudFormation template created two subnets within the VPC:

- **Public Subnet (10.0.1.0/24)** – Intended for resources that require Internet connectivity.
- **Private Subnet (10.0.2.0/24)** – Intended for internal resources that should remain isolated from direct Internet access.

The Public Route Table was associated with the Public Subnet, enabling outbound Internet access through the Internet Gateway, while the Private Subnet remained isolated from direct Internet connectivity.
