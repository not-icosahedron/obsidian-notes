## **Overview**
- **IAM** is a **global service** used to manage users, groups, and permissions in AWS.
- It allows you to control who can access your AWS resources and what actions they can perform.

---

## **Root User**
- When you create an AWS account, a **root user** is created by default.
- **Root User**:
  - Has full access to all AWS services and resources.
  - Should only be used for **initial account setup**.
  - **Best Practices**:
    - Do not use the root user for daily tasks.
    - Do not share the root user credentials.

---

## **IAM Users**
- **IAM Users** represent individual people within your organization.
- Each user has:
  - A unique username.
  - Security credentials (password, access keys).
- **Best Practices**:
  - Create individual IAM users for each person in your organization.
  - Assign permissions to users based on their roles.

---

## **IAM Groups**
- **Groups** are collections of IAM users.
- **Purpose**: Simplify permission management by assigning permissions to groups instead of individual users.
- **Key Points**:
  - Groups can only contain **users**, not other groups.
  - A user can belong to **multiple groups**.
  - Users do not have to belong to a group (though it’s not best practice).

---

### **Example: Organization with IAM Users and Groups**
- **Users**: Alice, Bob, Charles, David, Edward, Fred.
- **Groups**:
  - **Developers**: Alice, Bob, Charles.
  - **Operations**: David, Edward.
  - **Audit Team**: Charles, David.
- **Fred**: Does not belong to any group (not recommended).

---

## **IAM Policies**
- **Policies** are JSON documents that define permissions for users, groups, or roles.
- **Purpose**: Specify what actions are allowed or denied on which AWS resources.
- **Example Policy**:
  ```json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "ec2:Describe*",
          "elasticloadbalancing:Describe*",
          "cloudwatch:Describe*"
        ],
        "Resource": "*"
      }
    ]
  }