# Day 1: Create Key Pair

## Problem Statement

The Nautilus DevOps team is migrating infrastructure to AWS cloud in incremental steps. As part of the initial setup, they need to create SSH key pairs to securely access EC2 instances (virtual servers) in the cloud.

**Task:** Create an EC2 key pair that will be used for secure SSH authentication to cloud servers.

## Requirements

- **Key pair name:** `datacenter-kp`
- **Key type:** `rsa`
- **Region:** `us-east-1`

## Solution

### Create the Key Pair

```bash
aws ec2 create-key-pair \
    --key-name datacenter-kp \
    --key-type rsa \
    --query 'KeyMaterial' \
    --output text > datacenter-kp.pem
```

### Set Proper Permissions

```bash
chmod 400 datacenter-kp.pem
```

### Verify the Key Pair

```bash
aws ec2 describe-key-pairs --key-names datacenter-kp
```

## Understanding the Solution

**What is a Key Pair?**
- A key pair consists of a public key (stored in AWS) and a private key (stored on your computer)
- It's used for secure SSH authentication instead of passwords
- Think of it like a digital lock and key system

**What we created:**
- **RSA key pair:** A type of encryption algorithm for secure connections
- **Private key file (.pem):** Saved locally - this is your "key" to access servers
- **Public key:** Stored in AWS - this is the "lock" on your servers

**Command Breakdown:**
- `aws ec2 create-key-pair`: Creates a new key pair in AWS
- `--key-name datacenter-kp`: Names the key pair
- `--key-type rsa`: Specifies RSA encryption type
- `--query 'KeyMaterial'`: Extracts only the private key content
- `--output text > datacenter-kp.pem`: Saves the private key to a file
- `chmod 400`: Sets file permissions to read-only for owner (security requirement)

**Why chmod 400?**
SSH requires that private key files are not accessible by others. The `400` permission means:
- Owner can read (4)
- Group cannot access (0)
- Others cannot access (0)
