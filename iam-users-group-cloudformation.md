# AWS CloudFormation: IAM Users and Group

## Overview

This CloudFormation template demonstrates how to:

* Create **two IAM users**
* Create **one IAM group**
* Add both users to the group

The example is kept simple and is suitable for **learning, labs, and exam preparation**.

---

## CloudFormation YAML Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
# Specifies the CloudFormation template version

Description: >
  CloudFormation template to create two IAM users,
  one IAM group, and add both users to the group.
# Human-readable description of the template

Resources:
  # Section where AWS resources are defined

  MyIAMGroup:
    Type: AWS::IAM::Group
    # Defines an IAM Group

    Properties:
      GroupName: DevelopersGroup
      # Name of the IAM Group

  IAMUserOne:
    Type: AWS::IAM::User
    # Defines the first IAM User

    Properties:
      UserName: user-one
      # Username for the first IAM user

  IAMUserTwo:
    Type: AWS::IAM::User
    # Defines the second IAM User

    Properties:
      UserName: user-two
      # Username for the second IAM user

  AddUsersToGroup:
    Type: AWS::IAM::UserToGroupAddition
    # Adds IAM users to an IAM group

    Properties:
      GroupName: !Ref MyIAMGroup
      # References the IAM group

      Users:
        - !Ref IAMUserOne
        # Adds first user to the group

        - !Ref IAMUserTwo
        # Adds second user to the group

  AttachManagedPolicyToGroup:
    Type: AWS::IAM::GroupPolicyAttachment
    # Attaches an AWS managed policy to the IAM group

    Properties:
      GroupName: !Ref MyIAMGroup
      # IAM group to which the policy is attached

      PolicyArn: arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
      # AWS managed policy ARN
```

---

## Compulsory vs Optional Elements

### Compulsory

* `Resources` section
* `Type` for each resource
* `GroupName` and `Users` in `AWS::IAM::UserToGroupAddition`

### Optional (Recommended)

* `AWSTemplateFormatVersion`
* `Description`
* `UserName`
* `GroupName`
* Comments (`#`)

---

## Key Takeaways

* CloudFormation requires only **Resources + Type + required properties**
* Naming and descriptions improve clarity but are **not mandatory**
* This template can be extended by attaching **IAM policies** to the group

---

## Next Steps (Optional Enhancements)

* Attach managed policies (e.g., `AmazonS3ReadOnlyAccess`)
* Create login passwords for IAM users
* Generate access keys
* Convert into an **exam-ready minimal template**

---

# AWS CloudFormation: IAM Users and Group – Detailed Explanation

## Introduction

AWS CloudFormation is an Infrastructure as Code (IaC) service that allows you to define and provision AWS resources using templates written in YAML or JSON. This document explains a CloudFormation template that creates two IAM users, one IAM group, and adds both users to that group, with a clear explanation of each section and line.

This example is suitable for:

* Beginners learning AWS IAM
* Academic labs and assignments
* Exam preparation (AWS, cloud computing courses)

---

## Purpose of the Template

The purpose of this CloudFormation template is to:

* Create IAM resources automatically
* Avoid manual user and group creation
* Demonstrate how users are grouped for permission management

---

## CloudFormation Template Structure

### AWSTemplateFormatVersion (Optional)

Specifies the CloudFormation template format version. It is optional but recommended for clarity and compatibility.

### Description (Optional)

Provides a human-readable explanation of what the template does. This helps others understand the intent of the template.

### Resources (Compulsory)

This is the most important section of any CloudFormation template. All AWS resources must be defined here.

---

## IAM Group Resource Explanation

The IAM group resource defines a logical grouping of IAM users. Permissions are usually attached to groups rather than individual users.

Key points:

* `Type` is compulsory
* `GroupName` is optional but recommended

---

## IAM User Resources Explanation

Two IAM users are created using the `AWS::IAM::User` resource type.

Key points:

* `Type` is compulsory
* `UserName` is optional but recommended for clarity

---

## Adding Users to the Group

The `AWS::IAM::UserToGroupAddition` resource is used to associate IAM users with an IAM group.

Key points:

* `GroupName` and `Users` properties are compulsory
* `!Ref` intrinsic function is used to avoid hardcoding names

---

## Compulsory vs Optional Elements Summary

### Compulsory

* Resources section
* Type for every resource
* Required properties defined by AWS

### Optional

* AWSTemplateFormatVersion
* Description
* UserName
* GroupName
* Comments

---

## Benefits of Using IAM Groups

* Simplified permission management
* Improved security
* Easy scalability

---

## Conclusion

This CloudFormation template demonstrates a clean and structured approach to managing IAM users and groups using Infrastructure as Code. It helps automate IAM setup, reduce configuration errors, and maintain consistency across AWS environments.

*End of file*
