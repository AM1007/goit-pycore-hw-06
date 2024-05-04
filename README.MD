## Basic robotics with classes

> [!IMPORTANT] ☝ Our home robots will continue to develop our virtual assistant with a CLI interface.

Our assistant is already interacting with the client for the additional command line, removing commands, arguments, and other necessary actions. Whose assistant will need to learn about the internal logic of the assistant, how data is stored, what data itself is and what can be generated from it.

> [!IMPORTANT] ☝ We will add the logic itself to the bot in the upcoming home plant.

We will use object-oriented programming for these purposes. First, we will select several entities (models) with which we will work.

- The **user** will have an address book or a **contact book**. This **contact book** contains **entries**. Each **record** contains some set of **fields**.

In this way, we have described the entities (classes) that need to be implemented. Next, we will consider the requirements for these classes and establish their relationship, the rules by which they will interact.

- The user interacts with the **contact book** by adding, deleting and editing **entries**. Also, the user should be able to search for **entries in the contact book** by one or more criteria (fields).
- We can also say about the **fields** that they can be mandatory (name) and optional (phone or email, for example). Also, **records** can contain several **fields** of the same type (several phones, for example). User should be able to add/delete/edit **fields** in any record.

### Technical description of the task

Develop a system for managing the address book.

##### Essences:

- `Field`: Base class for record fields.
- `Name`: A class for storing the name of a contact. Mandatory field.
- `Phone`: A class for storing a phone number. Has format validation (10 digits).
- `Record`: A class for storing information about a contact, including name and phone list.
- `AddressBook`: A class for storing and managing records.

##### Functionality:

- `AddressBook`:Adding records.
- Search records by name.
- Deleting records by name.
- `Record`: Adding phones.
- Deleting phones.
- Editing phones.
- Phone search.

#### Recommendations for implementation:

As a start, you can take the following basic code to implement this homework:

```python
from collections import UserDict

class Field:
    def __init__(self, value):
        self.value = value

    def __str__(self):
        return str(self.value)

class Name(Field):
    # class implementation
		pass

class Phone(Field):
    # class implementation
		pass

class Record:
    def __init__(self, name):
        self.name = Name(name)
        self.phones = []

    # class implementation

    def __str__(self):
        return f"Contact name: {self.name.value}, phones: {'; '.join(p.value for p in self.phones)}"

class AddressBook(UserDict):
    # class implementation
		pass
```

Once implemented, your code should run as follows:

```python
# Creating a new address book
    book = AddressBook()

    # Create record for John
    john_record = Record("John")
    john_record.add_phone("1234567890")
    john_record.add_phone("5555555555")

    # Adding John to the address book
    book.add_record(john_record)

    # Create and add a new record for Jane
    jane_record = Record("Jane")
    jane_record.add_phone("9876543210")
    book.add_record(jane_record)

    # Output of all entries in the book
    for name, record in book.data.items():
        print(record)

    # Find and edit John's phone
    john = book.find("John")
    john.edit_phone("1234567890", "1112223333")

    print(john)  # Printing: Contact name: John, phones: 1112223333; 5555555555

    # Search for a specific phone in a John record
    found_phone = john.find_phone("5555555555")
    print(f"{john.name}: {found_phone}")  # Виведення: 5555555555

    # Printing record Jane
    book.delete("Jane")

```

In the next homework assignment, we will add this logic to our bot.

#### Evaluation criteria:

###### AddressBook class:

- Implemented the `add_record` method, which adds a record to `self.data`.
- Implemented the `find` method, which finds a record by name.
- Implemented the `delete` method, which deletes a record by name.

##### Record class:

- Storage of the `Name` object in a separate attribute has been implemented.
- Storage of the list of `Phone` objects in a separate attribute has been implemented.
- Implemented methods for adding - `add_phone/`deleting - `remove_phone/`editing - `edit_phone/`finding `Phone` objects - `find_phone`.

##### Phone class:

Validation of the phone number has been implemented (there must be a check for `10` digits).
