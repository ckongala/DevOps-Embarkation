```
Objective:
	Intro IaC:
	Types of Iac:
	Why Terraform:
	HCL Basics:
	Provision update and Destroy:
	Providers:
	Input Variables:
	Output Variables:
	Resource Attributes:
	Resource Dependencies:
	Terraform State:
	Commands:
	Mutable Vs Immutable:
	Lifecycle Rules:
	Datasources:
	Meta-arguments:
	count:
	for-each:
	version constraints:
	AWS Basics
		Programmatic Access, IAM, ec2, S3, DynamoDB
	
	Remote State:
	State Locking:
	Remote Backend with s3:
	State Commands
	Provisioners
	
	Terraform Taints:
	Debugging
	Terraform import
	Modules
	Functions
	Conditional Expression
	Workspaces
	Terraform cloud
	
====
::Tradational Infra Model::
Business(Req for app) >> 
Busibess Analyst(Gather needsa and analyze it, convert into high level technical req) >>  
Solution Architect/Technical Lead(desigh architrct for the deploy of app, include type spec and count of server) >> 
Infrastructure Team
	Field Engineers(rack and stack of equipment),
	System/NW Admins(perform initial config)(make system avaliable on the network),
	Storage Admins(asssign storage tot he servers), 
	Backup Admins(Backup), 
	Application Team(To deploy the app in those servers)
Drawback:
Time, Human error, not easy to sclae up down, cost high, inconsist in env, wasted resource,

Now Infra is taking care of Cloud(AWS, AZURE, GCP)
only two drawbacks Human Error, Inconsisty
to slove this use different approach; >> shell, Python, ruby, perl, powershell
====
:::IaC:::
Brodly divide into 3 types:
1. Configuration Managment : Ansible, Puppet, SALTSTACK,
	Design to install and manage software
	maintains standard structure
	version control
	idempotent
2. Server Templating: Docker Hashicorp Packer, Hashicorp Vagrant
	used to create a custom image of a VM or a container
	preinstalled software and dependencies
	immutable infrastructure
3. Provisioning Tools: Hashicorp Terraform, Cloudformation
	Deploy immutable infra resource 
	servers, databases, network comp tec..,
	multiple providers
====
Why Terraform??
	simple declarative lang(The code we define want to be infra struct in)(currrent state)
		
		
	support multiple cloud providers (include on-premis vSphere cluster), 
	Free open source, 
	install as single binary, setup very fast, execution(build, manage, destroy)infra also very fast
	
Works:
	Declarative >> take care of what is req, to go from current state to the desired state.
	3 phases: init, plan, apply;
	init  ==> initilize the project and identify the providers to be used for target env.
	plan ==> draft the plan to the target stage.
	apply ==> make necessary changes req on the target env to bring ot to desired state.
		(if some reason env shift from the desired state then a sebsequent terraform apply will bring back to desired state. by only fixing the missing comp)
resourece, 
lifecycle

statefile is a blue print
	mappinf congif to real world, tracking of metadata, performance, collaboration
====
conf Dir:
	statefiles;
	data from configuration files(use to provision and manage infra);
	main.tf, variables.tf, outputs.tf, provider.tf
	
best way: Statefile(Single source of truth) keep it in remote!! 
	Non-optional feature in terraform
====
if you do any changes in files(Infra) and run terraform apply, firstly it will delete old and create a new one
Reason:-
	It follows 'immutable'
what if you want to chage those steps, 
"Lifecycle Rules": comes into the picture,
	create first and then delete ==> lifecycle { create_before_destroy = true}
	create only no delete ==> lifecycle {prevent_destroy = true }
	ignore changes ==> lifecycle{ ignore_changes = all or [ tags,... ] }
<terraform destory will destory, it dosent prevent destroy>
====
Data Sources:
	allow terraform to read attribute from resources which are provision outside its control,
	syntax:- data "XX" "XX" { ... } simply instead of 'resource' use 'data'
A data source once created, can be used to create, update, and destroy infrastructure ==> False
===
Meta-arguments in terraform:
	used within any resource block to change behaviour of resources,
	ex:- depends_on, lifecycle, count, length, for_each, toset(),
===
Remote state
if youn run terraform apply at same time in 2 different(State lock) 
once done by one goes to next
not good to store in github (contains sensitive data, what if forget to push/pull latest, only one person has to update(not support Statelock))
so we use remote backend (S3, DynamoDB)
	Automatically load and upload state file, 
	may backends supports state locking
	security
s3 bucket & dynamoDb table to configure a remote backend for terraform config
S3 ==> to store Terraform state, 
DynamoDB ==> State Locking & consisty checks.
=====

Provisiioners









:::CMD:::
Terraform follows an immutable infrastructure approach, the file was recreated although the contents are the same.
terrafrom init ==>
terraform plan ==> 
terraform apply ==> 
terraform show -json ==>
terraform output/ terraform output <name/arg> ==>
terraform plan --refresh=false
terraform apply -refresh-only
terraform validate ==>
terraform fmt ==> 
terraform providers ==> 
terraform providers mirror <path> ==>
terraform graph | dot -Tsvg > graph.svg

State Commands:
terraform state <subcmd> [options] [args]
subcmd: list, mv, pull, rm, show

```
