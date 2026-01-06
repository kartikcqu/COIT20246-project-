# Cybersecurity Risk Assessment and Controls

## 1. Risk Assessment Overview

This section presents a cybersecurity risk assessment for Truelec's network infrastructure. The assessment follows the methodology taught in COIT20246, using the provided risk assessment template.

### 1.1 Scope of Assessment

The risk assessment covers:
- Headquarters network (65 staff, 3 floors, Brisbane)
- One branch office network (Perth, 22 staff)
- Network infrastructure (routers, switches, WiFi)
- Data assets (customer data, HR records, financial data, project data)
- Security systems (CCTV, IoT sensors, RFID access)

### 1.2 Assessment Methodology

1. **Identify Assets:** List all critical assets (hardware, software, data)
2. **Identify Threats:** Consider 8+ of the 12 information security threats
3. **Identify Vulnerabilities:** Determine weaknesses that threats can exploit
4. **Calculate Risk:** Assess likelihood and impact, calculate risk scores
5. **Prioritize Risks:** Rank assets by risk level
6. **Recommend Controls:** Suggest security controls for highest-risk assets

## 2. Asset Inventory

### 2.1 Hardware Assets

| Asset ID | Asset Name | Asset Type | Location | Description |
|----------|-----------|------------|----------|-------------|
| HW-001 | Core Router 1 | Hardware | HQ Floor 1 | Primary core router for headquarters |
| HW-002 | Core Router 2 | Hardware | HQ Floor 1 | Backup core router for headquarters |
| HW-003 | Distribution Switches | Hardware | HQ All Floors | 9 switches across 3 floors |
| HW-004 | WiFi Access Points | Hardware | HQ All Floors | 15 WiFi APs providing wireless coverage |
| HW-005 | File Servers | Hardware | HQ Floor 1 | 2 file servers storing company documents |
| HW-006 | Branch Router | Hardware | Perth Branch | Main router for Perth office |

### 2.2 Software Assets

| Asset ID | Asset Name | Asset Type | Description |
|----------|-----------|------------|-------------|
| SW-001 | Windows Server OS | Software | Operating system for file servers |
| SW-002 | CRM System | Software | Customer Relationship Management application |
| SW-003 | HR Management System | Software | Employee records and payroll system |
| SW-004 | Accounting Software | Software | Financial management system |
| SW-005 | Booking Application | Software | Special-purpose booking app for projects |

### 2.3 Data Assets

| Asset ID | Asset Name | Asset Type | Description | Confidentiality | Integrity | Availability |
|----------|-----------|------------|-------------|-----------------|-----------|--------------|
| DA-001 | Customer Database | Data | Client contact info, project details, contracts | HIGH | HIGH | HIGH |
| DA-002 | Employee HR Records | Data | Personal info, salaries, performance reviews | HIGH | HIGH | MEDIUM |
| DA-003 | Financial Records | Data | Invoices, payments, tax documents, payroll | HIGH | HIGH | HIGH |
| DA-004 | Project Documentation | Data | Project plans, technical drawings, specifications | MEDIUM | HIGH | MEDIUM |
| DA-005 | CCTV Footage | Data | Security camera recordings | MEDIUM | MEDIUM | LOW |

### 2.4 People Assets

| Asset ID | Asset Name | Asset Type | Description |
|----------|-----------|------------|-------------|
| PE-001 | ICT Staff | People | 10 IT professionals managing network and systems |
| PE-002 | Administrative Staff | People | Staff with access to sensitive HR and financial data |
| PE-003 | Project Managers | People | Staff with access to customer and project data |

## 3. Threat and Vulnerability Analysis

### 3.1 Information Security Threats Considered

We analyzed the following **8 threats** from the 12 standard information security threats:

1. **Malware** (virus, worm, trojan, ransomware)
2. **Unauthorized Access** (hackers, insiders)
3. **Phishing and Social Engineering**
4. **Denial of Service (DoS/DDoS)**
5. **Data Breach/Data Leakage**
6. **Physical Theft or Damage**
7. **System Failure** (hardware/software failure)
8. **Human Error** (accidental deletion, misconfiguration)

### 3.2 Risk Assessment Matrix

![TVA Matrix Screenshot](risk-assessment/tva-matrix-screenshot.png)

The complete risk assessment spreadsheet is available at: [risk-assessment.xlsx](risk-assessment/risk-assessment.xlsx)

### 3.3 Key Risk Findings (Summary)

Below is a summary of the highest-risk scenarios identified:

| Asset | Threat | Vulnerability | Likelihood | Impact | Risk Score | Risk Level |
|-------|--------|---------------|------------|--------|------------|------------|
| **DA-001: Customer Database** | Data Breach | Weak authentication, unencrypted storage | High (4) | Critical (5) | 20 | **CRITICAL** |
| DA-003: Financial Records | Ransomware | No offline backups, outdated antivirus | High (4) | Critical (5) | 20 | **CRITICAL** |
| DA-002: Employee HR Records | Unauthorized Access | Insufficient access controls | Medium (3) | High (4) | 12 | **HIGH** |
| HW-001: Core Router 1 | DoS Attack | Single point of failure without redundancy | Medium (3) | High (4) | 12 | **HIGH** |
| SW-002: CRM System | Phishing Attack | Staff not trained on phishing awareness | High (4) | Medium (3) | 12 | **HIGH** |
| DA-004: Project Documentation | Human Error (deletion) | No version control, limited backups | Medium (3) | Medium (3) | 9 | **MEDIUM** |
| HW-005: File Servers | Hardware Failure | Aging hardware (5 years old) | Medium (3) | Medium (3) | 9 | **MEDIUM** |
| DA-005: CCTV Footage | Physical Theft | Cameras accessible without authentication | Low (2) | Low (2) | 4 | **LOW** |

**Highest Risk Asset:** **DA-001: Customer Database** (Risk Score: 20 - CRITICAL)

## 4. Detailed Risk Analysis - Highest Risk Asset

### 4.1 Asset: Customer Database (DA-001)

**Description:** Database containing customer contact information, project details, contracts, payment information, and communication history.

**Why This Asset is Critical:**
- Contains personally identifiable information (PII) of hundreds of customers
- Loss or breach would violate Privacy Act 1988 and damage company reputation
- Critical for business operations - customer relationships depend on this data
- Financial impact: Potential fines up to $2.5 million under Australian Privacy Act

### 4.2 Threat: Data Breach/Data Leakage

**Threat Description:**
Unauthorized parties (external hackers or malicious insiders) gain access to the customer database and exfiltrate sensitive data.

**Attack Vectors:**
1. SQL injection through web application vulnerabilities
2. Compromised employee credentials (phishing or password reuse)
3. Insider threat - employee with legitimate access misuses data
4. Unsecured database backups on removable media
5. Network intrusion through unpatched systems

### 4.3 Vulnerabilities

1. **Weak Authentication:** Database only requires single-factor authentication (username + password)
2. **Unencrypted Storage:** Customer data stored in plaintext without encryption at rest
3. **Insufficient Access Controls:** Too many staff have full database access
4. **No Data Loss Prevention (DLP):** No monitoring for unusual data exports
5. **Lack of Encryption in Transit:** Data transmitted without TLS/SSL in some internal connections
6. **No Database Activity Monitoring:** No logging of who accesses what data

### 4.4 Risk Assessment

**Likelihood: High (4/5)**
- Cyber attacks targeting customer databases are common
- Weak authentication makes account compromise likely
- Multiple attack vectors available

**Impact: Critical (5/5)**
- Financial: Potential fines ($2.5M+), legal costs, customer compensation
- Reputational: Loss of customer trust, negative media coverage
- Operational: Loss of business, customer churn
- Legal: Privacy Act violations, potential lawsuits

**Risk Score:** 4 × 5 = **20 (CRITICAL)**

This is the highest-risk asset in our assessment.

## 5. Security Controls Recommendations

Based on the risk assessment, we recommend implementing three key security controls to protect the Customer Database (DA-001):

### 5.1 Control 1: Multi-Factor Authentication (MFA)

**Control Category:** Access Control (AC-2, AC-3, AC-7 from NIST SP800-53)

**Description:**
Implement multi-factor authentication for all access to the customer database, requiring users to provide two or more verification factors:
1. Something they know (password)
2. Something they have (smartphone app, hardware token)
3. Something they are (biometric - optional)

**How It Reduces Risk:**

This control directly addresses the "weak authentication" vulnerability:
- **Reduces likelihood:** Even if password is compromised (phishing, password reuse), attacker cannot access database without second factor
- **Mitigates insider threat:** Makes it harder for unauthorized staff to use stolen credentials
- **Provides audit trail:** MFA systems log all authentication attempts
- **Estimated risk reduction:** Likelihood reduced from High (4) to Low (2), reducing risk score from 20 to 10

**Implementation Details:**

**For Truelec's Network:**
1. **Database Server Level:**
   - Install Microsoft Authenticator or Google Authenticator integration
   - Require MFA for all SQL Server Management Studio connections
   - Configure Azure AD authentication (if using cloud) or Windows Hello for Business

2. **Application Level:**
   - Implement MFA in CRM and HR systems that access customer database
   - Use SAML/OAuth with MFA provider (Duo Security, Okta, or Microsoft Authenticator)

3. **VPN Access:**
   - Require MFA for all VPN connections from branches to headquarters
   - Configure on Fortinet FortiGate firewall using FortiToken

4. **Network Location:**
   - Implement on file servers (HW-005) where database backups are stored
   - Integrate with Active Directory and configure group policy

**Specific Technologies:**
- **Recommended Solution:** Microsoft Authenticator (free, integrates with Windows Server)
- **Hardware Tokens:** YubiKey for privileged users (ICT staff) - $50 per key
- **Cost:** Approximately $2,500 for initial setup + $50/user/year for licenses

**User Impact:**
- **Disadvantage:** Adds 10-15 seconds to login process
- **Disadvantage:** Users need smartphone or hardware token with them
- **Disadvantage:** Initial setup and user training required (1-2 hours per user)
- **Mitigation:** Provide clear training materials and support hotline during rollout

### 5.2 Control 2: Database Encryption (Encryption at Rest and in Transit)

**Control Category:** System and Communications Protection (SC-8, SC-13, SC-28 from NIST SP800-53)

**Description:**
Encrypt the customer database both "at rest" (when stored on disk) and "in transit" (when transmitted over the network).

**How It Reduces Risk:**

This control addresses the "unencrypted storage" and "lack of encryption in transit" vulnerabilities:
- **Reduces impact:** Even if attacker gains access to database files or intercepts network traffic, data is unreadable without encryption keys
- **Protects backups:** Backup tapes/drives are protected if physically stolen
- **Compliance:** Meets requirements of Privacy Act 1988 and ISO 27001
- **Estimated risk reduction:** Impact reduced from Critical (5) to High (4), reducing risk score from 20 to 16

**Implementation Details:**

**For Truelec's Network:**

1. **Encryption at Rest:**
   - Enable Transparent Data Encryption (TDE) on SQL Server
   - Encrypts database files, log files, and backups automatically
   - Configure on file servers (HW-005) where database is hosted

2. **Encryption in Transit:**
   - Enable TLS 1.3 for all database connections
   - Configure on Core Routers (HW-001, HW-002) and Distribution Switches (HW-003)
   - Force encrypted connections in SQL Server configuration

3. **Key Management:**
   - Use Windows Certificate Store or Azure Key Vault for encryption key management
   - Implement key rotation policy (every 90 days)
   - Store keys separately from encrypted data

4. **Network Segments:**
   - Apply encryption to all VLAN traffic carrying database queries
   - Configure on WiFi network - WPA3 already provides encryption
   - Ensure VPN tunnels to branches use AES-256 encryption

**Specific Technologies:**
- **SQL Server TDE:** Built into Windows Server (no additional cost)
- **TLS/SSL Certificates:** Let's Encrypt (free) or commercial certificate ($200/year)
- **Key Management:** Azure Key Vault ($0.03 per 10,000 operations) or Windows PKI (free)

**User Impact:**
- **Disadvantage:** Slight performance overhead (5-10% slower database queries)
- **Disadvantage:** Increased storage requirements (10% larger database files)
- **Minimal user-facing impact:** Encryption is transparent to end users
- **Mitigation:** Upgrade database server CPU/RAM if performance becomes issue

### 5.3 Control 3: Access Control and Monitoring (Least Privilege + Audit Logging)

**Control Category:** Audit and Accountability (AU-2, AU-3, AU-6, AU-12 from NIST SP800-53)

**Description:**
Implement strict access controls based on the principle of least privilege, combined with comprehensive logging and monitoring of all database access.

**How It Reduces Risk:**

This control addresses multiple vulnerabilities:
- **Insufficient access controls:** Only authorized users can access specific data they need
- **No database activity monitoring:** All access is logged and monitored for suspicious activity
- **Insider threats:** Unusual access patterns trigger alerts
- **Estimated risk reduction:** Likelihood reduced from High (4) to Medium (3) AND Impact reduced from Critical (5) to High (4), reducing risk score from 20 to 12

**Implementation Details:**

**For Truelec's Network:**

1. **Role-Based Access Control (RBAC):**
   - Create database roles: Read-Only, Accountant, HR-Admin, Project-Manager, DBA
   - Map employees to roles based on job function
   - Remove unnecessary admin privileges (currently too many staff have full access)

2. **Principle of Least Privilege:**
   - **Project Managers:** Read/write access only to their assigned projects
   - **Accounting Staff:** Read-only access to financial data, no customer contact data
   - **HR Staff:** Access to employee records only, no customer data
   - **ICT Staff:** Full admin access, but only for system maintenance

3. **Database Activity Monitoring:**
   - Enable SQL Server Audit to log all database operations
   - Track: Who accessed what data, when, from which IP address
   - Store audit logs on separate server (cannot be deleted by attacker)
   - Implement on file servers (HW-005)

4. **Alerting System:**
   - Configure alerts for suspicious activities:
     - Access outside business hours
     - Mass data exports (more than 1000 records)
     - Failed login attempts (more than 3 attempts)
     - Access from unusual locations (new IP addresses)
   - Send alerts to ICT staff email and SMS

5. **Regular Access Reviews:**
   - Quarterly review of user access rights
   - Disable accounts of terminated employees immediately
   - Implement automated workflow for access requests

**Network Integration:**
- **Distribution Switches (HW-003):** Configure port security to prevent rogue devices
- **Core Routers (HW-001, HW-002):** Implement access control lists (ACLs) restricting database server access
- **WiFi Network:** Separate SSIDs prevent guest/IoT devices from reaching database servers

**Specific Technologies:**
- **SQL Server Audit:** Built into SQL Server (free)
- **SIEM System:** Splunk Free (up to 500 MB/day) or paid version ($2,000/year)
- **Log Storage:** Additional 500 GB storage on file server or cloud ($10/month)

**User Impact:**
- **Disadvantage:** Users may request access to data they previously had but no longer need
- **Disadvantage:** Legitimate unusual access (e.g., working late) may trigger false alerts
- **Disadvantage:** Access request process adds delay (24-48 hours for approval)
- **Benefit:** Users appreciate knowing their data is protected
- **Mitigation:** Clearly communicate policy, provide fast-track approval for urgent needs

## 6. Summary of Security Controls

| Control | NIST Category | Risk Reduction | Implementation Cost | Ongoing Cost | Priority |
|---------|--------------|----------------|--------------------|--------------|---------| 
| Multi-Factor Authentication | AC-2, AC-7 | High to Low (20→10) | $2,500 | $50/user/year | **CRITICAL** |
| Database Encryption | SC-8, SC-28 | Critical to High Impact (5→4) | $200 | $200/year | **HIGH** |
| Access Control & Monitoring | AU-2, AU-6 | High to Medium (20→12) | $2,000 | $120/year | **HIGH** |

**Combined Effect:** 
Implementing all three controls together would reduce the Customer Database risk from **CRITICAL (score 20)** to approximately **LOW (score 6)**, calculated as:
- Likelihood: High (4) → Low (2) due to MFA and access controls
- Impact: Critical (5) → Medium (3) due to encryption and monitoring
- New Risk Score: 2 × 3 = 6 (LOW to MEDIUM)

This represents a **70% risk reduction**, making the customer database significantly more secure.

## 7. Additional Security Recommendations

While the above three controls address the highest-risk asset, we also recommend:

1. **Regular Security Awareness Training:** Reduce phishing susceptibility
2. **Patch Management Policy:** Address system vulnerabilities promptly
3. **Incident Response Plan:** Define procedures for responding to breaches
4. **Regular Backups:** Implement 3-2-1 backup strategy (3 copies, 2 media types, 1 offsite)
5. **Penetration Testing:** Annual third-party security assessment

## References

1. National Institute of Standards and Technology. (2020). NIST SP 800-53 Rev. 5: Security and Privacy Controls for Information Systems and Organizations.

2. Australian Government. (2023). Australian Privacy Principles. Office of the Australian Information Commissioner.

3. Microsoft. (2024). SQL Server Transparent Data Encryption (TDE). https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption

4. NIST. (2024). Multi-Factor Authentication Best Practices. https://www.nist.gov/

5. Australian Cyber Security Centre. (2024). Essential Eight Maturity Model. https://www.cyber.gov.au/