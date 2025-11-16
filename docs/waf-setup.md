# AWS WAF (Web Application Firewall) Setup Guide
This document explains how to create and configure AWS WAF to protect your Application Load Balancer (ALB) from common web threats and bots.

# 1. Create a Web ACL
	1. Open AWS Management Console → WAF & Shield.
	2. Click Create Web ACL.
	3. Configure:
		○ Name: nginx-web-acl
		○ Region: Select the same AWS region as your ALB.
		○ Resource type: Application Load Balancer

# 2. Add AWS Resources
	• Associate the Web ACL with your Application Load Balancer:
		○ Select your ALB (nginx-alb) from the list.

# 3. Configure Rules
Step 3.1 — Add Managed Rule Groups
	• Click Add Managed Rule Groups.
	• Choose AWS Managed Rules:
		○ Select Bot Control Managed Rule Group (to block automated bots).
		○ Add any other managed rule groups if needed for OWASP protections.
Step 3.2 — Define Rule Action
	• For requests that don’t match any rules, set default action to:
		○ Allow

# 4. Set Scope of Inspection
	• Choose:
		○ Inspect all web requests

# 5. Review and Create
	• Review the Web ACL configuration.
	• Click Create Web ACL.

# 6. Verification
	• Your ALB is now protected by the AWS WAF Web ACL.
	• Test by sending traffic to your website and monitor blocked requests in the WAF console.

# AWS WAF Setup Completed
You have successfully added an additional layer of security that protects your auto-scaled Nginx environment from common web exploits and malicious bots.
