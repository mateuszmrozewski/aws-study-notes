# EC2


### Dedicated Hosts and Dedicates Instanecs

An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use.

Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at the hardware level. In addition, Dedicated Instances that belong to AWS accounts that are linked to a single payer account are also physically isolated at the hardware level. However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.

Instance can have one of the following tenancies:
* default - shared hardware
* dedicated - single-tentant hardware
* host - instance runs on a dedicated host