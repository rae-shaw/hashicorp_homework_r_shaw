# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). In this guide, you'll learn how to download and install Terraform, in addtion to some of the basic Terraform commands.

## Prerequisites

System requirements:

Mac Os X:
* Requirement 1
* Requirement 2

Linux
* Requirement 1
* Requirement 2

Windows
* Requirement 1
* Requirement 2

## Download Terraform

Visit [Terraform.io](https://www.terraform.io/downloads.html) and download the appropriate package for your operating system and architecture.

Once Terraform is downloaded, unzip the file and move it to a directory included in your system's PATH. Verify that the installation was successful by typing the command `terraform` into a new terminal window. The output should look like the below block:

``` 
The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.

Common commands:
    apply              Builds or changes infrastructure
    console            Interactive console for Terraform interpolations
    destroy            Destroy Terraform-managed infrastructure
    env                Workspace management
    fmt                Rewrites config files to canonical format
    get                Download and install modules for the configuration
    graph              Create a visual graph of Terraform resources
    import             Import existing infrastructure into Terraform
    init               Initialize a Terraform working directory
    login              Obtain and save credentials for a remote host
    logout             Remove locally-stored credentials for a remote host
    output             Read an output from a state file
    plan               Generate and show an execution plan
    providers          Prints a tree of the providers used in the configuration
    refresh            Update local state file against real resources
    show               Inspect Terraform state or plan
    taint              Manually mark a resource for recreation
    untaint            Manually unmark a resource as tainted
    validate           Validates the Terraform files
    version            Prints the Terraform version
    workspace          Workspace management

All other commands:
    0.12upgrade        Rewrites pre-0.12 module source code for v0.12
    debug              Debug output management (experimental)
    force-unlock       Manually unlock the terraform state
    push               Obsolete command for Terraform Enterprise legacy (v1)
    state              Advanced state management
logout
Saving session...
...copying shared history...
...saving history...truncating history files...
...completed.
Deleting expired sessions...3 completed.

[Process completed]
```


## Build the Infrastructure

Now that Terraform is installed, you can dive right into creating creating infrastructure. 

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
Doublecheck your `main.tf` file.

```shell
$ cat main.tf
```
The output in your terminal should match the above lines.


## Initialization

Initialize Terraform with the `init` command. Terraform will install the AWS provider. 

```shell
$ terraform init
```
You should receive the following output:

```hcl
Initializing the backend...
 
Initializing provider plugins...
- Checking for available provider plugins...
- Downloading plugin for provider "docker" (terraform-providers/docker) 2.7.0...
 
The following providers do not have any version constraints in configuration,
so the latest version was installed.
 
To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.
 
* provider.docker: version = "~> 2.7"
 
Terraform has been successfully initialized!
 
You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.
 
If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```
If you receive any errors, doublecheck your `main.tf` file for any punctuation or syntax errors. If you still receive errors, check out the FAQ and resources:

* [Terraform FAQ](faketerraformfaq.ed)
* [Resource 1](faketerraformresource1.ed)
* [Resource 2](faketerraformresource2.ed)

## Provision

Now you can provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command takes up to a few minutes to run. Once the resource is provisioned, Terraform will display a message indicating success.

```hcl
SUCCESS MESSAGE HERE

See note in email about this output.
```

## Destroy Infrastructure

You've learned how to install, initialize, and provision Terraform and your infrastructure. Before moving on to more complex topics, we'll go over how to destroy the infrastructure.

Type `destroy` to terminate the resources previously defined.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation: 

```shell
Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.
 
  Enter a value: 
```

Type `yes` and hit ENTER. Terraform will destroy the resources it created earlier.

## Next Steps

At this point, you downloaded Terraform and completed the initialization and installation. Return this guide to review the steps and basic commands as needed.

To continue learning more intermediate and advanced topics, check out the following guides and resources:
1. Guide 1
2. Guide 2

1. Resource 1
2. Resource 2
