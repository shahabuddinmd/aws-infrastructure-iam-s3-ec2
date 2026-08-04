# AWS Infrastructure & Security Deployment (IAM, S3 Static Hosting, EC2 Role Delegation)

## Overview
This repository documents the implementation of a secure AWS infrastructure project demonstrating cloud security best practices, credential-less server access using IAM Roles, static website hosting via Amazon S3, and Amazon EC2 instance provisioning.

---

## Architecture & Implementation Summary

### 1. Identity & Access Management (IAM)
* Created a custom IAM Role: `EC2-S3-ReadOnly-Role`.
* Attached AWS managed policy: `AmazonS3ReadOnlyAccess`.
* **Security Outcome:** Completely eliminated reliance on hardcoded credentials on the application server.

### 2. Storage & Hosting (Amazon S3)
* Created bucket: `agency-ai-landingpage`.
* Disabled Block Public Access settings to enable public static delivery.
* Configured Static Website Hosting with index document `index.html`.
* Applied a JSON Bucket Policy for public read permissions:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "PublicReadGetObject",
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::agency-ai-landingpage/*"
      }
    ]
  }
