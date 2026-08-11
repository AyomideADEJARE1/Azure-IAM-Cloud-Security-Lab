# Azure IAM & Cloud Security Lab

## 1. Microsoft Entra ID — Users & Groups

The lab began with basic Microsoft Entra ID administration. Users were reviewed and organized into departmental security groups.

### Groups Used

- `IT-Team`
- `HR-Team`
- `Finance-Team`
- `Sales-Team`

The evidence shows the groups being created and managed, the user directory, and the members of the individual teams.

### Evidence

#### 01 — Azure Environment

![01 — Azure environment](01-azure-home.png)

#### 02 — Initial Entra ID Groups View

![02 — Initial Entra ID groups view](02-entra-groups-initial.png)

#### 03 — Cloud Shell Group-Management Commands

![03 — Cloud Shell group-management commands](screenshots/03-cloud-shell-group-creation.png)

#### 04 — Entra ID Groups

![04 — Entra ID groups](screenshots/04-entra-groups.png)

#### 05 — Entra ID Users

![05 — Entra ID users](screenshots/05-entra-users-basic.png)

#### 06 — Entra ID Users With Additional Details

![06 — Entra ID users with additional details](screenshots/06-entra-users-details.png)

#### 07 — IT-Team Membership

![07 — IT-Team membership](screenshots/07-it-team-members.png)

#### 08 — HR-Team Membership

![08 — HR-Team membership](screenshots/08-hr-team-members.png)

#### 09 — Finance-Team Membership

![09 — Finance-Team membership](screenshots/09-finance-team-members.png)

#### 10 — Sales-Team Membership

![10 — Sales-Team membership](screenshots/10-sales-team-members.png)

---

## 2. Resource Group & Azure RBAC

The lab used the resource group `AdejareTech-IAM-Lab` as the main management scope.

RBAC was then used to give different teams different levels of access. The evidence shows Owner, Contributor, and Reader assignments and their associated team groups.

The project demonstrates the basic idea that users can receive permissions through groups instead of assigning broad permissions individually to every user.

### Evidence

#### 11 — Cloud Shell and Resource Group Setup

![11 — Cloud Shell and Resource Group setup](screenshots/11-cloud-shell-and-resource-group.png)

#### 12 — Resource Group

![12 — Resource group](screenshots/12-resource-group.png)

#### 13 — IAM: Owner and Reader Assignments

![13 — IAM Owner and Reader assignments](screenshots/13-iam-owner-reader.png)

#### 14 — IAM: Contributor and Reader Assignments

![14 — IAM Contributor and Reader assignments](screenshots/14-iam-contributor-reader.png)

#### 15 — IAM Role Assignments

![15 — IAM role assignments](screenshots/15-iam-role-assignments.png)

#### 16 — IAM Team Assignments

![16 — IAM team assignments](screenshots/16-iam-all-team-assignments.png)

#### 17 — Storage Resource and IAM View

![17 — Storage resource and IAM view](screenshots/17-storage-center-and-iam.png)

#### 18 — IAM Assignments at the Storage/Resource Scope

![18 — IAM assignments at the storage/resource scope](screenshots/18-iam-role-assignments-storage-scope.png)

---

## 3. Azure Storage & Blob Storage

The project used the Storage Account:

`adejaretechiamlab01`

Blob Storage was used to provide an actual data resource for the access-control exercise. The evidence shows the Storage Account, its containers, and the test data container.

### Evidence

#### 19 — Storage Account / Storage Center

![19 — Storage Account / Storage Center](screenshots/19-storage-containers.png)

#### 20 — Test-Data Container and Blob

![20 — Test-data container and blob](screenshots/20-test-data-container.png)

---

## 4. Azure Policy — Storage Security

The Microsoft built-in policy below was assigned to the `AdejareTech-IAM-Lab` resource group:

> **Storage accounts should prevent shared key access**

The policy checks whether a Storage Account permits Shared Key access.

### Initial Policy State

The Storage Account was initially evaluated as **NonCompliant**. The evidence shows the policy assignment and the non-compliant resource.

#### 21 — Policy Assignment

![21 — Policy assignment](screenshots/21-policy-assignment.png)

#### 22 — Initial NonCompliant State

![22 — Initial NonCompliant state](screenshots/22-policy-noncompliant.png)

#### 23 — Compliance State Before Remediation

![23 — Compliance state before remediation](screenshots/23-policy-compliance-before.png)

### Remediation

The Shared Key configuration was then remediated. The Storage Account's `allowSharedKeyAccess` setting was changed from `true` to `false`.

A policy re-evaluation was triggered using Azure CLI.

### Final State

The resource was subsequently evaluated as **Compliant**.

#### 24 — Final Compliant State

![24 — Final Compliant state](screenshots/24-policy-compliant.png)

---

## 5. Security Workflow

The complete policy portion of the lab followed this process:

```text
Storage Account
      ↓
Azure Policy assignment
      ↓
Security configuration evaluated
      ↓
NonCompliant finding
      ↓
Investigation
      ↓
Shared Key access disabled
      ↓
Policy re-evaluation
      ↓
Compliant
```

---

## 6. Additional RBAC Least-Privilege Test

A separate Entra ID test identity named **RBAC Lab Reader** was created for a focused least-privilege exercise.

It was assigned: `Storage Blob Data Reader`

at the Storage Account scope: `adejaretechiamlab01`

The assignment was verified with Azure CLI.

This additional step demonstrates how a dedicated identity can receive narrow data-plane access without using the administrator account for the test.

---

## 7. Security Concepts Demonstrated
- `Microsoft Entra ID user management`
- `Microsoft Entra ID groups`
- `Group membership`
- `Azure RBAC`
- `Role-based access control`
- `Least privilege`
- `Azure Storage`
- `Blob Storage`
- `Azure Policy`
- `Security misconfiguration detection`
- `Security remediation`
- `Compliance verification`
- `Azure CLI`

---

## 8. Key Outcome

This lab demonstrates a practical cloud-security workflow:

1. Manage identities and groups.
2. Apply group-based access control.
3. Configure Azure Storage resources.
4. Audit a security configuration with Azure Policy.
5. Investigate a NonCompliant finding.
6. Remediate the security issue.
7. Verify that the resource becomes Compliant.
8. Apply a narrowly scoped data-access role to a dedicated test identity.

---
