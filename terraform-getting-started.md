# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn how to download and install Terraform.

## Prerequisites


## Download Terraform

Visit [Terraform.io](https://www.terraform.io/downloads.html) and download the appropriate package for your operating system and architecture.

Once Terraform is downloaded, create the infrastructure.

## Set-Up File Infrastructure

Create a new directory on your local machine for your Terraform configuration code and cd into it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, make a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into your `main.tf` file:

```hcl
provider "docker" {
    host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

##Install

Initialize Terraform with the `init` command. Terraform will install the AWS provider. 

```shell
$ terraform init
```

If there are no errors, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command takes up to a few minutes to run. Once the resource is provisioned, Terraform will display a message indicating success.

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it created earlier.

## Next Steps
