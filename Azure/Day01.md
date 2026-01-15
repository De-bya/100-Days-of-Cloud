# Day 1: Create SSH Key Pair for Azure Virtual Machine

## Problem Statement

The Nautilus DevOps team is migrating infrastructure to Azure cloud in incremental steps. As part of the initial setup, they need to create SSH key pairs to securely access Azure virtual machines (VMs) in the cloud.

**Task:** Create an SSH key pair in Azure that will be used for secure SSH authentication to cloud VMs.

## Requirements

- **Key pair name:** `datacenter-kp`
- **Key type:** `rsa`

## Solution

### Step 1: Check Available Resource Groups

```bash
az group list --output table
```

This shows all resource groups in your Azure subscription. You'll need one for the next step.

### Step 2: Create the SSH Key Pair

```bash
az sshkey create --name datacenter-kp --resource-group <your-resource-group-name>
```

Replace `<your-resource-group-name>` with the actual name from Step 1.

Example:
```bash
az sshkey create --name datacenter-kp --resource-group kml_rg_main-1334a144182245fa
```

### Step 3: Verify the SSH Key

```bash
az sshkey list --output table
```

## Understanding the Solution

**What is an SSH Key Pair?**
- A key pair consists of a public key (stored in Azure) and a private key (stored on your computer)
- Used for secure authentication instead of passwords

**What we created:**
- **RSA key pair:** A type of encryption algorithm for secure connections
- **Private key file:** Saved locally on your machine (your "key" to access VMs)
- **Public key:** Stored in Azure (the "lock" on your VMs)

**Command Breakdown:**
- `az sshkey create`: Creates a new SSH key pair in Azure
- `--name datacenter-kp`: Names the key pair
- `--resource-group`: Specifies which resource group to store the key in
- `--output table`: Formats the output as a readable table


- The private key location is shown when you create the key
- In production, use different key pairs for different environments

---

**Status:** ✅ Completed
