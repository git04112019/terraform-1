# Basic Two-Tier AWS Architecture 
## Installs nginx, mongodb, nodejs, bower, gulp and mean-cli

This is a fork from [Hashicorp's github repo](https://github.com/hashicorp/terraform/tree/master/examples/aws-two-tier).

I've modified this to make a few small changes from the original.  

1. I've made revisions to the AMI to Ubuntu 16.04 LTS
2. The software nginx, mongodb, nodejs, bower, gulp and mean-cli will be installed with the ability for you to build your MEAN based site right away.  

## TODO

  * Have automatic provisioned reverse proxy for nginx/nodejs
  * Rename everything to something that fits this repo
  * Make variables clearer, abtract some of it into separate tf's to organize this better.
  * Learn multiple provisioners.

This provides a template for running a simple two-tier architecture on Amazon
Web services. The premise is that you have stateless app servers running behind
an ELB serving traffic.

To simplify the example, this intentionally ignores deploying and
getting your application onto the servers. However, you could do so either via
[provisioners](https://www.terraform.io/docs/provisioners/) and a configuration
management tool, or by pre-baking configured AMIs with
[Packer](http://www.packer.io).

This example will also create a new EC2 Key Pair in the specified AWS Region. 
The key name and path to the public key must be specified via the  
terraform command vars.

After you run `terraform apply` on this configuration, it will
automatically output the DNS address of the ELB. After your instance
registers, this should respond with the default nginx web page.

To run, configure your AWS provider as described in 

https://www.terraform.io/docs/providers/aws/index.html

Run with a command like this:

```
terraform apply -var 'key_name={your_aws_key_name}' \
   -var 'public_key_path={location_of_your_key_in_your_local_machine}'` 
```

For example:

```
terraform apply -var 'key_name=terraform' -var 'public_key_path=/Users/jsmith/.ssh/terraform.pub'
```
