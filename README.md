

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
