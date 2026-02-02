# AWS CloudFormation: IAM Users and Group

## Overview
This Markdown file explains a simple AWS CloudFormation template that:
- Creates two IAM users
- Creates one IAM group
- Adds both users to the group

This example is suitable for labs, learning, and exam preparation.

---

## CloudFormation YAML Template

```yaml
AWSTemplateFormatVersion: '2010-09-09'
# Specifies the CloudFormation template format version

Description: >
  CloudFormation template to create two IAM users,
  one IAM group, and add both users to the group.
# Optional description of the template

Resources:
  # Mandatory section where AWS resources are defined

  MyIAMGroup:
    Type: AWS::IAM::Group
    # Defines an IAM Group

    Properties:
      GroupName: DevelopersGroup
      # Optional explicit name of the IAM group

  IAMUserOne:
    Type: AWS::IAM::User
    # Defines the first IAM user

    Properties:
      UserName: user-one
      # Optional username for first IAM user

  IAMUserTwo:
    Type: AWS::IAM::User
    # Defines the second IAM user

    Properties:
      UserName: user-two
      # Optional username for second IAM user

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
- Resources section
- Type for each resource
- GroupName and Users in AWS::IAM::UserToGroupAddition

### Optional (Recommended)
- AWSTemplateFormatVersion
- Description
- UserName
- GroupName
- Comments

---

## Key Takeaways
- Only Resources + Type + required properties are mandatory
- Naming and comments improve clarity but are not required

---

End of file
