# Understanding AWS IAM — Your Key to Secure Cloud Access

A plain-English breakdown of AWS Identity and Access Management, plus three example least-privilege policies ([`policies/`](./policies)) for a typical web application setup.

> 📖 Full write-up: [Understanding AWS IAM: Your Key to Secure Cloud Access](https://www.linkedin.com/pulse/understanding-aws-iam-your-key-secure-cloud-access-gaurav-khatri-owm0c/) by **Gaurav Khatri**

## What is IAM?

Think of IAM as the security guard and key system for your AWS account — just like you wouldn't give everyone in an office the master key to every room, IAM makes sure people and services only access what they actually need.

## The core components

| Component | What it is |
|---|---|
| **Users** | Individual people or applications, each with unique credentials |
| **Groups** | Collections of users — assign permissions once, to the group, instead of per person |
| **Roles** | Temporary permissions a user or service can assume — like borrowing an access card for a specific task |
| **Policies** | JSON rules that define what actions are allowed or denied; attached to users, groups, or roles |

## A real-world example

Running a web application on AWS, three different needs, three different scopes — instead of giving everyone admin access:

| Who | Needs access to | Example policy |
|---|---|---|
| Developers | EC2 instances + CloudWatch logs | [`developers-group-policy.json`](./policies/developers-group-policy.json) |
| Database admins | RDS only (scoped by tag) | [`dbadmins-group-policy.json`](./policies/dbadmins-group-policy.json) |
| EC2 application role | Read-only access to one S3 bucket | [`ec2-s3-read-role-policy.json`](./policies/ec2-s3-read-role-policy.json) |

None of these grant broad `*:*` admin access — each is scoped to exactly what that group or role needs.

## Best practices

- **Principle of least privilege** — give only the minimum permissions needed; you can always add more later
- **Enable MFA** — an extra security layer, like requiring both a password and a fingerprint
- **Use roles for applications** — never hardcode credentials in application code; use IAM roles instead
- **Regular audits** — periodically review who has access to what, and remove permissions no longer needed

## Getting started

Start simple: create a few test users, experiment with different policies, and gradually build understanding. AWS's managed policies for common use cases are a good way to learn the shape of a well-scoped policy before writing your own.

---

**Author:** [Gaurav Khatri](https://www.linkedin.com/in/gaurav-khatri-devops/) — DevOps Engineer @ Sarv.com | Kubernetes (EKS), Docker, GitOps & CI/CD
