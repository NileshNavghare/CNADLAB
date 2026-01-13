Below are **updated THEORY notes** and **IMPORTANT POINTS TO REMEMBER** for **DynamoDB CRUD operations using Boto3**, written in a **clear, exam-oriented format**.

---

## 📘 THEORY: DynamoDB CRUD Operations using Boto3

Amazon **DynamoDB** is a **fully managed NoSQL key–value and document database** service provided by AWS. It offers **single-digit millisecond performance**, automatic scaling, and high availability.

**Boto3** is the official **AWS SDK for Python** that allows developers to interact with AWS services programmatically.

CRUD operations represent the four basic database operations:

* **Create** – Insert an item into the table
* **Read** – Retrieve an item using primary key
* **Update** – Modify existing item attributes
* **Delete** – Remove an item from the table

In DynamoDB, every operation is performed using the **primary key**, which can be:

* **Partition key only**, or
* **Partition key + Sort key**

---

## 🔹 CREATE (Insert Item)

* Performed using `put_item()`
* Inserts a new item or replaces an existing item with the same primary key
* Item must contain the primary key attribute

```python
table.put_item(Item={...})
```

---

## 🔹 READ (Get Item)

* Performed using `get_item()`
* Retrieves an item based on primary key
* If item does not exist, response will not contain `Item`

```python
table.get_item(Key={...})
```

---

## 🔹 UPDATE (Update Item)

* Performed using `update_item()`
* Updates one or more attributes without replacing the entire item
* Uses **UpdateExpression**

```python
UpdateExpression="SET attribute = :value"
```

---

## 🔹 DELETE (Delete Item)

* Performed using `delete_item()`
* Deletes an item using its primary key

```python
table.delete_item(Key={...})
```

---

## ⭐ IMPORTANT POINTS TO REMEMBER (Exam-Oriented)

### ✅ DynamoDB Basics

* DynamoDB is **schema-less** (except primary key)
* It is a **NoSQL** database
* Data is stored as **items** and **attributes**
* Tables are **region-specific**

---

### ✅ Keys & Indexes

* Primary key is **mandatory**
* Operations always require **primary key**
* Supports **Global Secondary Index (GSI)** and **Local Secondary Index (LSI)**

---

### ✅ Boto3 Concepts

* `boto3.resource('dynamodb')` → high-level interface
* `boto3.client('dynamodb')` → low-level interface
* `Table('TableName')` gives table object

---

### ✅ CRUD Operation Points

| Operation | Method          | Key Requirement      |
| --------- | --------------- | -------------------- |
| Create    | `put_item()`    | Primary key required |
| Read      | `get_item()`    | Primary key required |
| Update    | `update_item()` | Primary key required |
| Delete    | `delete_item()` | Primary key required |

---

### ✅ UpdateExpression Rules

* Must use placeholders (`:value`)
* Prevents injection issues
* Supports `SET`, `REMOVE`, `ADD`

---

### ✅ Capacity Modes

* **Provisioned** (RCU/WCU specified)
* **On-Demand** (auto scaling)

---

### ✅ Security & Access

* IAM permissions required:

  * `dynamodb:PutItem`
  * `dynamodb:GetItem`
  * `dynamodb:UpdateItem`
  * `dynamodb:DeleteItem`
* Credentials must be configured

---

## 📝 2-Mark / Viva Ready Points

* DynamoDB is serverless and fully managed
* CRUD operations are key-based
* Boto3 enables programmatic AWS access
* `put_item()` replaces item if key exists

---

---

## ✅ Key Improvements Made

* Removed global complexity
* Clear function names
* Single primary key (common in exams)
* Minimal error handling
* Clean menu-driven program
* Easy to modify and understand

---

## ✅ Simplified DynamoDB CRUD Program (Python + Boto3)

```python
import boto3

# Create DynamoDB resource
dynamodb = boto3.resource('dynamodb')

# Change table name as required
TABLE_NAME = "StudentTable"

table = dynamodb.Table(TABLE_NAME)

# CREATE (Insert Item)
def create_item():
    roll = input("Enter Roll No: ")
    name = input("Enter Name: ")
    marks = int(input("Enter Marks: "))

    table.put_item(
        Item={
            'RollNo': roll,
            'Name': name,
            'Marks': marks
        }
    )
    print("Item inserted successfully")

# READ (Get Item)
def read_item():
    roll = input("Enter Roll No: ")

    response = table.get_item(
        Key={'RollNo': roll}
    )

    if 'Item' in response:
        print("Item Found:", response['Item'])
    else:
        print("Item not found")

# UPDATE (Update Item)
def update_item():
    roll = input("Enter Roll No: ")
    new_marks = int(input("Enter new Marks: "))

    table.update_item(
        Key={'RollNo': roll},
        UpdateExpression="SET Marks = :m",
        ExpressionAttributeValues={
            ':m': new_marks
        }
    )
    print("Item updated successfully")

# DELETE (Delete Item)
def delete_item():
    roll = input("Enter Roll No: ")

    table.delete_item(
        Key={'RollNo': roll}
    )
    print("Item deleted successfully")

# MENU
def menu():
    while True:
        print("\n--- DynamoDB CRUD Menu ---")
        print("1. Insert Item")
        print("2. Get Item")
        print("3. Update Item")
        print("4. Delete Item")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == '1':
            create_item()
        elif choice == '2':
            read_item()
        elif choice == '3':
            update_item()
        elif choice == '4':
            delete_item()
        elif choice == '5':
            break
        else:
            print("Invalid choice")

# MAIN
if __name__ == "__main__":
    menu()
```

---

## ✅ DynamoDB Table Assumption (Important for Exam)

* **Table Name:** `StudentTable`
* **Primary Key:** `RollNo` (String)

---

## ✅ How to Explain in Viva (1–2 Lines Each)

* **Create:** `put_item()` inserts a new record
* **Read:** `get_item()` fetches data using primary key
* **Update:** `update_item()` modifies attributes
* **Delete:** `delete_item()` removes item using key

---


* **Marks-wise answer**
* **Serverless version**
* **Exception-free version**
* **Diagram + explanation**

Just tell me 👍
