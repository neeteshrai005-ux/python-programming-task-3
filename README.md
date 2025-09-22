# python-programming-task-3. import json

class ContactBook:
    def __init__(self, filename="contacts.json"):
        self.filename = filename
        self.contacts = self.load_contacts()

    def load_contacts(self):
        """Load contacts from a JSON file, if it exists."""
        try:
            with open(self.filename, "r") as file:
                return json.load(file)
        except FileNotFoundError:
            return []

    def save_contacts(self):
        """Save contacts to a JSON file."""
        with open(self.filename, "w") as file:
            json.dump(self.contacts, file, indent=4)

    def add_contact(self, name, phone, email):
        """Add a new contact to the list."""
        contact = {
            "name": name,
            "phone": phone,
            "email": email
        }
        self.contacts.append(contact)
        self.save_contacts()
        print(f"Contact {name} added successfully!")

    def show_contacts(self):
        """Display all the contacts in the contact book."""
        if not self.contacts:
            print("No contacts found.")
            return
        for idx, contact in enumerate(self.contacts, 1):
            print(f"{idx}. {contact['name']} - {contact['phone']} - {contact['email']}")

def main():
    contact_book = ContactBook()

    while True:
        print("\nContact Book")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            name = input("Enter contact name: ")
            phone = input("Enter phone number: ")
            email = input("Enter email address: ")
            contact_book.add_contact(name, phone, email)
        elif choice == "2":
            contact_book.show_contacts()
        elif choice == "3":
            print("Exiting contact book...")
            break
        else:
            print("Invalid choice, please try again.")

if __name__ == "__main__":
    main()
task 3
