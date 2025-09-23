# Hybrid-IAM-Entra-AWS
Case study and technical documentation: Integrating Microsoft Entra ID as a central Identity Provider (IdP) for AWS IAM Identity Center in a hybrid and multi-cloud environment.

---

# Hybrid Identity and Access Management with Entra ID & AWS

This repository documents the **integration of Microsoft Entra ID as the central Identity Provider (IdP)** for AWS IAM Identity Center.  
It focuses on extending hybrid identity from on-premises Active Directory to AWS, enabling secure provisioning, Single Sign-On (SSO), and enforcing Zero Trust principles.

---

# Project Overview
In hybrid and multi-cloud environments, organizations often need a **unified identity provider** to secure access across on-premises and cloud resources.  
This project explores how **Microsoft Entra ID** can be configured as the **central IdP** to integrate with AWS and Azure.

---

# Current Scope
This article currently covers the **AWS + Entra ID integration**:
- Configuring Entra ID as a **SAML IdP** for AWS IAM Identity Center.  
- Automating provisioning with **SCIM** (users & groups).  
- Assigning **role-based access** in AWS via Entra groups.  

---

# Planned Extensions
Future articles may include:
- Synchronizing on-premises Active Directory with Entra ID using **Password Hash Synchronization (PHS)**. 
- **Global Secure Access (GSA)** deployment for VPN-less, Zero Trust network access.  
- **Zero Trust enforcement**: Verify explicitly, Least privilege, Assume breach.
- **Cloud Security Best Practices**  
  - AWS Well-Architected Framework (Security Pillar).  
  - Azure Security Center hardening.  
  - Continuous monitoring with SIEM integration.  


---

# Microsoft Entra ID Integration with AWS

Microsoft Entra ID (formerly Azure AD) enables centralized identity and access management for **AWS environments**, helping organizations replace fragmented AWS IAM silos with a **unified and secure access model**.

---

## Key Points
- **AWS Default IAM Model**: Each AWS account has its own IAM store, creating identity silos that are difficult to manage across multiple accounts.  
- **Entra ID Integration**: By integrating AWS accounts with Microsoft Entra ID, organizations enable:  
  - Single Sign-On (SSO) for apps and AWS resources.  
  - Centralized identity governance.  
  - Secure access for administrators and developers using their existing Entra identities.  

---

## Core Capabilities
- SSO across AWS and SaaS applications.  
- Multi-Factor Authentication (MFA) with support for third-party providers.  
- Conditional Access with risk-based authentication.  
- Threat detection & automated response leveraging Microsoft’s global threat intelligence.  
- Privileged Identity Management (PIM) time-limited role activation, with full audit logging.
- Identity Protection : Risk-based policies that detect compromised credentials, risky sign-ins, and anomalies.  
- Microsoft Defender for Identity : Detects threats targeting on-premises Active Directory and identity infrastructure, reducing the attack surface against advanced threats like lateral movement or domain dominance.
  
<img width="2838" height="1203" alt="image" src="https://github.com/user-attachments/assets/708b532e-d4a1-41ff-9721-dca04c4e732c" />

---

## 🔗 How SAML and SCIM Are Used

This project leverages **SAML** and **SCIM** to centralize authentication and automate user provisioning between **Microsoft Entra ID** and **AWS IAM Identity Center**.

### SAML (Security Assertion Markup Language)
- **Purpose:** Provides secure Single Sign-On (SSO) from Entra ID to AWS.

### SCIM (System for Cross-domain Identity Management)
- **Purpose:** Automates user and group provisioning between Entra ID and AWS.

**Together**, SAML and SCIM enable a **fully automated, centralized, and secure identity model**, forming the backbone of a Zero Trust hybrid identity solution.


<img width="2859" height="1293" alt="image" src="https://github.com/user-attachments/assets/2214d659-8fe9-4b8d-bd24-ce1563c340f3" />

-

First, navigate to **AWS IAM Identity Center** and change the default Identity Provider (IdP) to **Microsoft Entra ID**.  
To configure SAML, you can use the metadata file provided by AWS IAM Identity Center and upload it to Entra ID.  
This simplifies the configuration process and ensures a secure, seamless connection between Entra ID and AWS for Single Sign-On (SSO).


<img width="2610" height="1202" alt="image" src="https://github.com/user-attachments/assets/1cdc38d5-3d05-4fe9-820e-c6387e58aaed" />


Next, go to **Enterprise Applications** in Microsoft Entra ID, add the **AWS IAM Identity Center** application, and configure it for SAML-based Single Sign-On.  
This step connects Entra ID as the central Identity Provider, enabling secure authentication and role mapping for AWS users.


<img width="2595" height="1316" alt="image" src="https://github.com/user-attachments/assets/9dd25419-ff84-47af-9448-ba25641e77f5" />


Now, you can use the **metadata file** downloaded from **AWS IAM Identity Center** to configure the SAML protocol in Microsoft Entra ID.  
Uploading this metadata file automatically sets the required endpoints and certificates, simplifying the SAML configuration and ensuring a secure connection between Entra ID and AWS.


<img width="2235" height="688" alt="image" src="https://github.com/user-attachments/assets/369462b6-25d6-4a65-9f68-8687980de669" />


Similarly, you can download the **federation metadata XML file** from Microsoft Entra ID and use it to configure the **Identity Provider metadata** in AWS IAM Identity Center.  
This step ensures that AWS trusts Entra ID for SAML-based Single Sign-On, completing the bidirectional configuration between the two systems.



<img width="2218" height="1080" alt="image" src="https://github.com/user-attachments/assets/95e2e9ca-da65-4271-a13f-a10a569acb43" />

-

<img width="2276" height="856" alt="image" src="https://github.com/user-attachments/assets/a280958a-38d0-431c-a9e3-7552b0fd3056" />



Once these steps are completed, the Identity Provider (IdP) has been successfully updated, and AWS IAM Identity Center is now fully integrated with Microsoft Entra ID for SAML-based Single Sign-On.



<img width="2243" height="1100" alt="image" src="https://github.com/user-attachments/assets/b074a158-e09a-499b-b923-c2ec5f72d738" />

-

Next, we move on to **automated provisioning configuration**.  
This involves setting up **SCIM-based synchronization** between Microsoft Entra ID and AWS IAM Identity Center, allowing users and groups to be automatically provisioned, updated, or deprovisioned in AWS based on their Entra ID attributes and group memberships.

To enable automated provisioning, Microsoft Entra ID requires the **SCIM endpoint URL** and the corresponding **API key** from AWS IAM Identity Center.  
These credentials allow Entra ID to securely push users and groups from the Azure tenant to AWS IAM Identity Center, ensuring that account creation, updates, and deprovisioning are automatically synchronized.

<img width="2147" height="1135" alt="image" src="https://github.com/user-attachments/assets/e4253aa3-5f4f-43fe-9959-db27a757e583" />

-

<img width="871" height="482" alt="image" src="https://github.com/user-attachments/assets/959cedf3-65be-4ee0-907f-4a3d987dde15" />



### 3. Verify Provisioning
- After configuration, the test user (`admin@mohammedhilali.com`) created in Entra ID should appear in AWS IAM Identity Center.
  
<img width="2248" height="927" alt="image" src="https://github.com/user-attachments/assets/28d1cee9-df51-447e-9796-856563680501" />

-

<img width="2231" height="830" alt="image" src="https://github.com/user-attachments/assets/fc36e303-3d6b-4315-ac42-dbe150b6b488" />

-

<img width="2234" height="596" alt="image" src="https://github.com/user-attachments/assets/7c5d3a2c-6429-4aa3-a275-c04d7ee9292c" />

Now, the user can access AWS resources from **MyApps** and authenticate using **Microsoft Entra ID** as the central Identity Provider (IdP).

<img width="2259" height="556" alt="image" src="https://github.com/user-attachments/assets/03c0bf57-bdb3-46a0-9f68-63c0341774cf" />



