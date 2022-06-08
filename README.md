# Terraform on AWS CloudShell


## 1. Launch AWS CloudShell

   Refer to [***AWS CloudShell***](https://github.com/t2yijaeho/AWS-CloudShell)


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
