Example project to deploy an AWS ECS cluster using terraform.

I created this project as an exercise to familiarize myself with AWS Fargate and terraform.

## Description

The scripts will create a new VPC and deploy a configurable number of (jwilder's whoami)[https://github.com/jwilder/whoami] service in multiple availability zones.
The service simply prints the container ID when accessed via HTTP which makes it easy to verify the origin of a response when using a load balancer.
The containers run in an ECS cluster using Fargate.
For each availability zone we create a private subnet in which the ECS task can run, and a public subnet containing a NAT gateway for internet access.
Additionally, an application load balancer is created and redirects traffic to the container instances.


## Usage

To use this project, you need a valid AWS credentials and have terraform installed.

After cloning this repository, initialize terraform by running:

```tarraform init```

To deploy your infrastructure, run:

```terraform apply -var 'access_key=REPLACE_THIS' -var 'secret_key=REPLACE_THIS'```

To remove everything run:

```terraform destroy -var 'access_key=REPLACE_THIS' -var 'secret_key=REPLACE_THIS'```


The ```terraform apply``` command will print the public DNS name of the load balancer. You can paste this URL into your browser and see different containers responding on every refresh. Note: wait for 1-2min after deploying for all services and containers to start and connect to the load balancer.

Modify ```variables.tf``` to configure your deployment.