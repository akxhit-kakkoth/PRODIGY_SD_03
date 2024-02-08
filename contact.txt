import json

class ContactManager:
    def __init__(self):
        self.contacts = []

    def add_contact(self, name, phone, email):
        contact = {"name": name, "phone": phone, "email": email}
        self.contacts.append(contact)
        print(f"Contact added: {name}")

    def view_contacts(self):
        if not self.contacts:
            print("No contacts found.")
        else:
            print("Contact List:")
            for i, contact in enumerate(self.contacts, 1):
                print(f"{i}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

    def edit_contact(self, index, name, phone, email):
        if 0 < index <= len(self.contacts):
            self.contacts[index - 1] = {"name": name, "phone": phone, "email": email}
            print("Contact updated successfully.")
        else:
            print("Invalid contact index.")

    def delete_contact(self, index):
        if 0 < index <= len(self.contacts):
            deleted_contact = self.contacts.pop(index - 1)
            print(f"Contact deleted: {deleted_contact['name']}")
        else:
            print("Invalid contact index.")

    def save_to_file(self, filename):
        with open(filename, 'w') as file:
            json.dump(self.contacts, file)
            print(f"Contacts saved to {filename}.")

    def load_from_file(self, filename):
        try:
            with open(filename, 'r') as file:
                self.contacts = json.load(file)
                print(f"Contacts loaded from {filename}.")
        except FileNotFoundError:
            print("No existing contacts file found.")

# Example usage of ContactManager
contact_manager = ContactManager()

while True:
    print("\nContact Management System:")
    print("1. Add Contact")
    print("2. View Contacts")
    print("3. Edit Contact")
    print("4. Delete Contact")
    print("5. Save Contacts to File")
    print("6. Load Contacts from File")

    choice = input("Enter your choice (1-6): ")

    if choice == '1':
        name = input("Enter the name: ")
        phone = input("Enter the phone number: ")
        email = input("Enter the email address: ")
        contact_manager.add_contact(name, phone, email)
    elif choice == '2':
        contact_manager.view_contacts()
    elif choice == '3':
        index = int(input("Enter the index of the contact to edit: "))
        name = input("Enter the new name: ")
        phone = input("Enter the new phone number: ")
        email = input("Enter the new email address: ")
        contact_manager.edit_contact(index, name, phone, email)
    elif choice == '4':
        index = int(input("Enter the index of the contact to delete: "))
        contact_manager.delete_contact(index)
    elif choice == '5':
        filename = input("Enter the filename to save contacts: ")
        contact_manager.save_to_file(filename)
    elif choice == '6':
        filename = input("Enter the filename to load contacts from: ")
        contact_manager.load_from_file(filename)
    else:
        print("Invalid choice. Please enter a number between 1 and 6.")
