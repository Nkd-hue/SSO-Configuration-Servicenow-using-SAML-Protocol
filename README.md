
# 🔐 IdP-Initiated SSO with SAML — Microsoft Entra ID + ServiceNow

## Overview

This project documents the configuration of Single Sign-On (SSO) using the SAML 2.0 protocol between **Microsoft Entra ID** (Identity Provider) and **ServiceNow** (Service Provider) within the NovaTech Solutions home lab environment.

The goal was to demonstrate IdP-initiated SSO, in which an authenticated user is seamlessly redirected from Entra ID to ServiceNow without re-entering credentials.

---

## Architecture

```
User → Microsoft Entra ID (IdP) → SAML Assertion → ServiceNow (SP)
```

| Component | Role | Platform |
|---|---|---|
| Microsoft Entra ID | Identity Provider (IdP) | Azure |
| ServiceNow | Service Provider (SP) | ServiceNow PDI |
| Protocol | SAML 2.0 | — |
| SSO Type | IdP-Initiated | — |

---

## Prerequisites

- Microsoft Entra ID tenant (Azure subscription or free tier)
- ServiceNow Personal Developer Instance (PDI)
- Global Administrator or Application Administrator role in Entra ID

---

## Configuration Steps

### Step 1: Register ServiceNow as an Enterprise Application

1. Navigate to **Microsoft Entra admin center** → **Enterprise Applications**
2. Click **New Application**
3. Search for **ServiceNow** in the Microsoft Entra App Gallery
4. Click **Create**

---

### Step 2: Configure SAML Settings in Entra ID

1. Open the ServiceNow Enterprise Application
2. Navigate to **Single Sign-On → SAML**
3. Edit **Basic SAML Configuration** with the following values:

| Field | Value |
|---|---|
| Identifier (Entity ID) | `https://<your-instance>.service-now.com` |
| Reply URL (ACS URL) | `https://<your-instance>.service-now.com` |
| Sign-On URL | `https://<your-instance>.service-now.com` |

> Replace `<your-instance>` with your ServiceNow PDI instance name (e.g. `dev270383`)

4. Click **Save**

---

### Step 3: Configure User Attributes & Claims

Default claims were retained:

| Claim | Value |
|---|---|
| emailaddress | user.mail |
| name | user.userprincipalname |
| givenname | user.givenname |
| surname | user.surname |

---

### Step 4: Assign Users

1. Navigate to **Users and Groups** within the Enterprise Application
2. Click **Add User/Group**
3. Assign the relevant user(s) to the application

---

### Step 5: Test SSO

1. Navigate to **Single Sign-On → SAML**
2. Click **Test this application**
3. Entra ID issued a SAML assertion and redirected the authenticated session directly into ServiceNow

✅ **Result:** IdP-initiated SSO confirmed — authenticated directly into ServiceNow with no additional credential prompt.

---
### Screenshots
<img width="1710" height="1107" alt="Screenshot 2026-05-06 at 1 53 16 PM" src="https://github.com/user-attachments/assets/4a21724f-8207-40a8-85ee-90728ecd5ce5" />

<img width="1710" height="1107" alt="Screenshot 2026-05-06 at 4 59 44 PM" src="https://github.com/user-attachments/assets/ecb29c69-5617-4cf1-b4f4-44a6efe6c461" />

<img width="1710" height="1107" alt="Screenshot 2026-05-06 at 5 03 48 PM" src="https://github.com/user-attachments/assets/5462c72b-f1ba-45df-8d92-35153ee428d7" />

<img width="1710" height="1107" alt="Screenshot 2026-05-06 at 5 01 32 PM" src="https://github.com/user-attachments/assets/c69514be-2c82-4b3f-95fa-01ecdd7cfacd" />

## Key Concepts

**Single Sign-On (SSO)**
Allows users to authenticate once and gain access to multiple applications using an active session token, eliminating repeated login prompts.

**SAML 2.0 (Security Assertion Markup Language)**
An XML-based open standard for exchanging authentication and authorization data between an Identity Provider (IdP) and a Service Provider (SP).

**IdP-Initiated SSO**
The authentication flow originates from the Identity Provider. The user logs into Entra ID and is pushed directly into the target application via a SAML assertion.

**Why SSO Matters**
- Reduces password fatigue across users
- Shrinks the attack surface for credential-based threats (phishing, brute force)
- Centralizes access control and audit logging
- Core component of Zero Trust architecture

---

## Environment

| Detail | Value |
|---|---|
| Lab Name | NovaTech Solutions |
| Domain | novatechs.solutions |
| Identity Platform | Microsoft Entra ID |
| ServiceNow Instance | Personal Developer Instance (PDI) |
| Release | Australia |

---

## Related Projects

- [Enterprise Hybrid Identity Infrastructure](https://github.com/Nkd-hue)
- [Zero Trust Authentication & Conditional Access Framework](https://github.com/Nkd-hue)
- [Identity Governance & Lifecycle Management](https://github.com/Nkd-hue)

---

## Author

**Nadia Kroduah**
Identity & Access Management Analyst | SC-300 | Microsoft Entra ID | Secret Clearance
[GitHub](https://github.com/Nkd-hue) • [LinkedIn](https://www.linkedin.com/in/)
