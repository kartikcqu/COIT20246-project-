# COIT20246 Networking and Cyber Security Project

## Project Details

**Unit:** COIT20246 Networking and Cyber Security  
**Term:** 3, 2025  
**Project:** Network Design and Security Assessment for Truelec Electrical Contracting

## Group Members

| Name | Student ID | Email |
|------|-----------|-------|
| Kartik Trivedi | 12304142 | k.trivedi@cqu.edu.au |
| Kunjkumar Patel | 12314074 | k.patel3@cqu.edu.au |

## Project Timeline

**Start Date:** December 25, 2025  
**End Date:** January 9, 2026  
**Duration:** 15 days

## Project Submissions

### Part 1 - Network Design
- **Due Date:** Week 10
- **Status:** Complete
- **Submitted Files:** README.pdf, plan.pdf, network.pdf, repository.zip

### Part 2 - Cloud, Security, Ethics & Presentation
- **Due Date:** January 9, 2026
- **Status:** Complete
- **Submitted Files:** cloud.pdf, security.pdf, ethics.pdf, reflection.pdf, repository.zip, presentation.mp4

## Repository Structure

```
project/
├── README.md                      # Project overview
├── plan.md                        # Project plan and communication strategy
├── network.md                     # Network design documentation
├── cloud.md                       # Cloud services analysis
├── security.md                    # Security risk assessment
├── ethics.md                      # Ethical and social issues
├── reflection.md                  # Project reflection
├── diagrams/                      # Network diagrams
│   ├── headquarters-network.drawio
│   ├── headquarters-network.png
│   ├── branch-network.drawio
│   └── branch-network.png
├── risk-assessment/               # Security assessment files
│   ├── risk-assessment.xlsx
│   └── tva-matrix-screenshot.png
├── cloud-estimates/               # Cloud pricing exports
│   ├── aws-estimate.csv
│   └── azure-estimate.xlsx
├── reflection/                    # Reflection materials
│   └── git-commits-screenshot.png
└── presentation/                  # Video presentation
    └── presentation.mp4
```

## Key Design Assumptions

- **Headquarters Location:** Brisbane, Queensland
- **IP Addressing:** Primary addresses start with 42 (from Kartik's ID: 12304142)
- **Alternative IP Range:** 74.x.x.x available (from Kunjkumar's ID: 12314074)
- **Headquarters Staff:** 65 employees
- **Branch Offices:** Brisbane, Perth, Adelaide, Hobart
- **Branch Office Design:** Brisbane branch with 22 staff members

## Network Design Highlights

- **Headquarters:** Three-layer hierarchical design with dual core routers
- **Branch Office:** Two-layer simplified design with VPN to headquarters
- **WiFi:** WPA3-Enterprise with three SSIDs (Corporate, Guest, IoT)
- **Redundancy:** Dual ISPs, redundant core routers, multiple switches
- **Security:** Fortinet firewalls, encrypted VPN tunnels, segmented VLANs

## Cloud Recommendation

**Recommended Provider:** AWS (Amazon Web Services)
- **Cost Savings:** $27,400 over 5 years compared to on-premise
- **Service:** EC2 t3.xlarge instances in Sydney region
- **Justification:** Best cost-performance ratio, mature platform, Australian data centers

## Security Assessment

- **Threats Analyzed:** 8 of 12 standard information security threats
- **Highest Risk Asset:** Customer Database (Risk Score: 20 - CRITICAL)
- **Top Security Controls:**
  1. Multi-Factor Authentication (MFA)
  2. Database Encryption (at rest and in transit)
  3. Access Control and Monitoring (RBAC + audit logging)

## Important Links

- [CQU Moodle - COIT20246](https://moodle.cqu.edu.au)
- [Draw.io Diagram Editor](https://app.diagrams.net/)
- [AWS Pricing Calculator](https://calculator.aws/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

## Commit Guidelines Compliance

✅ Both group members committed regularly throughout project  
✅ Minimum 1 commit per day worked  
✅ Commits made by person who did the work  
✅ Meaningful commit messages  
✅ Frequent commits across all 3 weeks (not just before deadline)

## Academic Integrity Statement

This project represents our own original work completed for COIT20246. All external sources, including AI tools, websites, and technical documentation, have been properly referenced. We have followed CQU's academic integrity policies throughout this project.

**Date Completed:** January 8, 2026  
**Submitted:** January 9, 2026

---

**For questions or issues, contact:**
- Kartik Trivedi: k.trivedi@cqu.edu.au
- Kunjkumar Patel: k.patel3@cqu.edu.au