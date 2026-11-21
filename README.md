# Vantrel Health Inc. – PCI DSS & HIPAA Gap Analysis

## Governance, Risk & Compliance (GRC) Case Study

**Project Type:** Compliance Gap Analysis  
**Industry:** Healthcare / Telehealth  
**Frameworks:** PCI DSS v4.0.1 and HIPAA Security Rule  
**Assessment Type:** Initial, Scenario-Based Compliance Assessment  
**Role:** Junior Governance, Risk & Compliance (GRC) Analyst  
**Organisation:** Vantrel Health Inc.  

---

## 1. Project Overview

This project presents an initial Governance, Risk, and Compliance (GRC) gap analysis of **Vantrel Health Inc.**, a fictional healthcare technology company providing telehealth consultations and medical billing services to three healthcare clinics in the United States.

The assessment evaluates Vantrel's described security practices against two important compliance frameworks:

- **Payment Card Industry Data Security Standard (PCI DSS) v4.0.1**
- **Health Insurance Portability and Accountability Act (HIPAA) Security Rule**

Vantrel processes payment card information for telehealth services and handles electronic Protected Health Information (ePHI) on behalf of its U.S. healthcare clients. Consequently, the organisation must implement appropriate safeguards to protect payment card data and sensitive patient information.

The assessment identifies security and compliance gaps, maps them to relevant framework requirements, evaluates their potential business impact, and recommends corrective actions through a prioritised remediation plan.

The objective is to demonstrate how a GRC analyst can translate technical security weaknesses into compliance risks, business impacts, and actionable remediation strategies.

## 2. Business Scenario

Vantrel Health Inc. operates a telehealth platform and medical billing services for three U.S. clinics.

### Organisation Profile

| Category | Description |
|---|---|
| Organisation | Vantrel Health Inc. |
| Industry | Healthcare Technology / Telehealth |
| Employees | Approximately 150 |
| Headquarters | Toronto, Canada |
| Hosting Environment | Amazon Web Services (AWS) |
| Customers | Three U.S. healthcare clinics |
| Services | Telehealth consultations, appointment booking, and medical billing |
| Payment Processing | Online payment card transactions |
| Sensitive Information | Payment card data and electronic Protected Health Information (ePHI) |

### Technology Environment

The case study identifies the following systems and infrastructure:

- Web and mobile telehealth applications with integrated card checkout.
- Billing database containing payment-related information.
- Cloud-hosted patient-records database.
- AWS-hosted production environment.
- IT support vendor with remote server access.
- Production firewall.
- Antivirus software installed on company laptops.
- Employee password policy.
- Annual security awareness training.

### Business Drivers

Two significant business requirements are driving the compliance assessment:

1. A prospective U.S. hospital requires evidence of HIPAA compliance before establishing a business relationship.
2. The organisation's acquiring bank has requested PCI DSS validation.

These requirements make compliance readiness important to Vantrel's ability to establish and maintain business relationships.

---

## 3. Project Objectives

The primary objective is to identify gaps between Vantrel's current-state security practices and the applicable PCI DSS and HIPAA requirements.

The assessment focuses on:

1. Identifying the sensitive information handled by the organisation.
2. Determining which compliance frameworks apply to the information and services.
3. Identifying systems, employees, processes, and third parties that interact with sensitive information.
4. Evaluating the security weaknesses described in the case study.
5. Mapping identified gaps to relevant PCI DSS requirements and HIPAA Security Rule provisions.
6. Explaining the potential security, operational, financial, and compliance impacts.
7. Developing a prioritised remediation plan.
8. Establishing a preliminary compliance scope for both frameworks.

## 4. Compliance Frameworks Assessed

### 4.1 Payment Card Industry Data Security Standard (PCI DSS v4.0.1)

PCI DSS applies to organisations that store, process, or transmit payment account data, as well as systems that can affect the security of the cardholder data environment (CDE).

For Vantrel, the assessment focuses on protecting payment card information processed through its telehealth checkout and billing systems.

Key areas considered include:

- Protection of stored cardholder data.
- Prevention of prohibited sensitive authentication data retention.
- Strong authentication.
- Network security and segmentation.
- Service-provider management.
- Logging and monitoring.
- Incident response.

**Important finding:** Vantrel retains card verification values (CVV) after payment authorisation and stores primary account numbers (PAN) in plain text. These practices create significant PCI DSS compliance and payment-data security concerns.

### 4.2 Health Insurance Portability and Accountability Act (HIPAA)

HIPAA establishes requirements for protecting the privacy and security of protected health information handled by covered entities and their business associates.

In this scenario, Vantrel acts as a business associate because it handles PHI on behalf of the three U.S. healthcare clinics.

The assessment considers relevant administrative, physical, and technical safeguards, including:

- Security risk analysis.
- Access control.
- Person or entity authentication.
- Audit controls.
- Security incident procedures.
- Business Associate Agreements (BAAs).

**Important finding:** Vantrel has not completed a formal HIPAA risk analysis and has no Business Associate Agreements in place with the clinics or relevant vendors handling patient information.

---

## 5. Assessment Methodology

The assessment follows a data-first GRC approach.

### Step 1: Identify Sensitive Information

Determine what information Vantrel collects, stores, processes, and transmits.

The two primary information categories are:

| Information Type | Description | Applicable Framework |
|---|---|---|
| Cardholder Data | Primary Account Number (PAN) and related payment card information | PCI DSS |
| Sensitive Authentication Data | CVV/CVC and other sensitive authentication data | PCI DSS |
| Protected Health Information | Identifiable patient health information | HIPAA |
| Electronic Protected Health Information | PHI created, received, maintained, or transmitted electronically | HIPAA |

### Step 2: Identify Systems and Stakeholders

Determine which systems, employees, service providers, and business processes interact with sensitive information.

### Step 3: Evaluate Existing Security Controls

Review the security controls described in the scenario, including:

- Production firewall.
- Antivirus protection.
- Password policy.
- Annual security awareness training.
- Existing network architecture.
- Vendor remote access.
- Application logging and monitoring.

### Step 4: Identify Compliance Gaps

Compare the stated security practices against the relevant framework requirements.

### Step 5: Map Findings to Framework Requirements

Associate each finding with the applicable PCI DSS requirement and/or HIPAA Security Rule provision.

### Step 6: Evaluate Risk and Recommend Remediation

Prioritise corrective actions based on severity, exposure, and implementation sequence.

---

## 6. Detailed Gap Analysis

The assessment identifies five primary compliance gaps and two additional security weaknesses.

### Gap 1: Improper Storage of Payment Card Information

**Current State:**

Vantrel stores full Primary Account Numbers (PAN) in plain text and retains CVV values to support one-click repeat payments.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| PCI DSS | Requirement 3.3.1 | Prohibits storage of sensitive authentication data after authorisation. |
| PCI DSS | Requirement 3.5.1 | Requires stored PAN to be rendered unreadable. |

**Risk and Business Impact:**

- Exposure of usable payment card information following a database compromise.
- Increased likelihood of payment card fraud.
- Potential financial and contractual consequences.
- Failure to meet applicable PCI DSS requirements.

**Recommended Remediation:**

- Immediately eliminate stored CVV values.
- Prevent applications and databases from retaining CVV after authorisation.
- Work with the payment provider to implement tokenisation where appropriate.
- Protect any PAN that must remain stored using an approved approach.
- Review payment data flows to identify other locations where card information may be retained.

**Priority:** Critical

### Gap 2: Lack of Multi-Factor Authentication (MFA)

**Current State:**

MFA is not enforced for administrators or the IT support vendor's remote access.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| PCI DSS | Requirements 8.4.1–8.4.3 | MFA requirements for applicable access scenarios. |
| HIPAA | §164.312(d) | Person or entity authentication. |

**Risk and Business Impact:**

- Compromised passwords could provide unauthorised system access.
- Attackers could gain access to payment systems and patient information.
- Vendor remote access could become an entry point into sensitive environments.
- Increased likelihood of data breaches and operational disruption.

**Recommended Remediation:**

- Enforce MFA for privileged administrators.
- Apply MFA to applicable access paths into the cardholder data environment.
- Secure vendor remote access.
- Review privileged accounts and access permissions.
- Periodically review authentication configurations.

**Priority:** Critical

### Gap 3: Absence of a Formal HIPAA Security Risk Analysis

**Current State:**

Vantrel has never completed a formal HIPAA Security Rule risk analysis.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| HIPAA | §164.308(a)(1)(ii)(A) | Risk analysis implementation specification. |

**Risk and Business Impact:**

- Threats and vulnerabilities affecting ePHI may remain unidentified.
- Existing safeguards may not adequately address organisational risks.
- Security investments may not be prioritised according to actual exposure.
- Vantrel may be unable to demonstrate a documented, risk-based approach to protecting ePHI.

**Recommended Remediation:**

- Conduct a formal HIPAA Security Rule risk analysis.
- Identify systems, users, applications, and vendors that interact with ePHI.
- Document relevant threats and vulnerabilities.
- Evaluate existing safeguards.
- Determine and document risk levels.
- Develop a risk-treatment plan.
- Maintain evidence of remediation and periodic reassessment.

**Priority:** High

### Gap 4: Missing Business Associate Agreements (BAAs)

**Current State:**

Vantrel has no Business Associate Agreements in place with the U.S. clinics or vendors handling patient information.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| HIPAA | §164.308(b)(1) | Business associate contracts or other arrangements. |
| PCI DSS | Requirement 12.8 | Management of service providers that can affect account-data security. |

**Risk and Business Impact:**

- Missing contractual safeguards for PHI handling.
- Unclear responsibilities between Vantrel and its healthcare clients.
- Inadequate contractual oversight of vendors and subcontractors.
- Increased legal, regulatory, and business relationship risks.

**Recommended Remediation:**

- Execute appropriate BAAs with the U.S. healthcare clinics.
- Identify vendors that create, receive, maintain, or transmit PHI on Vantrel's behalf.
- Establish appropriate subcontractor business-associate agreements where required.
- Maintain a current vendor inventory.
- Implement a documented third-party risk management and oversight process.

**Priority:** High

### Gap 5: Flat Network Architecture

**Current State:**

The payment database shares a flat network with employee laptops and the Human Resources (HR) system.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| PCI DSS | Requirement 1.3 | Restricts network access to the cardholder data environment. |
| HIPAA | §164.312(a)(1) | Access control. |

**Risk and Business Impact:**

- A compromised employee workstation could create a pathway to the payment database.
- Unnecessary network connectivity increases attack surface.
- The PCI DSS assessment boundary may expand to connected systems.
- Sensitive patient and payment information may be exposed through insufficiently restricted network access.

**Recommended Remediation:**

- Design network segmentation between the CDE and corporate systems.
- Separate payment infrastructure from staff endpoints and HR systems.
- Apply appropriate firewall rules and access restrictions.
- Review network connectivity and remote-access pathways.
- Validate that implemented segmentation effectively isolates the CDE.

**Priority:** High

---

## 7. Additional Security Findings

In addition to the five primary gaps, the scenario identifies two further weaknesses that should be recorded in Vantrel's remediation register.

### 7.1 Weak Logging and Monitoring

**Current State:**

Application logs are retained for only 30 days and are not reviewed.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| PCI DSS | Requirement 10.4.1 | Daily log review. |
| PCI DSS | Requirement 10.5.1 | Log retention. |
| HIPAA | §164.312(b) | Audit controls. |

**Risk:**

Insufficient log retention and review can delay the identification of suspicious activity and make incident investigations more difficult.

**Recommended Remediation:**

- Establish appropriate log-retention periods.
- Conduct required daily reviews.
- Centralise relevant security logs.
- Implement monitoring and alert escalation.
- Restrict access to log data.
- Maintain evidence of log reviews.

### 7.2 Absence of a Documented Incident Response Plan

**Current State:**

Vantrel has no documented incident response or breach-notification procedure.

**Framework Mapping:**

| Framework | Requirement | Description |
|---|---|---|
| PCI DSS | Requirement 12.10.1 | Incident response plan. |
| HIPAA | §164.308(a)(6) | Security incident procedures. |
| HIPAA | Breach Notification Rule | Applicable breach-notification obligations. |

**Risk:**

- Delayed incident detection and containment.
- Unclear responsibilities during a security incident.
- Inadequate evidence preservation.
- Potential failure to meet applicable notification obligations.
- Increased operational and reputational damage.

**Recommended Remediation:**

- Develop and approve a documented incident response plan.
- Define incident classification and escalation procedures.
- Assign incident response responsibilities.
- Establish evidence preservation procedures.
- Document internal and external communication workflows.
- Include applicable breach-notification requirements.
- Conduct periodic incident response exercises.

---

## 8. Proposed Compliance Scope

### 8.1 PCI DSS Scope

PCI DSS scope covers Vantrel Health's card-payment environment, including:

- Web and mobile checkout applications.
- Billing database.
- AWS-hosted systems that store, process, or transmit payment account data.
- Systems connected to or capable of affecting the security of the CDE.
- Relevant employees, processes, and third-party service providers.
- Administrative and remote-access pathways into the payment environment.

### 8.2 HIPAA Scope

HIPAA scope covers all people, processes, systems, and vendors that create, receive, maintain, or transmit ePHI for Vantrel's U.S. clinic clients.

This includes:

- Patient-records cloud database.
- Appointment and billing services.
- Telehealth platform.
- Supporting AWS cloud environment.
- Employees with access to patient information.
- IT support vendors and relevant subcontractors.
- Administrative and remote-access pathways.

### Scope Validation Considerations

The exact compliance boundary must be confirmed through:

1. Data-flow mapping.
2. Asset inventory.
3. Network architecture diagrams.
4. User and access-path analysis.
5. Third-party vendor inventory.
6. Evidence demonstrating effective network segmentation.

A system should not be excluded from PCI DSS scope simply because it is labelled as a corporate or HR system.

---

## 9. Prioritised Remediation Roadmap

The following remediation roadmap translates the identified compliance weaknesses into actionable security improvements.

| Priority | Recommended Action | Framework | Target Timeline |
|---|---|---|---|
| 1 – Critical | Delete stored CVV values and prevent retention after authorisation. Protect or eliminate stored PAN through appropriate tokenisation and protection measures. | PCI DSS | Immediately (0–1 month) |
| 2 – Critical | Enforce MFA for privileged administrators and applicable access paths, including IT vendor remote access. | PCI DSS + HIPAA | Immediately (0–1 month) |
| 3 – High | Execute BAAs with the U.S. clinics and appropriate subcontractor/business-associate agreements with vendors handling ePHI. | HIPAA / PCI DSS | Phase 1 (0–3 months) |
| 4 – High | Conduct and document a formal HIPAA Security Rule risk analysis. | HIPAA | Phase 1 (0–3 months) |
| 5 – High | Implement and validate network segmentation between the CDE, staff endpoints, HR, and corporate networks. | PCI DSS / HIPAA | Phase 2 (3–6 months) |
| 6 – High | Improve log retention, daily review, monitoring, and alert escalation. | PCI DSS + HIPAA | Phase 2 (3–6 months) |
| 7 – High | Approve and test a documented incident response plan. | PCI DSS + HIPAA | Phase 2 (3–6 months) |

### Expected Remediation Outcomes

Successful implementation should help Vantrel:

- Eliminate prohibited storage of sensitive authentication data.
- Reduce exposure of payment card information.
- Strengthen identity and access management.
- Establish documented HIPAA risk management practices.
- Formalise business-associate and vendor responsibilities.
- Reduce unnecessary network connectivity.
- Improve security monitoring and auditability.
- Improve incident detection, containment, and response readiness.

---

## 10. Key GRC Observations

The assessment highlights several important GRC principles.

### 10.1 Compliance Must Be Driven by Data Classification

Different types of sensitive information trigger different regulatory and contractual obligations.

Payment card data is governed by PCI DSS, while ePHI handled for U.S. covered entities is governed by HIPAA.

Cardholder data should not automatically be classified as PHI without supporting facts.

### 10.2 Shared Controls Can Support Multiple Frameworks

Some security controls support both PCI DSS and HIPAA requirements.

Examples include:

- Multi-factor authentication.
- Access control.
- Audit logging.
- Vendor oversight.
- Incident response.
- Security risk management.

Designing shared controls consistently can reduce duplicated effort and help prevent compliance gaps.

### 10.3 Network Segmentation Requires Validation

Network segmentation can reduce the PCI DSS assessment boundary, but drawing a network diagram alone does not establish effective segmentation.

The organisation must demonstrate that the implemented controls restrict connectivity and protect the CDE.

### 10.4 Third-Party Risk Must Be Managed

Vantrel depends on external vendors and cloud-hosted infrastructure.

The organisation should identify third parties that can access sensitive environments or handle ePHI and establish appropriate contractual and security oversight.

### 10.5 Compliance Is an Ongoing Process

Compliance readiness requires more than implementing policies.

Organisations must establish accountable control owners, retain evidence, monitor control effectiveness, track remediation milestones, and periodically reassess risks.

---

## 11. Key Terms and Definitions

| Term | Definition |
|---|---|
| CDE | Cardholder Data Environment: people, processes, and systems that store, process, or transmit card data, plus connected systems that can affect its security. |
| CHD | Cardholder Data, including the Primary Account Number (PAN) and associated cardholder data elements. |
| SAD | Sensitive Authentication Data, such as CVV/CVC, PIN data, and full track/chip data. |
| PAN | Primary Account Number: the payment card number identifying the cardholder account. |
| PHI | Protected Health Information: identifiable health information. |
| ePHI | Electronic Protected Health Information: PHI created, received, maintained, or transmitted electronically. |
| Covered Entity | A health plan, healthcare clearinghouse, or qualifying healthcare provider conducting covered electronic transactions. |
| Business Associate | An organisation that creates, receives, maintains, or transmits PHI on behalf of a covered entity. |
| BAA | Business Associate Agreement: a written agreement establishing permitted uses and disclosures of PHI and required safeguards and responsibilities. |
| MFA | Multi-Factor Authentication: authentication using multiple factors to verify a user's identity. |
| Tokenisation | Replacing a card number with a substitute token so the underlying PAN is not stored in the merchant environment. |
| GRC | Governance, Risk, and Compliance: an integrated approach to organisational oversight, risk management, and regulatory compliance. |
| Gap Analysis | A structured assessment that identifies differences between existing practices and required controls or standards. |
| Remediation | Corrective action taken to address an identified security or compliance weakness. |

---

## 12. Project Deliverables

This case study demonstrates the following GRC assessment activities:

- PCI DSS v4.0.1 applicability assessment.
- HIPAA Security Rule applicability assessment.
- Sensitive data identification and classification.
- Initial compliance gap identification.
- Mapping of security findings to framework requirements.
- Risk and business impact analysis.
- Preliminary PCI DSS and HIPAA scope definition.
- Third-party and vendor risk considerations.
- Prioritised remediation planning.
- Security governance recommendations.

---

## 13. Assessment Limitations

This is an initial, scenario-based gap analysis based on the information provided in the case study.

The assessment did not include:

- Technical penetration testing.
- Vulnerability scanning.
- AWS configuration review.
- Firewall rule inspection.
- Database security testing.
- Access-control configuration review.
- Employee or vendor interviews.
- Independent evidence sampling.
- Formal PCI DSS assessment or HIPAA compliance validation.

Accordingly, the findings are preliminary and should be validated through a formal assessment supported by technical evidence, documentation, interviews, and control testing.

This report does not represent a PCI DSS certification, attestation, or independent confirmation of HIPAA compliance.

---

## 14. Conclusion

The Vantrel Health Inc. case study demonstrates how weaknesses in technical infrastructure, data protection, access management, vendor governance, and incident response can create significant compliance risks.

The most urgent findings involve the retention of CVV, plain-text storage of PAN, and the absence of MFA for privileged and vendor access.

Other important governance weaknesses include the absence of a formal HIPAA Security Risk Analysis, missing Business Associate Agreements, inadequate network segmentation, weak logging and monitoring, and the lack of a documented incident response plan.

A structured remediation programme will help Vantrel improve its security posture, strengthen regulatory readiness, protect sensitive information, and support future healthcare business relationships.

**The central GRC takeaway:** Effective compliance is not simply about satisfying regulatory requirements. It requires understanding how information flows through an organisation, identifying the risks associated with those flows, implementing appropriate controls, assigning accountability, and maintaining evidence that those controls operate effectively.

---

## 15. Skills Demonstrated

This project demonstrates practical knowledge and foundational skills in:

- Governance, Risk & Compliance (GRC).
- PCI DSS v4.0.1.
- HIPAA Security Rule.
- Security control gap analysis.
- Risk identification and assessment.
- Sensitive data classification.
- Compliance requirement mapping.
- Access control and MFA.
- Payment card data protection.
- Network segmentation.
- Third-party risk management.
- Business Associate Agreements.
- Security logging and monitoring.
- Incident response planning.
- Risk remediation and prioritisation.
- Compliance documentation and reporting.

---

## 16. Source Basis

This README is based on the supplied **Vantrel Health Inc. – PCI DSS & HIPAA Gap Analysis Submission**.

The original assessment was prepared as a scenario-based GRC case study using the supplied organisational facts, framework mappings, identified gaps, proposed compliance scope, and remediation guidance.

No external research or independent control validation was performed for the underlying submission.

---

**Disclaimer:** Vantrel Health Inc. is a fictional organisation used for educational and GRC portfolio purposes. This project is intended to demonstrate compliance assessment and risk-management concepts and should not be interpreted as legal advice or a formal compliance certification.
