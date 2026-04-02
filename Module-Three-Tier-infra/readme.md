# 🚀 Terraform CI/CD Pipeline using Jenkins

This project implements a **production-ready CI/CD pipeline** using **Jenkins** to deploy a **3-Tier Infrastructure on AWS** using **Terraform**.

---

## 📌 Overview

The pipeline automates:

* Infrastructure provisioning (VPC, EC2, ALB, RDS)
* Environment-based deployments (dev/test/prod)
* Safe execution using Terraform plan & apply workflow
* Optional manual approval for controlled environments

---

## 🏗️ Architecture

* **Terraform Modules**

  * VPC
  * Bastion Host
  * Frontend EC2
  * Backend EC2
  * Application Load Balancers
  * RDS Database

* **CI/CD Tool**

  * Jenkins (Declarative Pipeline)

* **Cloud Provider**

  * AWS

---

## 📂 Repository Structure

```
Module-Three-Tier-infra/
│
├── ROOT/
│   ├── modules/              
│   └── envs/
│       ├── dev/              
│       ├── test/
│       └── prod/
│
└── Jenkinsfile               
```

---

## ⚙️ Jenkins Pipeline Stages

| Stage                   | Description                    |
| ----------------------- | ------------------------------ |
| Checkout Code           | Clone repository               |
| Set Terraform Directory | Select environment dynamically |
| Verify Files            | Debug Terraform files          |
| Terraform Init          | Initialize Terraform           |
| Terraform Validate      | Validate config                |
| Terraform Plan          | Generate plan                  |
| Show Plan               | Display plan                   |
| Approval                | Manual approval (test/prod)    |
| Terraform Apply         | Apply changes                  |

---

## 🔄 Pipeline Workflow

```
Git Push → Jenkins → Init → Validate → Plan → Approval → Apply
```

---

# 🔐 AWS IAM Role Setup (VERY IMPORTANT)

Instead of using access keys, attach an **IAM Role to Jenkins EC2**.

---

## 🧱 Step 1: Create IAM Role

1. Go to AWS Console → IAM → Roles
2. Click **Create Role**
3. Select:

   * Trusted entity: **AWS Service**
   * Use case: **EC2**
4. Click Next

---

## 📜 Step 2: Attach Policies

### ✅ Option A: Quick Setup (POC)

Attach AWS managed policies:

* AmazonEC2FullAccess
* AmazonVPCFullAccess
* AmazonRDSFullAccess
* ElasticLoadBalancingFullAccess
* IAMFullAccess *(optional for testing)*

---

### ✅ Option B: Custom Policy (Recommended)

Create a policy:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "ec2:*",
        "rds:*",
        "elasticloadbalancing:*",
        "autoscaling:*",
        "cloudwatch:*",
        "logs:*",
        "iam:PassRole"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

Attach this policy to the role.

---

## 🔗 Step 3: Attach Role to Jenkins EC2

1. Go to EC2 → Instances
2. Select Jenkins instance
3. Actions → Security → **Modify IAM Role**
4. Attach the created role

---

## ✅ Step 4: Verify Access

SSH into Jenkins EC2:

```
aws sts get-caller-identity
```

You should see the IAM role ARN.

---

## ⚠️ Important Notes

* `iam:PassRole` is required for EC2/RDS creation
* Avoid using access keys in Jenkins
* Use least privilege in production

---

## ▶️ How to Run

1. Open Jenkins
2. Create Pipeline Job
3. Add repo:

```
https://github.com/aniljadhavmca/Module-Three-Tier-infra
```

4. Build with parameters
5. Select environment:

   * dev
   * test
   * prod

---

## 🧠 Key Features

* ✅ Environment-based deployment
* ✅ Safe Terraform workflow
* ✅ IAM Role-based authentication
* ✅ Manual approval support
* ✅ Scalable architecture

---

## ⚠️ Important Notes

* Terraform runs from:

```
ROOT/envs/<env>
```

* Each environment must contain:

```
main.tf
```

* Avoid `-target` in production

---

## 🔥 Recommended Enhancements

* 🌍 S3 backend + DynamoDB locking
* 🔐 Least privilege IAM policies
* 🔍 Security scanning (tfsec/checkov)
* 💰 Cost estimation (Infracost)

---

## 📌 Example Commands

```
terraform -chdir=ROOT/envs/dev plan -out=tfplan
terraform -chdir=ROOT/envs/dev apply tfplan
```

---

## 🎯 Future Improvements

* Multi-environment promotion
* Approval workflows
* Rollback strategies

---

## 🤝 Contributing

Feel free to contribute and improve!

---

## 📄 License

For learning and demonstration purposes.
