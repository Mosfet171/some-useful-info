# Infrastructure as Code

## 🧱 What is IaC?

Infrastructure as Code (IaC) is the practice of defining and managing your infrastructure (servers, networks, DBs, etc.) using code, rather than clicking around in a cloud provider’s UI.

You write code to spin up, change, and destroy cloud resources — just like writing app code.

## 💡 Why use IaC?

- ✅ Version control – Your infrastructure lives in Git (just like your code)
- ✅ Repeatability – Set it up the same way every time
- ✅ Automation – No more manual mistakes
- ✅ Collaboration – Work as a team, review infra changes in pull requests

## 🛠️ Common IaC Tools

Tool	| Use case	| Notes
--------| --------- | ------
Terraform	| Cloud-agnostic infra provisioning	| Very popular + declarative
Pulumi	| Infra as code using real languages	| Supports Python, TS, Go, etc.
Ansible	| Config management (less for infra)	| No agents, easy YAML syntax
CloudFormation	| AWS-native IaC	| Deep AWS integration
Chef/Puppet	| Older config management tools	| Agent-based

## ✍️ Example (Terraform)

Here’s how to create an AWS EC2 instance using Terraform:

```hcl
provider "aws" {
  region = "us-east-1"
}
```

```hcl 
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
}
``` 

Then you’d run:

``` 
terraform init     # Set up project
terraform apply    # Create the infrastructure
terraform destroy  # Tear it down
``` 
That’s it — the infra is now code.

## 🧠 Key Concepts

1. Declarative vs Imperative
	- Declarative (like Terraform): “I want X to exist” → Tool figures out how.
	- Imperative (like bash scripts): “Do step 1, then 2, then 3.”
2. Idempotent
	- Run it once or ten times — result is the same. No duplicates.
3. State Management
	- Tools like Terraform keep a state file to track what exists.
4. Modules
	- Reusable blocks of IaC code (e.g., a module for creating a VPC)

## ☁️ What can you manage with IaC?

- Servers (EC2, Droplets, VMs)
- Databases (RDS, CloudSQL, etc.)
- Networks (VPCs, subnets, firewalls)
- Load balancers, DNS, storage, containers
- Kubernetes clusters
Basically, everything you’d normally configure in the cloud console.

## 🔄 DevOps + IaC = ❤️

IaC fits perfectly into your DevOps CI/CD pipelines:

- Infra gets created/updated alongside code deployments
- You can preview changes (like Terraform's plan)
- You can roll back infra changes like you roll back code


## 🏁 TL;DR

IaC = using code to manage infrastructure.
It’s fast, repeatable, version-controlled, and essential for modern DevOps.

