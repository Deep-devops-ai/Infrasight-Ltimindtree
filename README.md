# 🚀 InfraSight Demo: Cost Optimization & Housekeeping Checks

## 📘 Overview
InfraSight is a cloud automation tool designed to optimize AWS infrastructure costs and perform routine housekeeping checks. This demo simulates real-world scenarios by provisioning sample resources and running scheduled evaluations via AWS Lambda.

---

## 🔧 Features

- **Toggleable Resource Creation**
  - EC2 instances (varied utilization)
  - RDS databases (low/high usage)
  - S3 buckets (with/without lifecycle policies)

- **Scheduled Lambda Execution**
  - Runs periodic checks (via EventBridge)
  - Evaluates resource efficiency and hygiene
  - Generates a report with actionable insights
  - Sends report via email or stores in S3

---

## 🔍 Checks Performed

| Category       | Checks                                                                 |
|----------------|------------------------------------------------------------------------|
| EC2            | Over-provisioned instances, Spot candidates                            |
| ASG            | Under-utilization                                                      |
| EBS            | gp2 → gp3 migration recommendation                                     |
| RDS            | Under-utilized databases                                               |
| S3             | Missing lifecycle policies                                             |
| IAM            | Unused access keys and roles                                           |
| Snapshots      | Orphaned snapshots                                                     |
| Target Groups  | Unused target groups                                                   |
| RI/SP          | Reserved Instance & Savings Plan recommendations                       |

---

## 📂 Output

- **Format**: JSON report
- **Contents**: Timestamped findings with optimization suggestions
- **Delivery**:
  - Stored in S3 bucket
  - Optionally emailed to stakeholders

---

## 🧪 How to Run

1. **Deploy Lambda Function**
   - Use AWS Console, SAM, or CloudFormation
   - Schedule via EventBridge (e.g., daily)

2. **Provision Sample Resources** *(optional)*
   - Use Terraform/CDK or manual setup

3. **Monitor Output**
   - Check S3 bucket or email inbox for reports

---

## 📄 Sample Report
```json
{
  "timestamp": "2025-11-04 12:35:00",
  "findings": [
    "EC2 i-001 is over-provisioned. Consider downsizing or using Spot instances.",
    "RDS rds-001 is under-utilized. Consider resizing or consolidating.",
    "S3 bucket demo-bucket is missing lifecycle policy.",
    "EBS volume vol-001 is gp2. Consider migrating to gp3 for cost savings.",
    "IAM user admin has unused access keys.",
    "ASG asg-001 is under-utilized. Desired: 5, Actual: 2.",
    "Snapshot snap-001 is orphaned. Consider deleting.",
    "Target Group tg-001 is unused.",
    "Consider Reserved Instances for EC2 i-001"
  ]
}
