# Cloud Services Analysis

## 1. Current Situation

Truelec currently operates:
- **Headquarters:** 3 Dell PowerEdge Tower Servers (5 years old)
- **Perth Branch:** 1 Dell PowerEdge Tower Server (5 years old)
- **Adelaide Branch:** 1 Dell PowerEdge Tower Server (5 years old)
- **Hobart Branch:** 1 Dell PowerEdge Tower Server (5 years old)
- **Melbourne Branch:** 1 Dell PowerEdge Tower Server (5 years old)

**Total:** 7 servers running the booking application

These servers are reaching end-of-life and need replacement. The company is considering either:
1. Purchasing new Dell PowerEdge servers, or
2. Migrating to cloud virtual machines (VMs)

## 2. Server Requirements Analysis

### 2.1 Application Requirements

Based on the booking application needs:
- **Operating System:** Windows Server 2022
- **CPU:** 4 vCPUs minimum (for application processing)
- **RAM:** 16 GB (to handle concurrent bookings)
- **Storage:** 500 GB (for application, database, and logs)
- **Backup:** 500 GB additional storage for daily backups
- **Operating Hours:** 24/7 availability
- **Redundancy:** High availability required

### 2.2 Server Specifications - Standardized

To ensure fair comparison, we use identical specifications across all cloud providers:

| Specification | Value | Justification |
|---------------|-------|---------------|
| **Region** | Australia (Sydney/Melbourne) | Low latency for Australian users, data sovereignty compliance |
| **Operating System** | Windows Server 2022 | Booking app requires Windows Server |
| **vCPUs** | 4 vCPUs | Adequate for booking application processing |
| **RAM** | 16 GB | Sufficient for application and database |
| **Primary Storage** | 500 GB SSD (Premium) | Fast storage for application performance |
| **Backup Storage** | 500 GB Standard | Daily backups, slower storage acceptable |
| **Data Transfer** | 1 TB/month outbound | Estimated based on booking transactions |
| **Operating Hours** | 730 hours/month (24/7) | Continuous availability required |
| **License** | Windows license included | Simplifies management |

**Region Justification:** Sydney/Melbourne regions selected for:
- Lowest latency for Australian users
- Compliance with Australian data protection laws
- Local support and faster incident response

## 3. Cloud Provider Comparison

### 3.1 AWS (Amazon Web Services) - Pricing

**Service:** Amazon EC2 - t3.xlarge instance

**Monthly Cost Breakdown:**

| Component | Specification | Monthly Cost (AUD) |
|-----------|--------------|-------------------|
| Compute (EC2 instance) | t3.xlarge (4 vCPU, 16 GB RAM) - 730 hrs | $182.50 |
| Primary Storage (EBS) | 500 GB gp3 SSD | $65.00 |
| Backup Storage (S3) | 500 GB Standard | $15.00 |
| Data Transfer Out | 1 TB/month | $122.00 |
| Windows Server License | Included in EC2 pricing | $0.00 |

**Total Monthly Cost per VM:** $384.50 AUD  
**Total Annual Cost per VM:** $4,614.00 AUD

**AWS Pricing Export:** [aws-estimate.csv](cloud-estimates/aws-estimate.csv)

**AWS Calculator Link:** https://calculator.aws/#/

### 3.2 Microsoft Azure - Pricing

**Service:** Azure Virtual Machine - Standard_D4s_v5

**Monthly Cost Breakdown:**

| Component | Specification | Monthly Cost (AUD) |
|-----------|--------------|-------------------|
| Compute (VM) | Standard_D4s_v5 (4 vCPU, 16 GB RAM) - 730 hrs | $295.20 |
| Primary Storage | 500 GB Premium SSD | $78.00 |
| Backup Storage | 500 GB Standard Blob | $12.50 |
| Data Transfer Out | 1 TB/month | $118.00 |
| Windows Server License | Included in VM pricing | $0.00 |

**Total Monthly Cost per VM:** $503.70 AUD  
**Total Annual Cost per VM:** $6,044.40 AUD

**Azure Pricing Export:** [azure-estimate.xlsx](cloud-estimates/azure-estimate.xlsx)

**Azure Calculator Link:** https://azure.microsoft.com/en-us/pricing/calculator/

### 3.3 Pricing Comparison Summary

| Cloud Provider | Monthly Cost/VM | Annual Cost/VM | 5-Year Cost/VM |
|----------------|-----------------|----------------|----------------|
| **AWS** | $384.50 | $4,614.00 | $23,070.00 |
| **Azure** | $503.70 | $6,044.40 | $30,222.00 |
| **Difference** | AWS is $119.20 cheaper/month | AWS is $1,430.40 cheaper/year | AWS is $7,152.00 cheaper over 5 years |

## 4. Total Cost of Cloud Migration

### 4.1 Five-Year Cloud Costs

Based on 7 servers total (3 HQ + 4 branches):

| Provider | Cost per VM (5 years) | Total for 7 VMs (5 years) |
|----------|----------------------|--------------------------|
| **AWS** | $23,070.00 | $161,490.00 |
| **Azure** | $30,222.00 | $211,554.00 |

**Cost Difference:** AWS is $50,064 cheaper than Azure over 5 years for 7 VMs.

### 4.2 On-Premise Alternative - New Server Purchase

**New Dell PowerEdge Tower Server Specifications:**
- Model: Dell PowerEdge T550
- CPU: Intel Xeon Silver 4310 (12 cores, 2.1 GHz)
- RAM: 32 GB DDR4 (upgradable to 128 GB)
- Storage: 2x 1TB SSD (RAID 1 for redundancy)
- Redundant Power Supply: Yes
- Price per server: $6,500 AUD (approximate from Dell Australia)

**Five-Year On-Premise Costs:**

| Cost Component | Calculation | Total Cost (AUD) |
|----------------|-------------|------------------|
| **Initial Hardware** | 7 servers × $6,500 | $45,500 |
| **Power Consumption** | 7 servers × 400W × 24 hrs × 365 days × 5 years × $0.25/kWh | $30,660 |
| **Cooling (estimate)** | Power × 0.5 (50% of power consumption) | $15,330 |
| **Windows Server Licenses** | 7 servers × $1,200 (one-time) | $8,400 |
| **Maintenance/Support** | $800/server/year × 7 servers × 5 years | $28,000 |
| **Physical Space** | Rack space rental (if applicable): $100/month × 60 months | $6,000 |
| **UPS/Backup Power** | 2 UPS units × $2,000 | $4,000 |
| **Network Equipment** | Additional switches, cabling | $3,000 |
| **IT Staff Time** | Hardware maintenance - 10 hrs/month × $80/hr × 60 months | $48,000 |

**Total 5-Year On-Premise Cost:** $188,890 AUD

### 4.3 Cost Comparison - Cloud vs On-Premise

| Solution | 5-Year Total Cost | Cost per Server | Savings vs On-Premise |
|----------|------------------|-----------------|----------------------|
| **AWS Cloud** | $161,490 | $23,070 | $27,400 (14.5% cheaper) |
| **Azure Cloud** | $211,554 | $30,222 | -$22,664 (12% more expensive) |
| **On-Premise** | $188,890 | $26,984 | Baseline |

**Winner:** AWS is the most cost-effective option, saving $27,400 over 5 years compared to on-premise.

## 5. Advantages and Disadvantages Analysis

### 5.1 Advantages of Cloud VMs

#### Financial Advantages
1. **Lower upfront capital expenditure:** No large hardware purchase required ($45,500 saved initially)
2. **Predictable monthly costs:** OpEx model makes budgeting easier
3. **No maintenance costs:** Hardware failures covered by cloud provider
4. **No power/cooling costs:** Included in cloud pricing

#### Technical Advantages
1. **Scalability:** Easy to add more servers or increase resources as business grows
2. **High availability:** Cloud providers offer 99.95-99.99% uptime SLAs
3. **Disaster recovery:** Built-in backup and recovery options
4. **Automatic updates:** Managed patches and security updates (if using managed services)
5. **Global reach:** Can deploy closer to branch locations if needed
6. **Redundancy:** Cloud VMs run on redundant infrastructure
7. **Quick deployment:** New VMs can be provisioned in minutes

#### Operational Advantages
1. **Reduced IT burden:** Less hardware management, more focus on applications
2. **Remote management:** Full control from anywhere with internet
3. **Better security:** Cloud providers invest heavily in physical and network security
4. **Compliance certifications:** AWS/Azure have ISO 27001, SOC 2, and other certifications

### 5.2 Disadvantages of Cloud VMs

#### Financial Disadvantages
1. **Ongoing costs:** Monthly payments continue indefinitely (no asset ownership)
2. **Cost unpredictability:** Unexpected usage spikes increase costs
3. **Data egress charges:** High data transfer costs if usage increases
4. **Currency fluctuation:** Prices in USD, exposed to exchange rate changes

#### Technical Disadvantages
1. **Internet dependency:** Requires reliable internet connection
2. **Latency:** Slightly higher latency compared to local servers (though minimal with Sydney region)
3. **Limited customization:** Cannot modify hardware or physical infrastructure
4. **Vendor lock-in:** Difficult to migrate away once fully committed

#### Operational Disadvantages
1. **Learning curve:** Staff need training on cloud management
2. **Security concerns:** Data stored off-premise (though mitigated by encryption)
3. **Compliance complexity:** Must ensure cloud provider meets regulatory requirements
4. **Less control:** Dependent on cloud provider's infrastructure and policies

### 5.3 Advantages of On-Premise Servers

1. **Full control:** Complete control over hardware and software
2. **No internet dependency:** Local access even during internet outages
3. **One-time purchase:** After 5 years, servers can continue operating with minimal cost
4. **Data sovereignty:** Complete control over data location
5. **Lower long-term cost:** If servers last beyond 5 years, overall cost decreases

### 5.4 Disadvantages of On-Premise Servers

1. **High upfront cost:** $45,500 initial investment required
2. **Maintenance burden:** IT staff must manage hardware failures, updates, patches
3. **Limited scalability:** Requires purchasing new hardware to scale
4. **Physical space required:** Need dedicated server room with cooling and power
5. **Disaster recovery:** Requires separate backup infrastructure and strategy
6. **Hardware obsolescence:** Servers become outdated, requiring replacement
7. **Power/cooling costs:** Ongoing electricity expenses
8. **Single point of failure:** Hardware failure causes downtime unless redundancy is built in

## 6. Recommendation

### 6.1 Recommended Cloud Provider: **AWS**

We recommend **AWS** for the following reasons:

1. **Cost-effectiveness:** AWS is $27,400 cheaper than on-premise and $50,064 cheaper than Azure over 5 years

2. **Mature platform:** AWS has been operating longer than other cloud providers and has proven reliability

3. **Australian presence:** Strong presence in Sydney region with low latency to all Truelec locations

4. **Comprehensive services:** Wide range of additional services (databases, AI/ML, analytics) if Truelec wants to expand

5. **Market leader:** Largest cloud provider with extensive documentation and community support

6. **Flexible pricing:** Reserved instances or savings plans can reduce costs further (up to 30-40% additional savings)

7. **Better performance:** t3 instances offer good balance of performance and cost

### 6.2 Implementation Strategy

**Phase 1 - Pilot (Months 1-2):**
- Migrate one branch office server to AWS
- Test performance, connectivity, and user experience
- Train IT staff on AWS management

**Phase 2 - Branch Migration (Months 3-4):**
- Migrate remaining branch offices
- Establish site-to-site VPN connections to AWS
- Monitor performance and costs

**Phase 3 - Headquarters Migration (Months 5-6):**
- Migrate headquarters servers to AWS
- Implement high-availability configuration
- Complete documentation and training

### 6.3 Additional Considerations

**Cost Optimization:**
- Use AWS Reserved Instances for 1-3 year commitments to save 30-40% on compute costs
- Implement auto-scaling to scale down during off-peak hours (if applicable)
- Use AWS Cost Explorer to monitor and optimize spending

**Security:**
- Implement AWS security best practices (IAM, Security Groups, encryption)
- Enable CloudTrail for audit logging
- Use AWS Backup for automated backups

**Hybrid Option:**
- Consider keeping headquarters servers on-premise initially while moving branches to cloud
- This provides fallback option and allows gradual migration

## 7. Conclusion

Based on our analysis, **AWS cloud VMs** provide the best value for Truelec's booking application servers. The cloud migration will save $27,400 over 5 years compared to purchasing new on-premise servers, while providing better scalability, reliability, and reduced management burden for IT staff.

The cloud approach aligns with modern IT best practices and positions Truelec for future growth without significant capital investment in hardware infrastructure.

## References

1. AWS. (2024). AWS Pricing Calculator. https://calculator.aws/
2. Microsoft Azure. (2024). Azure Pricing Calculator. https://azure.microsoft.com/en-us/pricing/calculator/
3. Dell Technologies. (2024). Dell PowerEdge T550 Specifications. https://www.dell.com/
4. AWS. (2024). Amazon EC2 Pricing. https://aws.amazon.com/ec2/pricing/
5. Gartner. (2024). Magic Quadrant for Cloud Infrastructure and Platform Services.