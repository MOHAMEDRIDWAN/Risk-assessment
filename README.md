# EX 4: RISK ASSESSMENT

**NAME:** MOHAMED RIDWAN A
**REG NO:** 212223110030

## AIM

To perform an asset-oriented risk assessment of cloud storage assets including:

* AWS Elastic Block Store (EBS)
* AWS Elastic File System (EFS)
* Azure Files (File Storage)

---

## PRE-REQUISITES

### 1. Background

Cloud storage services provide flexible, scalable, and highly available storage for applications and users. However, each storage service introduces different security risks depending on its configuration.

This experiment focuses on identifying cloud storage assets and evaluating their security posture based on:

* Confidentiality
* Integrity
* Availability
* Access control
* Encryption
* Backup and recovery
* Network security
* Auditing and monitoring

### 2. Tools Required

* AWS Management Console
* Amazon EC2
* Amazon EBS
* Amazon EFS
* Microsoft Azure Portal
* Azure Storage Account
* IAM credentials with sufficient permissions
* Internet browser
* Microsoft Excel / Google Sheets

---

# 3. PROCEDURE

## PART A — IDENTIFYING AWS STORAGE ASSETS

### Step 1: Login to AWS Console

1. Open the AWS Management Console.
2. Sign in using valid AWS credentials.
3. Open the **EC2** service.

### Step 2: Identify EBS Volumes

1. Navigate to **EC2 → Elastic Block Store → Volumes**.
2. Identify all available EBS volumes.
3. For each volume, record:

* Volume ID
* Size
* Volume type
* Availability Zone
* Attached EC2 instance
* Encryption status
* Tags

Example:

| Parameter         | Observation       |
| ----------------- | ----------------- |
| Volume ID         | vol-0abc123456789 |
| Size              | 8 GB              |
| Volume Type       | gp3               |
| Availability Zone | ap-south-1a       |
| Attached Instance | i-0abc123456789   |
| Encryption        | Enabled           |
| Tags              | Name: WebServer   |

### Step 3: Identify EFS File Systems

1. Open **Amazon EFS** from the AWS Console.
2. Select **File systems**.
3. Identify the available file systems.
4. Record:

* File System ID
* File System Name
* Mount Targets
* Availability Zones
* Throughput Mode
* Performance Mode
* Lifecycle Policy
* Encryption at Rest

Example:

| Parameter          | Observation              |
| ------------------ | ------------------------ |
| File System ID     | fs-0abc123456789         |
| Name               | Project-EFS              |
| Mount Targets      | 2                        |
| Availability Zones | ap-south-1a, ap-south-1b |
| Throughput Mode    | Bursting                 |
| Performance Mode   | General Purpose          |
| Lifecycle Policy   | After 30 days            |
| Encryption         | Enabled                  |

---

# PART B — IDENTIFYING AZURE FILE STORAGE ASSETS

## Step 4: Login to Azure Portal

1. Open the Microsoft Azure Portal.
2. Sign in using valid credentials.
3. Search for **Storage Accounts**.
4. Select the required storage account.

## Step 5: View File Shares

1. Open the selected Storage Account.
2. Navigate to **Data storage → File shares**.
3. Select the required file share.
4. Record:

* File Share Name
* Quota
* Used Space
* Protocol
* Authentication Method
* Snapshot / Backup configuration

Example:

| Parameter       | Observation |
| --------------- | ----------- |
| File Share Name | datafiles   |
| Quota           | 100 GB      |
| Used Space      | 2 GB        |
| Protocol        | SMB         |
| Authentication  | Shared Key  |
| Snapshots       | Enabled     |

---

# 4. RISK ASSESSMENT METHODOLOGY

Each identified storage asset is evaluated based on the following security factors:

### Confidentiality

Checks whether unauthorized users can access stored information.

### Integrity

Checks whether stored information can be modified or deleted without authorization.

### Availability

Checks whether the storage remains available when required.

### Access Control

Checks whether appropriate authentication and authorization mechanisms are implemented.

### Encryption

Checks whether data is protected using encryption at rest and, where applicable, during transmission.

### Backup and Recovery

Checks whether appropriate backup, versioning, snapshots, or recovery mechanisms are available.

### Auditing and Monitoring

Checks whether access and security-related activities can be monitored and investigated.

### Risk Level

The overall risk is classified as:

| Risk Level | Description                                         |
| ---------- | --------------------------------------------------- |
| Low        | Minimal security concern                            |
| Medium     | Requires monitoring or improvement                  |
| High       | Significant security concern requiring mitigation   |
| Critical   | Severe security exposure requiring immediate action |

---

# 5. OBSERVATIONS AND TABULATION

| Cloud Provider | Asset Type      | Asset ID          | Encrypted | Access Control              | Risk Level | Comments                             |
| -------------- | --------------- | ----------------- | --------- | --------------------------- | ---------- | ------------------------------------ |
| AWS            | EBS Volume      | vol-0abc123456789 | Yes       | IAM / EC2 Security Controls | Low        | Encrypted EBS volume attached to EC2 |
| AWS            | EFS File System | fs-0abc123456789  | Yes       | IAM / Security Group        | Low        | Multi-AZ mount targets configured    |
| Azure          | File Share      | datafiles         | Yes       | Shared Key / Azure AD       | Medium     | SMB file share with configured quota |

---

# 6. DETAILED RISK ASSESSMENT

| Asset            | Vulnerability / Concern      | Threat                                         | Likelihood | Impact | Risk Score | Risk Level | Recommended Mitigation                                              |
| ---------------- | ---------------------------- | ---------------------------------------------- | ---------: | -----: | ---------: | ---------- | ------------------------------------------------------------------- |
| EBS Volume       | Encryption disabled          | Unauthorized disclosure of stored data         |          3 |      4 |         12 | High       | Enable EBS encryption                                               |
| EBS Volume       | No recent snapshot/backup    | Data loss after failure or accidental deletion |          3 |      4 |         12 | High       | Configure regular snapshots                                         |
| EFS              | Excessive access permissions | Unauthorized file modification                 |          3 |      4 |         12 | High       | Apply least-privilege IAM and security groups                       |
| EFS              | Encryption disabled          | Exposure of stored data                        |          3 |      4 |         12 | High       | Enable encryption at rest                                           |
| Azure File Share | Shared key used excessively  | Unauthorized access to file data               |          3 |      4 |         12 | High       | Prefer identity-based authentication where appropriate              |
| Azure File Share | Unrestricted network access  | External unauthorized access                   |          3 |      4 |         12 | High       | Restrict network access and use private endpoints where appropriate |

**Risk Score = Likelihood × Impact**

---

# 7. SECURITY ANALYSIS

### AWS EBS

The EBS volumes were examined for encryption, attachment information, volume type, availability zone, and backup considerations. Encryption protects stored data from unauthorized disclosure, while snapshots provide recovery capability in case of accidental deletion or system failure.

### AWS EFS

The EFS file system was evaluated based on encryption, mount targets, performance configuration, lifecycle policy, and access control. Multi-AZ mount targets improve availability, while security groups and IAM policies help control access.

### Azure Files

The Azure File Share was assessed based on authentication, encryption, quota, network accessibility, and snapshot/recovery capabilities. Appropriate access control and network restrictions help prevent unauthorized access to shared files.

---

# 8. FINAL RISK SUMMARY

| Cloud | Asset      | Major Risk                       | Risk Level | Recommended Mitigation                  |
| ----- | ---------- | -------------------------------- | ---------- | --------------------------------------- |
| AWS   | EBS Volume | Encryption/backup not configured | High       | Enable encryption and regular snapshots |
| AWS   | EFS        | Excessive access permissions     | High       | Apply least privilege                   |
| AWS   | EFS        | Encryption disabled              | High       | Enable encryption at rest               |
| Azure | File Share | Excessive shared-key access      | High       | Use appropriate identity-based access   |
| Azure | File Share | Unrestricted network access      | High       | Restrict network access                 |

---

# 9. RESULT

The active cloud storage assets in **AWS EBS, AWS EFS, and Azure Files** were identified and analyzed. Their encryption, access control, availability, backup, and security configurations were evaluated. Potential vulnerabilities and threats were identified, and risk levels were determined based on likelihood and impact. Appropriate security controls and mitigation measures were recommended to improve the overall security posture of the cloud storage assets.
