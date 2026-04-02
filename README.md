# CI/CD and Jenkins Overview

## 🚀 What is CI/CD?
**CI/CD** is a modern development practice that automates the process of moving code from a developer's machine to a live environment.

*   **Continuous Integration (CI)**: Developers merge code changes into a shared repository frequently. Each "commit" triggers an **automated build and test** to catch bugs early.
*   **Continuous Delivery (CD)**: Automatically prepares code for release to staging or production after passing CI. It ensures the software is **always in a deployable state**.
*   **Continuous Deployment (CD)**: An advanced version where every change that passes all tests is **automatically pushed to production** without manual intervention.

## 🏗️ What is Jenkins?
**Jenkins** is an open-source **automation server** that acts as the "engine" for your CI/CD pipelines.

*   **Automation Hub**: Connects to your code (GitHub), runs build tools (Maven), and executes tests.
*   **Extensible**: Offers **1,800+ plugins** to integrate with tools like Docker, Kubernetes, and AWS.
*   **Pipeline as Code**: Workflows are defined in a simple text file called a **Jenkinsfile**.

## 📊 Summary Table


| Concept | Goal | Key Benefit |
| :--- | :--- | :--- |
| **CI** | Integrate and test code often | Finds bugs immediately |
| **CD** | Keep code ready for release | Reduces manual work |
| **Jenkins** | Automate the entire process | Faster, high-quality releases |

---
*Definitions for DevOps Practice & Documentation.*
