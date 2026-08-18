# Secure EC2 Monitoring & Alerting System

## 📌 Project Overview

A secure AWS monitoring system that automatically monitors an EC2 instance and sends an email alert when CPU utilization exceeds a defined threshold.

## 🎯 Problem Statement

Manually monitoring server resources is inefficient and can cause administrators to miss abnormal resource usage.

This project solves the problem by implementing automated monitoring and alerting using AWS CloudWatch and SNS.

## 🏗️ AWS Architecture

EC2 Instance
→ IAM Role
→ CloudWatch
→ CloudWatch Alarm
→ SNS
→ Email Alert

The EC2 instance is deployed inside a custom VPC and public subnet.

## ☁️ AWS Services Used

- Amazon VPC
- Amazon EC2
- IAM Role
- IAM Policy
- CloudWatch
- CloudWatch Agent
- CloudWatch Alarm
- Amazon SNS
- Nginx

## 🔐 Security

- EC2 deployed inside a custom VPC
- IAM Role used instead of storing AWS access keys on the server
- Security Group controls inbound traffic
- CloudWatch permissions provided through an IAM Role

## 📊 Monitoring

CloudWatch monitors:

- CPU utilization
- Memory utilization
- Disk utilization

The CloudWatch Agent publishes memory and disk metrics under the custom namespace:

`SecureMonitoring`

EC2 automatically provides CPU metrics through:

`AWS/EC2`

## 🚨 Alerting

A CloudWatch Alarm was configured with:

- Metric: CPUUtilization
- Threshold: Greater than 70%
- Evaluation period: 5 minutes
- Action: SNS notification

When CPU utilization exceeds the threshold, the alarm enters the `ALARM` state and SNS sends an email notification.

## 🧪 Testing

CPU stress was intentionally generated on the EC2 instance.

The test successfully demonstrated:

EC2 CPU spike
→ CloudWatch detects high CPU
→ CloudWatch Alarm enters ALARM state
→ SNS sends notification
→ Email received successfully

## 📸 Project Evidence

Screenshots demonstrating the implementation are available in the `screenshots` directory.

## 🎓 Key Learnings

- Creating and configuring a custom AWS VPC
- Working with public subnets and Internet Gateways
- Launching EC2 instances
- Attaching IAM Roles to EC2
- Configuring CloudWatch Agent
- Creating CloudWatch Alarms
- Configuring SNS email notifications
- Testing automated monitoring and alerting

## 👨‍💻 Project Outcome

Successfully implemented an automated AWS EC2 monitoring and alerting system that detects abnormal CPU utilization and notifies the administrator through email.
