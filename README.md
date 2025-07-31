# 🚀 DevOps AWS EC2 Deployment Project

A complete Infrastructure as Code (IaC) project using Terraform to deploy a web server on AWS EC2 with proper networking, security, and monitoring.

## 📋 Project Overview

This project demonstrates how to:
- **Deploy infrastructure** using Terraform
- **Set up networking** with VPC, subnets, and security groups
- **Launch EC2 instances** with automated configuration
- **Implement security best practices** with proper access controls
- **Monitor and manage** your infrastructure

## 🏗️ Architecture

```
┌─────────────────┐
│   Internet      │
│                 │
└─────────┬───────┘
          │
          ▼
┌─────────────────┐
│   EC2 Instance  │
│   - Web Server  │
│   - Apache      │
│   - Auto-config │
└─────────────────┘
```

## 📁 Project Structure

```
terraform-aws-webserver/
├── main.tf              # Main Terraform configuration
├── variables.tf          # Input variables
├── outputs.tf           # Output values
├── versions.tf          # Provider versions
├── .gitignore          # Git ignore rules
└── README.md           # This file
```

## 🛠️ Prerequisites

Before you begin, ensure you have:

- [Terraform](https://www.terraform.io/downloads.html) (>= 1.0)
- [AWS CLI](https://aws.amazon.com/cli/) configured
- AWS account with appropriate permissions
- Git

## 🚀 Quick Start

### Step 1: Clone the Repository

```bash
git clone https://github.com/TshegoR24/terraform-aws-webserver.git
cd terraform-aws-webserver
```

### Step 2: Configure AWS Credentials

```bash
aws configure
```

Enter your:
- AWS Access Key ID
- AWS Secret Access Key
- Default region (e.g., us-west-2)
- Default output format (json)

### Step 3: Create EC2 Key Pair

Create a key pair in AWS Console or via AWS CLI:

```bash
aws ec2 create-key-pair --key-name webserver-key --query 'KeyMaterial' --output text > webserver-key.pem
chmod 400 webserver-key.pem
```

### Step 4: Initialize Terraform

```bash
terraform init
```

### Step 5: Review the Plan

```bash
terraform plan
```

### Step 6: Deploy Infrastructure

```bash
terraform apply
```

When prompted, type `yes` to confirm.

## 🌐 Access Your Application

After successful deployment, you'll see output similar to:

```
Outputs:

instance_public_ip = "54.xxx.xxx.xxx"
website_url = "http://54.xxx.xxx.xxx"
```

Visit the website URL in your browser to see your deployed web server!

## 🔧 Configuration

### Variables

The following variables can be customized in `variables.tf`:

| Variable | Description | Default |
|----------|-------------|---------|
| `aws_region` | AWS region for deployment | `us-west-2` |
| `instance_type` | EC2 instance type | `t3.micro` |
| `vpc_cidr` | VPC CIDR block | `10.0.0.0/16` |
| `subnet_cidr` | Subnet CIDR block | `10.0.1.0/24` |
| `key_name` | EC2 key pair name | `webserver-key` |
| `project_name` | Project name for resource naming | `terraform-aws-webserver` |

### Customizing Deployment

Create a `terraform.tfvars` file to override defaults:

```hcl
aws_region = "us-east-1"
instance_type = "t3.small"
key_name = "my-custom-key"
```

## 🔒 Security Features

- **VPC with public subnet** for proper network isolation
- **Security group** with minimal required access:
  - SSH (port 22) for management
  - HTTP (port 80) for web traffic
  - HTTPS (port 443) for secure traffic
  - Application port (3000) for custom apps
- **EC2 instance** with latest Amazon Linux 2 AMI
- **Auto-configured web server** with Apache

## 📊 Monitoring and Management

### Check Instance Status

```bash
terraform show
```

### View Outputs

```bash
terraform output
```

### SSH into Instance

```bash
ssh -i webserver-key.pem ec2-user@<instance_public_ip>
```

### View Application Logs

```bash
# SSH into instance first
sudo tail -f /var/log/httpd/access_log
sudo tail -f /var/log/httpd/error_log
```

## 🧹 Cleanup

When you're done testing, destroy the infrastructure:

```bash
terraform destroy
```

**⚠️ Warning**: This will delete all created resources and data.

## 🔧 Troubleshooting

### Common Issues

1. **"Key pair not found"**
   - Ensure you've created the key pair in AWS
   - Check the key name in `variables.tf`

2. **"Permission denied"**
   - Verify your AWS credentials are configured
   - Check IAM permissions for EC2, VPC, and Security Groups

3. **"Instance not accessible"**
   - Check security group rules
   - Verify the instance is running
   - Check the public IP address

### Useful Commands

```bash
# Check Terraform state
terraform state list

# Refresh state
terraform refresh

# Validate configuration
terraform validate

# Format code
terraform fmt
```

## 🚀 Next Steps

Consider enhancing your infrastructure with:

- **Load Balancer** for high availability
- **Auto Scaling Group** for scalability
- **RDS Database** for data persistence
- **CloudWatch Monitoring** for observability
- **SSL/TLS Certificates** for HTTPS
- **CI/CD Pipeline** with GitHub Actions
- **Containerization** with Docker
- **Multi-region deployment** for disaster recovery

## 📝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Support

If you encounter any issues:

1. Check the [Issues](../../issues) page
2. Create a new issue with detailed information
3. Include logs and error messages

## 🔗 Useful Links

- [Terraform Documentation](https://www.terraform.io/docs)
- [AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)

---

**Note**: This is a learning project. For production use, please ensure proper security configurations and follow AWS best practices.

## 🎯 Learning Outcomes

This project demonstrates:

- **Infrastructure as Code** principles
- **Cloud deployment** best practices
- **Security** configuration
- **Networking** fundamentals
- **Monitoring** and management
- **Terraform** workflow and best practices

---

⭐ **Star this repository** if you found it helpful! 