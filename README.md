# Terraform on AWS CloudShell


## 1. Launch AWS CloudShell

1. Sign in to AWS Management Console <img src="https://github.com/t2yijaeho/Terraform-on-AWS-CloudShell/blob/main/images/AWS%20Management%20Console.png?raw=true" width="16">

2. Choose the AWS CloudShell icon <img src="https://github.com/t2yijaeho/Terraform-on-AWS-CloudShell/blob/main/images/AWS%20CloudShell.png?raw=true" width="16"> on the navigation bar

    ***[Supported AWS Regions for AWS CloudShell](https://docs.aws.amazon.com/general/latest/gr/cloudshell.html)***

3. Check AWS Command Line Interface (AWS CLI) version

    ```bash
    aws --version
    ```

    <img src="https://github.com/t2yijaeho/Terraform-on-AWS-CloudShell/blob/main/images/AWS%20CloudShell%20version.png?raw=true">


## 2. Install Terraform

1. Get latest Terraform version

    ```console
    LATEST_RELEASE=$(curl https://api.github.com/repos/hashicorp/terraform/releases/latest | jq --raw-output '.tag_name' | cut -c 2-)
    echo $LATEST_RELEASE
    ```

2. Download Terraform Linux binary zip file

    ```console
    wget https://releases.hashicorp.com/terraform/${LATEST_RELEASE}/terraform_${LATEST_RELEASE}_linux_amd64.zip
    ```

3. Unzip binary file and remove zip file

    ```console
    unzip -d ./bin/ terraform_${LATEST_RELEASE}_linux_amd64.zip
    rm terraform_${LATEST_RELEASE}_linux_amd64.zip
    ```

4. Check Terraform version

    ```console
    terraform version
    ```
