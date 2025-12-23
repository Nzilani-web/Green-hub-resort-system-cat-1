
# Greenhub hotel system
# ABMI/00946/2023
# Faith Nzilani

class PaymentMethod:
    def make_payment(self, amount):
        pass

class CardPayment(PaymentMethod):
    def make_payment(self, amount):
        print(f"Paid KES {amount} using card.")

class MpesaPayment(PaymentMethod):
    def make_payment(self, amount):
        print(f"Paid KES {amount} using Mpesa.")

guest_bills = {}

class Service:
    def __init__(self, id, name, price):
        self.id = id
        self.name = name
        self.price = price

class HotelManagementSystem:
    def __init__(self):
        self.services = [
            Service(1, "Airport transfer", 3000),
            Service(2, "Spa and wellness", 5000),
            Service(3, "Accommodation service", 3500),
            Service(4, "Personal chef", 8500)
        ]
        self.guests = {}
        self.discount_policy = {1: 0.1, 2: 0.05, 3: 0.05}

    def add_guest(self):
        guest_id = input("Enter guest ID: ")
        name = input("Enter guest name: ")
        print("In select hotel service")
        print("1. Airport transfers (KES 3000 - 10% discount)")
        print("2. Spa & wellness (KES 5000 - 5% discount)")
        print("3. Accommodation service (KES 3500 - 5% discount)")
        print("4. Personal chef (KES 8500)")
        choice = input("Enter choice: ")
        if choice == "1":
            service = "Airport transfers"
            price = 3000
            discount_percentage = 10
        elif choice == "2":
            service = "Spa & wellness"
            price = 5000
            discount_percentage = 5
        elif choice == "3":
            service = "Accommodation service"
            price = 3500
            discount_percentage = 5
        elif choice == "4":
            service = "Personal chef"
            price = 8500
            discount_percentage = 0
        else:
            print("Invalid service choice!!")
            return
        total_cost = price - (price * discount_percentage / 100)
        print(f"Total cart amount: KES {total_cost}")
        print("In select payment method:")
        print("1. Card Payment")
        print("2. Mpesa")
        payment_choice = input("Enter payment method choice: ")
        if payment_choice == "1":
            CardPayment().make_payment(total_cost)
        elif payment_choice == "2":
            MpesaPayment().make_payment(total_cost)
        else:
            print("Invalid payment option")
        self.guests[guest_id] = {"name": name, "service": service, "total_cost": total_cost}

    def view_guests(self):
        print("Guests:")
        for guest_id, guest_info in self.guests.items():
            print(f"ID: {guest_id}, Name: {guest_info['name']}, Service: {guest_info['service']}, Total Cost: KES {guest_info['total_cost']}")

    def search_guest(self):
        guest_id = input("Enter guest ID: ")
        if guest_id in self.guests:
            guest_info = self.guests[guest_id]
            print(f"Name: {guest_info['name']}, Service: {guest_info['service']}, Total Cost: KES {guest_info['total_cost']}")
        else:
            print("Guest not found.")

    def update_guest(self):
        guest_id = input("Enter guest ID: ")
        if guest_id in self.guests:
            name = input("Enter new guest name: ")
            self.guests[guest_id]["name"] = name
            print("Guest updated successfully.")
        else:
            print("Guest not found.")

    def payment(self):
        guest_id = input("Enter guest ID: ")
        if guest_id in self.guests:
            guest_info = self.guests[guest_id]
            print(f"Total Cost: KES {guest_info['total_cost']}")
        else:
            print("Guest not found.")

    def main_menu(self):
        while True:
            print("In Green hub management system")
            print("1. Add new guest")
            print("2. View all guests")
            print("3. Search by guest ID")
            print("4. Update a guest")
            print("5. Check payment")
            print("6. Exit")
            choice = input("Select an option (1-6): ")
            if choice == "1":
                self.add_guest()
            elif choice == "2":
                self.view_guests()
            elif choice == "3":
                self.search_guest()
            elif choice == "4":
                self.update_guest()
            elif choice == "5":
                self.payment()
            elif choice == "6":
                print("Thank you!")
                break
            else:
                print("Invalid choice.")

# Example usage
hotel_system = HotelManagementSystem()
hotel_system.main_menu()
