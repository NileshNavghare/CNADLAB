I can help you **complete this CNAD Practical Exam answer properly** (ready for submission / viva), based on the PDF you uploaded .
Below is a **clean, exam-oriented solution** for **both topics**, with **steps + code + explanation**.

---

# **CNAD Practical Exam – Complete Solution**

**Name:** Prathamesh Shelke
**PRN:** 202201040037
**Class:** TY BTech

---

## **Topic 1: Launch EC2 Instance with Key Pair, Security Group (SSH/HTTP/HTTPS) using CloudFormation**

### **Objective**

To create:

* EC2 Instance
* Security Group allowing SSH (22), HTTP (80), HTTPS (443)
* Attach Security Group to EC2 using **AWS CloudFormation**

---

### **CloudFormation Template (YAML)**

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: EC2 Instance with Security Group allowing SSH, HTTP and HTTPS

Resources:

  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH, HTTP and HTTPS
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 443
          ToPort: 443
          CidrIp: 0.0.0.0/0

  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0a4408457f9a03be3   # Amazon Linux 2
      KeyName: mykeypair
      SecurityGroupIds:
        - !Ref MySecurityGroup
```

---

### **Steps to Execute**

1. Open **AWS CloudFormation Console**
2. Click **Create Stack → With new resources**
3. Upload the YAML template
4. Provide Stack Name
5. Click **Create Stack**
6. Verify:

   * Stack status → **CREATE_COMPLETE**
   * EC2 Instance created
   * Security Group attached

---

### **Output**

✔ Security Group created
✔ EC2 instance launched
✔ SSH/HTTP/HTTPS enabled
✔ Security Group attached to EC2

---

## **Topic 2: Create Lambda Function to Log S3 Bucket Details into CloudWatch**

### **Objective**

To:

* Create a Lambda function
* Trigger it using S3 events
* Log S3 event details into **CloudWatch Logs**

---

### **Steps**

#### **1. Create IAM Role for Lambda**

* Permissions:

  * `AWSLambdaBasicExecutionRole`
  * `AmazonS3ReadOnlyAccess`

---

#### **2. Create Lambda Function**

* Runtime: **Python 3.9**
* Execution Role: Created IAM role

---

#### **3. Add S3 Trigger**

* Select S3 bucket
* Event type: **Object Created (PUT)**

---

### **Lambda Function Code (Python)**

```python
import json

def lambda_handler(event, context):
    print("S3 Event Details:")
    print(json.dumps(event, indent=4))

    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        object_name = record['s3']['object']['key']
        print(f"Bucket Name: {bucket_name}")
        print(f"Object Name: {object_name}")

    return {
        'statusCode': 200,
        'body': 'S3 event logged successfully'
    }
```

---

### **4. Testing**

1. Upload a file to the S3 bucket
2. Open **CloudWatch → Log Groups**
3. View Lambda logs

---

### **Output**

✔ S3 event triggered Lambda
✔ Bucket name and object name logged
✔ Logs visible in CloudWatch

---

## **Conclusion**

* Successfully launched EC2 instance using **CloudFormation**
* Security Group created and attached properly
* Lambda function triggered by S3 events
* S3 details logged into CloudWatch

---

### ✅ **Exam Tip (Viva)**

If asked:

* **Why CloudFormation?**
  → Infrastructure as Code, repeatable & automated
* **Why Lambda?**
  → Serverless, event-driven, cost-effective
* **Why CloudWatch?**
  → Centralized logging and monitoring

---

If you want, I can also:

* Convert this into **handwritten-friendly format**
* Prepare **viva questions & answers**
* Shorten it to **2–3 pages exam write-up**
* Add **screenshots explanation captions**

Just tell me 👍
