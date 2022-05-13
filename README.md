# Terraform on AWS CloudShell


## 1. Launch AWS CloudShell

1.1 Sign in to AWS Management Console

1.2 Choose the AWS CloudShell icon on the navigation bar

1.3 Check AWS Command Line Interface (AWS CLI) version

```console
aws --version
```


## 2. Install Terraform

2.1 Download Terraform Linux binary zip file

```console
wget https://releases.hashicorp.com/terraform/1.1.9/terraform_1.1.9_linux_amd64.zip
```

2.2 Unzip binary file and remove zip file

```console
unzip terraform_1.1.9_linux_amd64.zip
rm terraform_1.1.9_linux_amd64.zip
```

2.3 Make binary directory and move binary file

```console
mkdir ~/bin
mv terraform ~/bin
```

2.4 Check Terraform version

```console
terraform version
```
