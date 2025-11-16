# Custom AMI Creation Guide
This document explains how to create a custom Amazon Machine Image (AMI) based on an Ubuntu EC2 instance with Nginx installed and configured. The custom AMI will be used to launch instances in your Auto Scaling Group.

# 1. Launch Base Ubuntu EC2 Instance
	1. Open the AWS Management Console → EC2 → Instances → Launch Instance.
	2. Choose an Ubuntu Server AMI (e.g., Ubuntu 20.04 LTS).
	3. Select instance type: t2.micro (or as needed).
	4. Configure security group to allow:
		○ SSH (port 22)
		○ HTTP (port 80)
		○ HTTPS (port 443)
	5. Add the user-data script (automate Nginx installation):
	6. Launch the instance.

# 2. Connect and Verify
	• SSH into your instance: ssh -i your-key.pem ubuntu@<instance-public-ip>
	• Verify Nginx is running: sudo systemctl status nginx
	• Access the instance's public IP in a browser to confirm the custom welcome page.

# 3. Prepare the Instance
	• Stop any unnecessary services.
	• Ensure the instance is stable and configured correctly.

# 4. Create Custom AMI
	1. From the EC2 Dashboard, select your instance.
	2. Click Actions → Image and templates → Create Image.
	3. Provide an Image name, e.g.: nginx-custom-ami
	4. Optionally, add a description.
	5. Click Create Image.

# 5. Monitor AMI Creation
	• Navigate to AMIs under EC2 Dashboard → Images.
	• Wait until the AMI status changes to Available.

# 6. Use Your Custom AMI
    Your new AMI can now be used to:
	• Create Launch Templates
	• Launch Auto Scaling Group instances

Custom AMI Creation Completed
You now have a reusable, pre-configured image for rapid, consistent deployment of Nginx servers.
