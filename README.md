# Terraform on AWS CloudShell


## 1. Launch AWS CloudShell

Refer to [***AWS CloudShell***](https://github.com/t2yijaeho/AWS-CloudShell)


## 2. Install Terraform

### 1. Get latest Terraform version

```sh
LATEST_RELEASE=$(curl https://api.github.com/repos/hashicorp/terraform/releases/latest | jq --raw-output '.tag_name' | cut -c 2-)
echo $LATEST_RELEASE
```
    
```sh
[cloudshell-user@ip-10-0-123-234 ~]$ LATEST_RELEASE=$(curl https://api.github.com/repos/hashicorp/terraform/releases/latest | jq --raw-output '.tag_name' | cut -c 2-)
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                    Dload  Upload   Total   Spent    Left  Speed
100  3027  100  3027    0     0  15891      0 --:--:-- --:--:-- --:--:-- 15931
[cloudshell-user@ip-10-0-123-234 ~]$ echo $LATEST_RELEASE
1.2.4
[cloudshell-user@ip-10-0-123-234 ~]$ 
```

### 2. Download Terraform Linux binary zip file

```sh
wget https://releases.hashicorp.com/terraform/${LATEST_RELEASE}/terraform_${LATEST_RELEASE}_linux_amd64.zip
```
    
```sh
[cloudshell-user@ip-10-0-123-234 ~]$ wget https://releases.hashicorp.com/terraform/${LATEST_RELEASE}/terraform_${LATEST_RELEASE}_linux_amd64.zip
--2022-07-06 07:28:33--  https://releases.hashicorp.com/terraform/1.2.4/terraform_1.2.4_linux_amd64.zip
Resolving releases.hashicorp.com (releases.hashicorp.com)... 151.101.54.49
Connecting to releases.hashicorp.com (releases.hashicorp.com)|151.101.54.49|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 19895510 (19M) [application/zip]
Saving to: ‘terraform_1.2.4_linux_amd64.zip’

100%[=============================================================================================>] 19,895,510  --.-K/s   in 0.08s   

2022-07-06 07:28:33 (234 MB/s) - ‘terraform_1.2.4_linux_amd64.zip’ saved [19895510/19895510]

[cloudshell-user@ip-10-0-123-234 ~]$ 
```
    

### 3. Unzip binary file and remove zip file

```sh
unzip -d ./bin/ terraform_${LATEST_RELEASE}_linux_amd64.zip
rm terraform_${LATEST_RELEASE}_linux_amd64.zip
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ unzip -d ./bin/ terraform_${LATEST_RELEASE}_linux_amd64.zip
Archive:  terraform_1.2.4_linux_amd64.zip
    inflating: ./bin/terraform         
[cloudshell-user@ip-10-0-123-234 ~]$ rm terraform_${LATEST_RELEASE}_linux_amd64.zip
[cloudshell-user@ip-10-0-123-234 ~]$ 
```

### 4. Check Terraform version

```sh
terraform version
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ terraform version
Terraform v1.2.4
on linux_amd64
[cloudshell-user@ip-10-0-123-234 ~]$ 
```

## 3. Apply Terraform

### 1. Create Configuration File

```text
cat <<EOF >aws.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
    }
  }
}

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}

# Create a VPC
resource "aws_vpc" "aws" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "aws"
  }
}
EOF
```

### 2. Initialize Provider Plugin

```sh
terraform init
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/aws...
- Installing hashicorp/aws v5.9.0...
- Installed hashicorp/aws v5.9.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
[cloudshell-user@ip-10-0-123-234 ~]$ 
```

### 3. Create Resources

```sh
terraform apply -auto-approve
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated
with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_vpc.aws will be created
  + resource "aws_vpc" "aws" {
      + arn                                  = (known after apply)
      + cidr_block                           = "10.0.0.0/16"
      + default_network_acl_id               = (known after apply)
      + default_route_table_id               = (known after apply)
      + default_security_group_id            = (known after apply)
      + dhcp_options_id                      = (known after apply)
      + enable_dns_hostnames                 = (known after apply)
      + enable_dns_support                   = true
      + enable_network_address_usage_metrics = (known after apply)
      + id                                   = (known after apply)
      + instance_tenancy                     = "default"
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      + main_route_table_id                  = (known after apply)
      + owner_id                             = (known after apply)
      + tags                                 = {
          + "Name" = "aws"
        }
      + tags_all                             = {
          + "Name" = "aws"
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
aws_vpc.aws: Creating...
aws_vpc.aws: Creation complete after 1s [id=vpc-0428798344e78e9e0]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

### 4. Describe Resources

```sh
aws ec2 describe-vpcs --filters "Name=tag:Name,Values=aws*"
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ aws ec2 describe-vpcs --filters "Name=tag:Name,Values=aws*"
{
    "Vpcs": [
        {
            "CidrBlock": "10.0.0.0/16",
            "DhcpOptionsId": "dopt-04e20fc537599e464",
            "State": "available",
            "VpcId": "vpc-0428798344e78e9e0",
            "OwnerId": "123456789012",
            "InstanceTenancy": "default",
            "CidrBlockAssociationSet": [
                {
                    "AssociationId": "vpc-cidr-assoc-058fb6235853d46bc",
                    "CidrBlock": "10.0.0.0/16",
                    "CidrBlockState": {
                        "State": "associated"
                    }
                }
            ],
            "IsDefault": false,
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "aws"
                }
            ]
        }
    ]
}
```

### 5. Delete Resources

```sh
terraform apply -destroy -auto-approve
```

```sh
[cloudshell-user@ip-10-0-123-234 ~]$ terraform apply -destroy -auto-approve
aws_vpc.aws: Refreshing state... [id=vpc-0428798344e78e9e0]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # aws_vpc.aws will be destroyed
  - resource "aws_vpc" "aws" {
      - arn                                  = "arn:aws:ec2:us-east-1:123456789012:vpc/vpc-0428798344e78e9e0" -> null
      - assign_generated_ipv6_cidr_block     = false -> null
      - cidr_block                           = "10.0.0.0/16" -> null
      - default_network_acl_id               = "acl-09ec77f3b32c6c7c7" -> null
      - default_route_table_id               = "rtb-004ba222a277f79f0" -> null
      - default_security_group_id            = "sg-07a7f1661195658a0" -> null
      - dhcp_options_id                      = "dopt-04e20fc537599e464" -> null
      - enable_dns_hostnames                 = false -> null
      - enable_dns_support                   = true -> null
      - enable_network_address_usage_metrics = false -> null
      - id                                   = "vpc-0428798344e78e9e0" -> null
      - instance_tenancy                     = "default" -> null
      - ipv6_netmask_length                  = 0 -> null
      - main_route_table_id                  = "rtb-004ba222a277f79f0" -> null
      - owner_id                             = "123456789012" -> null
      - tags                                 = {
          - "Name" = "aws"
        } -> null
      - tags_all                             = {
          - "Name" = "aws"
        } -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.
aws_vpc.aws: Destroying... [id=vpc-0428798344e78e9e0]
aws_vpc.aws: Destruction complete after 1s

Apply complete! Resources: 0 added, 0 changed, 1 destroyed.
```
