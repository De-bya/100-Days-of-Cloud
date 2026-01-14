# Day 2: Create Security Group

## Problem Statement

The Nautilus DevOps team is migrating infrastructure to AWS cloud in incremental steps. As part of this migration, they need to set up proper security controls for their application servers.

**Task:** Create a security group in the default VPC to allow web traffic and SSH access to the Nautilus App Servers.

## Requirements

- **Name:** `nautilus-sg`
- **Description:** `Security group for Nautilus App Servers`
- **Region:** `us-east-1`
- **Inbound Rules:**
  - HTTP (Port 80) from anywhere (0.0.0.0/0)
  - SSH (Port 22) from anywhere (0.0.0.0/0)

## Solution

### Step 1: Create the Security Group

```bash
aws ec2 create-security-group \
    --group-name nautilus-sg \
    --description "Security group for Nautilus App Servers" \
    --region us-east-1
```

### Step 2: Add HTTP Inbound Rule

```bash
aws ec2 authorize-security-group-ingress \
    --group-name nautilus-sg \
    --protocol tcp \
    --port 80 \
    --cidr 0.0.0.0/0 \
    --region us-east-1
```

### Step 3: Add SSH Inbound Rule

```bash
aws ec2 authorize-security-group-ingress \
    --group-name nautilus-sg \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0 \
    --region us-east-1
```

### Step 4: Verify Configuration

```bash
aws ec2 describe-security-groups \
    --group-names nautilus-sg \
    --region us-east-1
```

## Understanding the Solution

**What is a Security Group?**
- Acts as a virtual firewall for your cloud servers
- Controls what traffic can enter (inbound) or leave (outbound) your servers
- Essential for securing cloud infrastructure

**What we created:**
- **Port 80 (HTTP):** Allows web browsers to access applications running on the servers
- **Port 22 (SSH):** Allows administrators to remotely login and manage the servers
- **CIDR 0.0.0.0/0:** Means "from anywhere on the internet" (in production, you'd restrict this to specific IPs)

**Command Breakdown:**
- `aws ec2 create-security-group`: Creates a new security group
- `aws ec2 authorize-security-group-ingress`: Adds an inbound traffic rule
- `--protocol tcp`: Specifies TCP protocol
- `--port`: The port number to open
- `--cidr`: IP range allowed to connect (0.0.0.0/0 = everyone)
