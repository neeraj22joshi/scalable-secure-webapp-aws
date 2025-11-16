# Auto Scaling Group (ASG) Setup Guide
This document provides a complete, step-by-step procedure for configuring an Auto Scaling Group (ASG) on AWS using a custom Nginx AMI and a Launch Template.
This ASG ensures high availability, fault tolerance, and automatic scaling based on CPU utilization.

# 1. Prerequisites
Before creating the ASG, ensure you have:
	• A custom AMI that includes Nginx (created earlier)
	• A Launch Template configured using that AMI
	• A VPC with at least two public subnets across different Availability Zones
	• A Security Group allowing:
		○ SSH (22)
		○ HTTP (80)
		○ HTTPS (443)

# 2. Create the Auto Scaling Group
  Step 2.1 — Navigate to Auto Scaling Groups
	1. Go to the AWS Management Console
	2. Open EC2 → Left sidebar → Auto Scaling Groups
	3. Click Create Auto Scaling group

# 3. Configure Basic Settings
  Step 3.1 — Provide ASG Name
  Example: nginx-asg

  Step 3.2 — Select Launch Template
  Choose the Launch Template you created earlier: nginx-lt
  This template should reference your custom Nginx AMI.

# 4. Configure Network Settings
  Step 4.1 — Select VPC and Subnets
	• Choose default VPC or your project VPC
	• Select all available subnets across multiple AZs
  This ensures high availability across zones.

# 5. Attach Load Balancer
  Step 5.1 — Choose Load Balancing Options
  Select: Attach to a new load balancer

  Step 5.2 — ALB Configuration
	• Load Balancer Type: Application Load Balancer
	• Scheme: Internet-facing
	• Listener: HTTP (Port 80)

  Step 5.3 — Target Group
  Create a new Target Group: nginx-target-group
  Health Check Settings:
	• Protocol: HTTP
	• Path: /
	• Health Check Grace Period: 300 seconds

# 6. Configure Group Size and Scaling Policy
  Step 6.1 — Set Capacity
  Desired: 2
  Minimum: 1
  Maximum: 4

  Step 6.2 — Add Scaling Policy
  Choose Target Tracking Scaling Policy:
	• Metric: Average CPU Utilization
	• Target Value: 20%
	• Instance Warmup Time: 60 seconds
  This policy ensures the ASG adds or removes EC2 instances based on real-time load.

# 7. Add Notifications (Optional)
  You may configure SNS notifications for:
	• Instance launches
	• Instance terminations
	• Scaling activity

# 8. Add Tags
  Add project-related tags such as:
  Key	Value
  Name	nginx-asg-instance
  Project	Auto-Scalable-Nginx
  Tags help with resource tracking and cost allocation.

# 9. Review and Create
  Review all settings and select:

  Create Auto Scaling group
  AWS will immediately launch the number of instances defined in your desired capacity.

# 10. Verification
	• Go to EC2 → Instances
	• Verify that multiple EC2 instances have been created
	• Check Load Balancers → Target Groups to confirm:
		○ Instances are healthy
		○ ALB is routing traffic correctly
  You can also access the ALB DNS name in a browser to verify the Nginx homepage.

# ASG Setup Completed
  Your environment is now capable of:
	• Handling traffic spikes
	• Scaling automatically
	• Maintaining availability across AZs
