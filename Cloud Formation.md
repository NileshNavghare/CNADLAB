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

*End of file*
