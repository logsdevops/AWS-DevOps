# Install AWS, kubectl & eksctl CLI's
## _Step-00: Introduction_
- Install AWS CLI
- Install kubectl CLI
- Install eksctl CLI

## Step-01: Installing the latest version of the AWS CLI
- Reference: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### _01- MAC - Install and configure AWS CLI_
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

