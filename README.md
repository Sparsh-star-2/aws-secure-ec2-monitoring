# Secure EC2 Monitoring & Alerting System

An AWS monitoring and alerting project that uses Amazon CloudWatch and SNS to monitor EC2 resource utilization and automatically notify administrators when CPU usage exceeds a defined threshold.

## 📌 Project Overview

This project demonstrates how to implement secure EC2 monitoring and automated alerting using AWS managed services.

It collects system-level metrics, evaluates CPU utilization through CloudWatch Alarms, and sends email notifications through Amazon SNS when abnormal CPU usage is detected.

The project covers:

- EC2 infrastructure deployment inside a custom VPC
- IAM Role-based access management
- CloudWatch monitoring and custom metrics
- Automated CPU threshold monitoring
- SNS email notifications
- CPU stress testing and alert validation

# 🏗️ AWS Architecture

```text
                 ┌─────────────────────┐
                 │     Custom VPC      │
                 │                     │
                 │   Public Subnet     │
                 │                     │
                 │    EC2 Instance     │
                 │         │           │
                 │      Nginx          │
                 │         │           │
                 │  CloudWatch Agent   │
                 └─────────┬───────────┘
                           │
                      IAM Role
                           │
                           ▼
                    Amazon CloudWatch
                           │
                    CloudWatch Alarm
                           │
                    CPU > 70% for
                     5 minutes
                           │
                           ▼
                       Amazon SNS
                           │
                           ▼
                      Email Alert
```

# ☁️ AWS Infrastructure

| AWS Service | Purpose |
|---|---|
| Amazon VPC | Isolated network environment |
| Public Subnet | Hosts the EC2 instance |
| Internet Gateway | Internet connectivity for the public subnet |
| Amazon EC2 | Server being monitored |
| IAM Role | Secure permissions for EC2 |
| IAM Policy | Defines CloudWatch permissions |
| CloudWatch | Metric collection and monitoring |
| CloudWatch Agent | Collects memory and disk metrics |
| CloudWatch Alarm | Detects high CPU utilization |
| Amazon SNS | Sends email notifications |

# 🛠️ Technology Stack

| Technology | Usage |
|---|---|
| AWS EC2 | Cloud server |
| AWS VPC | Network isolation |
| AWS IAM | Identity and access management |
| Amazon CloudWatch | Monitoring and metrics |
| CloudWatch Agent | System-level metric collection |
| Amazon SNS | Email alerting |
| Linux / Ubuntu | Server operating system |
| Nginx | Web server |
| Shell Commands | Server administration |

# ✨ Key Features

## 1. Secure EC2 Infrastructure

- Deploys EC2 inside a custom VPC and public subnet
- Uses Security Groups to control inbound traffic
- Attaches an IAM Role to the EC2 instance
- Avoids storing AWS access keys directly on the server

## 2. CloudWatch Monitoring

Monitors the following system metrics:

| Metric | Source | Purpose |
|---|---|---|
| CPU Utilization | `AWS/EC2` | Monitors processor usage |
| Memory Utilization | `SecureMonitoring` | Tracks memory consumption |
| Disk Utilization | `SecureMonitoring` | Tracks disk usage |

The CloudWatch Agent collects memory and disk metrics and publishes them under the custom namespace:

`SecureMonitoring`

EC2 provides CPU utilization metrics through the default namespace:

`AWS/EC2`

## 3. Automated Alerting

A CloudWatch Alarm monitors CPU utilization and triggers an SNS notification when the configured threshold is exceeded.

**CloudWatch Alarm Configuration**

| Setting | Value |
|---|---|
| Metric | CPUUtilization |
| Namespace | AWS/EC2 |
| Threshold | Greater than 70% |
| Evaluation Period | 5 minutes |
| Notification Service | Amazon SNS |
| Notification Type | Email |

## 4. Email Notifications

- Configures an SNS topic for notifications
- Connects the CloudWatch Alarm to SNS
- Sends email alerts when the alarm enters the `ALARM` state
- Helps administrators respond to abnormal CPU utilization

# 🔐 Security Configuration

Security was implemented using AWS identity and network controls.

- EC2 deployed inside a custom VPC
- Public subnet configured for the EC2 instance
- Security Group controls inbound access
- IAM Role attached to EC2
- IAM permissions provided through an IAM Policy
- No hardcoded AWS access keys stored on the instance

# 📊 Monitoring & Alerting Workflow

```text
EC2 Instance
     │
     ▼
CloudWatch Metrics
     │
     ├── CPU → AWS/EC2
     │
     └── Memory & Disk → SecureMonitoring
                            │
                            ▼
                    CloudWatch Alarm
                            │
                     CPU > 70%
                      for 5 minutes
                            │
                            ▼
                       SNS Topic
                            │
                            ▼
                     Email Notification
```

# 🧪 Testing & Validation

The monitoring and alerting workflow was tested by intentionally generating CPU stress on the EC2 instance.

**Test Execution Flow**

1. Generated CPU load on the EC2 instance.
2. CloudWatch detected increased CPU utilization.
3. CPU utilization crossed the configured threshold.
4. CloudWatch Alarm entered the `ALARM` state.
5. SNS triggered an email notification.
6. Email notification was successfully received.

<badge color="success">Successfully tested</badge> Automated CPU monitoring and email alert delivery.

# 📸 Project Screenshots

Screenshots demonstrating the implementation, AWS configuration, monitoring metrics, and alerting workflow are available in the `screenshots` directory.

# 📁 Project Structure

```text
aws-secure-ec2-monitoring/
│
├── screenshots/
│   ├── vpc-configuration
│   ├── ec2-instance
│   ├── iam-role
│   ├── cloudwatch-agent
│   ├── cloudwatch-metrics
│   ├── cloudwatch-alarm
│   └── sns-email-alert
│
├── scripts/
│
└── README.md
```

# 🎯 Learning Objectives

This project demonstrates practical experience with:

- AWS VPC and subnet configuration
- EC2 instance deployment
- IAM Roles and Policies
- Linux server administration
- CloudWatch metrics and namespaces
- CloudWatch Agent configuration
- CloudWatch Alarm creation
- SNS email notifications
- Automated monitoring and alerting
- CPU stress testing and validation

# 🚧 Future Improvements

- Add automated disk and memory threshold alarms
- Configure additional alert conditions
- Implement backup monitoring
- Improve alert messages with metric details
- Add centralized monitoring dashboards
- Introduce automated recovery actions where appropriate

# 📚 Project Purpose

The purpose of this project is to demonstrate how AWS monitoring and alerting services can be used to maintain visibility into EC2 resource utilization and notify administrators when resource usage becomes abnormal.

It combines AWS infrastructure, IAM security, Linux administration, CloudWatch monitoring, and SNS notifications in a practical cloud environment.

# 👨‍💻 Author

**Sparsh Jambhulkар**

AWS | Cloud | DevOps | Linux | Python

# 📄 Project Ownership

This project was implemented as a hands-on learning project to demonstrate practical AWS infrastructure monitoring, security, and automated alerting skills.
