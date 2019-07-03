# AWS Managed Microsoft AD and Amazon FSx for Windows File Server

Log into the AWS Management Console and choose the [N. Virginia Region](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html).

## 1. Create a new Key Pair

You will need to get into your Windows instance, using the private key you will obtain the Administrator password and then login using RDP.

1.1\. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2.

1.2\. Click on **Key Pairs** in the **NETWORK & SECURITY** section. This will display a page to manage your key pairs.

![Key Pairs menu](images/ec2-key-pairs-menu.png)

1.3\. To create a new key pair, click the **Create Key Pair** button.

![Create Key Pair](images/ec2-create-key-pair.png)

1.4\. In the resulting pop up window, for **Key Pair Name** type `my-keypair` and click **Create**.

![Key Pair Name](images/ec2-key-pair-name.png)

1.5\. The private key file is automatically downloaded by your browser. The base file name is the name you specified as the name of your key pair, and the file name extension is .pem. Save the private key file in a safe place.

## 2. Create the AWS Managed Microsoft AD and Amazon FSx for Windows File Server using CloudFormation

2.1\. Download the [CloudFormation template AURBAC-MicrosoftAD-And-FSx.json](scripts/AURBAC-MicrosoftAD-And-FSx.json), we are going to use it to create the environment and services required.

2.2\. Open the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation.
  
2.3\. In **Stacks** section choose **Create Stack**.

![Create Stack](images/cloudformation-create-stack.png)

2.4\. In the **Create stack** section, select **Template is ready**, select **Upload a template file** and **Choose file** for the template downloaded **AURBAC-MicrosoftAD-And-FSx.json** and click **Next**.

![Create Stack Select file](images/cloudformation-create-stack-file.png)

2.5\. In the **Specify stack details** section, for **Stack name** type `MicrosoftAD-And-FSx` to identify the cloudformation stack.

![Stack name](images/cloudformation-stack-name.png)

2.6\. For **KeyName** select your key pair created previously.

![Key Pair](images/cloudformation-key-pair.png)

2.7 Review the default values, just remember that the **Password** for your Active Directory will be **`MicrosoftADPW123*`** as default, you can change it if you want, scroll down and click **Next**.

2.8\. For the **Configure stack options** section choose **Next**.

2.9\. For the **Review MicrosoftAD-And-FSx** section, check the box for **I acknowledge that AWS CloudFormation might create IAM resources with custom names.** and click **Create Stack**.

![Review](images/cloudformation-review.png)

2.10\. It will take about 45 minutes while your stack is being created, it is listed on the **Stacks** page with a status of **CREATE_IN_PROGRESS**.

2.11\. After your stack has been successfully created, its status changes to **CREATE_COMPLETE**. You can then click the **Outputs** tab to view your stack's outputs required for the following configurations.

![Cloudformation Complete](images/cloudformation-create-complete.png)

### AWS Services created

* One Amazon VPC environment with two public and two private subnets.
* One Microsoft AD Standard.
* One EC2 instance with Windows 2016 (t3.medium).
* One Amazon FSx for Windows File Server

![AWS Services](images/microsoftad-and-fsx.png)

## 3. Create a new Key Pair