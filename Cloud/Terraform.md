
# what is terraform

Terraform is an infrastructure as code tool that lets you build, and automate infrastructure efficiently. 

Terraform uses APIs provided by the cloud providers to make this automate and managing resources. 

# Stages

Terraform workflow has three stages:

1) Write: You define resources which maybe across multiple cloud providers and services.
2) Plan: Terraform creates an execution plan describing the infrastructure it will create, update or destroy based on existing infra and configuration
3) Apply: Finally apply all the configuration and creating resources.

# How does terraform work?

## components

Terraform has two main components. 

1) core
2) Providers

1) Core needs two input sources: configuration and current state. You provide configuration file with your desired state of the infra and also provide current state of the infra to the core. Based on this inputs, the core will determine what resources should be created/destroyed/updated.

2) The second component is providers. Providers are cloud or PaaS providers like k8s. They provide API which terraform uses to provision infrastructure.

# Declarative vs imperative

Terraform config files are declarative, meaning you define the end state in your config file.  You do not need write step-by-step instructions to created resources. 

Terraform compares the current state with the desired state and make all the changes to move the infra/system to the desired state, instead of giving instruction step-by-step. This makes terraform manage infra more efficiently.

# Modules

A module is essentially a directory containing Terraform configuration files (`.tf` files). It is a way to organize and reuse your infrastructure as code.

Think of a module as a blueprint that groups resources into a single reusable unit. For example:

- A module can define all the resources needed to deploy an AWS EC2 instance with a security group and an attached EBS volume.
- Another module might define a VPC with subnets, route tables, and gateways.

You can divide your whole infrastructure into logical blocks called modules and then execute them where required. It makes managing terraform configuration files easier. 

### structure

This is usually the structure of each modules
module-name/ 
├── main.tf # Main resources definition 
├── variables.tf # Input variables 
├── outputs.tf # Output variables (to display information on cli) 
├── providers.tf # (Optional) Provider configurations 
├── README.md # Documentation for the module


To use module tf file in another module we use source property and then module url.

# Terraform  commands

## Essential commands

#### Initialize
```bash
terraform init
```
Brings all the plugins (AWS, AZ, etc) required according to the providers mentioned in the configuration file.
#### Plan changes
```bash
terraform plan
```
Show all the changes that executing the config file will do to the architecture
#### Apply changes
```bash
terraform apply
```
Finally applies all the changes
#### Destroy infrastructure
```bash
terraform destroy
```

## Other commands

#### Lists all resources in the Terraform state.
```bash
terraform state list
```

#### Displays detailed information about a specific resource in the state.
```bash
terraform state show <resource_name>
```

#### Applies changes only to a specific resource
```bash
terraform apply -target=<resource>
```


