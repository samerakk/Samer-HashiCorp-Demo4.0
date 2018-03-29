# Nomad and Consul Separate Clusters Example

This folder shows an example of how to use Packer to build a Nomad and Consul AMI and use Terraform code to deploy a [Nomad](https://www.nomadproject.io/) cluster that connects 
to a separate [Consul](https://www.consul.io/) cluster in [AWS](https://aws.amazon.com/) (if you want to run Nomad and 
Consul in the same clusters, see the [nomad-consul-colocated-cluster example](https://github.com/hashicorp/terraform-aws-nomad/tree/master/MAIN.md) 
instead). The Nomad cluster consists of two Auto Scaling Groups (ASGs): one with a small number of Nomad server 
nodes, which are responsible for being part of the [concensus 
quorum](https://www.nomadproject.io/docs/internals/consensus.html), and one with a larger number of Nomad client nodes, 
which are used to run jobs:

![Nomad architecture](https://raw.githubusercontent.com/hashicorp/terraform-aws-nomad/master/_docs/architecture-nomad-consul-separate.png)

You will need to create an [Amazon Machine Image (AMI)](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html) 
that has Nomad and Consul installed, which you can do using the [nomad-consul-ami example](https://github.com/hashicorp/terraform-aws-nomad/tree/master/examples/nomad-consul-ami)).  

For more info on how the Nomad cluster works, check out the [nomad-cluster](https://github.com/hashicorp/terraform-aws-nomad/tree/master/modules/nomad-cluster) documentation.




## Quick start

To deploy a Nomad Cluster:

1. `git clone` this repo to your computer.
2. Follow the readme file under /nomad-consul-ami to build Nomad Consul AMI, or See the [nomad-consul-ami example](https://github.com/hashicorp/terraform-aws-nomad/tree/master/examples/nomad-consul-ami) documentation for 
   instructions. Make sure to note down the ID of the AMI.
3. Install [Terraform](https://www.terraform.io/).
4. Open `vars.tf`, set the environment variables specified at the top of the file, and fill in any other variables that
   don't have a default, including putting your AMI ID into the `ami_id` variable.
5. Run `terraform get`.
6. Run `terraform plan`.
7. If the plan looks good, run `terraform apply`.

