# Install AWS, kubectl & eksctl CLI's
## _Step-00: Introduction_
- Install AWS CLI
- Install kubectl CLI
- Install eksctl CLI

## Step-01: Installing the latest version of the AWS CLI
- Reference: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### _01 - MAC - Install and configure AWS CLI_
- Download the binary and install via command line using below two commands.
```
# Download Binary
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"

# Install the binary
sudo installer -pkg ./AWSCLIV2.pkg -target /
```
- Verify the installation
```
aws --version
aws-cli/2.0.7 Python/3.7.4 Darwin/19.4.0 botocore/2.0.0dev11

which aws
```
### _02- Windows - Install and configure AWS CLI_
- The AWS CLI version 2 is supported on Windows XP or later.
- The AWS CLI version 2 supports only 64-bit versions of Windows.
- Download Binary: https://awscli.amazonaws.com/AWSCLIV2.msi
- Install the downloaded binary (standard windows install)

```
aws --version
aws-cli/2.0.8 Python/3.7.5 Windows/10 botocore/2.0.0dev12
```
### _03- Configure AWS Command Line using Security Credentials_
- Go to AWS Management Console --> Services --> IAM
- Select the IAM User: Shrikant
- Important Note: Use only IAM user to generate Security - Credentials. Never ever use Root User. (Highly not recommended)
- Click on Security credentials tab
- Click on Create access key
- Copy Access ID and Secret access key
- Go to command line and provide the required details
```
aws configure
AWS Access Key ID [None]: ABCDEFGHIAZBERTUCNGG  (Replace your creds when prompted)
AWS Secret Access Key [None]: uMe7fumK1IdDB094q2sGFhM5Bqt3HQRw3IHZzBDTm  (Replace your creds when prompted)
Default region name [None]: us-east-1
Default output format [None]: json
```
- Test if AWS CLI is working after configuring the above
```
aws ec2 describe-vpcs
```
## Step-02: Install kubectl CLI
#### IMPORTANT NOTE:
Kubectl binaries for EKS please prefer to use from Amazon (Amazon EKS-vended kubectl binary)
- This will help us to get the exact Kubectl client version based on our EKS Cluster version. You can use the below documentation link to download the binary.
- Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html
### 01: MAC - Install and configure kubectl
- Kubectl version we are using here is 1.31 (It may vary based on Cluster version you are planning use in AWS EKS)
```
# Download the Package
mkdir kubectlinstallbinary
cd kubectlinstallbinary
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.31.2/2024-11-15/bin/darwin/amd64/kubectl

# Provide execute permissions
chmod +x ./kubectl

# Set the Path by copying to user Home Directory
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bash_profile

# Verify the kubectl version
kubectl version --short --client
Output: Client Version: v1.16.8-eks-e16311
```
### Step-02: Windows 10 - Install and configure kubectl
- Install kubectl on Windows 11
```
mkdir kubectlinstallbinary
cd kubectlinstallbinary
curl.exe -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.31.2/2024-11-15/bin/windows/amd64/kubectl.exe
```
- Update the system Path environment variable
C:\Users\haris\kubectlinstallbinary
- Verify the kubectl client version
```
kubectl version --client
```
## Step-03: Install eksctl CLI
### Step-01: eksctl on Mac
```
# Install Homebrew on MacOs
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

# Install the Weaveworks Homebrew tap.
brew tap weaveworks/tap

# Install the Weaveworks Homebrew tap.
brew install weaveworks/tap/eksctl

# Verify eksctl version
eksctl version
```
## Step-02: eksctl on windows or linux
### Step-01 Open CMD as administrator
- Run the below command to install Chocolatey
```
# Install Chocolatey by executing this command

@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

```
- verify by running below command
```
choco
```
Chocolatey v2.4.1
### Step-02 Install eksctl
```
choco install eksctl
```
- Check the version
```
eksctl version
```
0.197.0
