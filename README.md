# Terraform on AWS CloudShell


## 1. Launch AWS CloudShell

Refer to [***AWS CloudShell***](https://github.com/t2yijaeho/AWS-CloudShell)


## 2. Install Terraform

1. Get latest Terraform version

    ```console
    LATEST_RELEASE=$(curl https://api.github.com/repos/hashicorp/terraform/releases/latest | jq --raw-output '.tag_name' | cut -c 2-)
    echo $LATEST_RELEASE
    ```
    
    ```console
    [cloudshell-user@ip-10-0-123-234 ~]$ LATEST_RELEASE=$(curl https://api.github.com/repos/hashicorp/terraform/releases/latest | jq --raw-output '.tag_name' | cut -c 2-)
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100  3027  100  3027    0     0  15891      0 --:--:-- --:--:-- --:--:-- 15931
    [cloudshell-user@ip-10-0-123-234 ~]$ echo $LATEST_RELEASE
    1.2.4
    [cloudshell-user@ip-10-0-123-234 ~]$ 
    ```

2. Download Terraform Linux binary zip file

    ```console
    wget https://releases.hashicorp.com/terraform/${LATEST_RELEASE}/terraform_${LATEST_RELEASE}_linux_amd64.zip
    ```
    
    ```console
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
    

3. Unzip binary file and remove zip file

    ```console
    unzip -d ./bin/ terraform_${LATEST_RELEASE}_linux_amd64.zip
    rm terraform_${LATEST_RELEASE}_linux_amd64.zip
    ```
    
    ```console
    [cloudshell-user@ip-10-0-123-234 ~]$ unzip -d ./bin/ terraform_${LATEST_RELEASE}_linux_amd64.zip
    Archive:  terraform_1.2.4_linux_amd64.zip
      inflating: ./bin/terraform         
    [cloudshell-user@ip-10-0-123-234 ~]$ rm terraform_${LATEST_RELEASE}_linux_amd64.zip
    [cloudshell-user@ip-10-0-123-234 ~]$ 
    ```


4. Check Terraform version

    ```console
    terraform version
    ```
    
    ```console
    [cloudshell-user@ip-10-0-123-234 ~]$ terraform version
    Terraform v1.2.4
    on linux_amd64
    [cloudshell-user@ip-10-0-123-234 ~]$ 
    ```
