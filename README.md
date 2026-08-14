# Customer_management

customers = []
customer_id = 1


# ---------- ADD CUSTOMER ----------
def add_customer():
    global customer_id

    try:
        print("\n========== ADD CUSTOMER ==========")

        name = input("Enter customer name: ").strip()
        phone = input("Enter phone number: ").strip()
        email = input("Enter email: ").strip()
        city = input("Enter city: ").strip()

        if name == "":
            print("Customer name cannot be empty!")
            return

        if phone == "":
            print("Phone number cannot be empty!")
            return

        # Check duplicate phone number
        for customer in customers:
            if customer["phone"] == phone:
                print("Customer with this phone number already exists!")
                return

        customer = {
            "id": customer_id,
            "name": name,
            "phone": phone,
            "email": email,
            "city": city
        }

        customers.append(customer)

        print("\nCustomer added successfully!")
        print("Customer ID:", customer_id)

        customer_id += 1

    except Exception as e:
        print("Error while adding customer:", e)


# ---------- VIEW CUSTOMERS ----------
def view_customers():
    try:
        print("\n========== ALL CUSTOMERS ==========")

        if len(customers) == 0:
            print("No customers available.")
            return

        print("-" * 85)
        print(f"{'ID':<5}{'Name':<20}{'Phone':<15}{'Email':<25}{'City':<15}")
        print("-" * 85)

        for customer in customers:
            print(
                f"{customer['id']:<5}"
                f"{customer['name']:<20}"
                f"{customer['phone']:<15}"
                f"{customer['email']:<25}"
                f"{customer['city']:<15}"
            )

        print("-" * 85)

    except Exception as e:
        print("Error while displaying customers:", e)


# ---------- SEARCH CUSTOMER ----------
def search_customer():
    try:
        print("\n========== SEARCH CUSTOMER ==========")

        search = input("Enter customer name or phone: ").strip().lower()

        if search == "":
            print("Please enter something to search.")
            return

        found = False

        for customer in customers:

            if (search in customer["name"].lower() or
                search in customer["phone"]):

                print("\nCustomer Found!")
                print("---------------------------")
                print("Customer ID :", customer["id"])
                print("Name        :", customer["name"])
                print("Phone       :", customer["phone"])
                print("Email       :", customer["email"])
                print("City        :", customer["city"])
                print("---------------------------")

                found = True

        if not found:
            print("Customer not found.")

    except Exception as e:
        print("Error while searching customer:", e)


# ---------- UPDATE CUSTOMER ----------
def update_customer():
    try:
        print("\n========== UPDATE CUSTOMER ==========")

        customer_id = int(input("Enter customer ID: "))

        found = False

        for customer in customers:

            if customer["id"] == customer_id:

                found = True

                print("\nCustomer Found!")
                print("Name :", customer["name"])
                print("Phone:", customer["phone"])
                print("Email:", customer["email"])
                print("City :", customer["city"])

                print("\nLeave blank if you don't want to change the value.")

                name = input("Enter new name: ").strip()
                phone = input("Enter new phone: ").strip()
                email = input("Enter new email: ").strip()
                city = input("Enter new city: ").strip()

                if name:
                    customer["name"] = name

                if phone:
                    customer["phone"] = phone

                if email:
                    customer["email"] = email

                if city:
                    customer["city"] = city

                print("\nCustomer updated successfully!")
                break

        if not found:
            print("Customer ID not found.")

    except ValueError:
        print("Please enter a valid numeric customer ID.")

    except Exception as e:
        print("Error while updating customer:", e)


# ---------- DELETE CUSTOMER ----------
def delete_customer():
    try:
        print("\n========== DELETE CUSTOMER ==========")

        customer_id = int(input("Enter customer ID: "))

        found = False

        for customer in customers:

            if customer["id"] == customer_id:

                found = True

                print("\nCustomer Found!")
                print("Name:", customer["name"])
                print("Phone:", customer["phone"])

                confirm = input(
                    "Are you sure you want to delete? (yes/no): "
                ).lower()

                if confirm == "yes":

                    customers.remove(customer)

                    print("Customer deleted successfully!")

                else:
                    print("Delete operation cancelled.")

                break

        if not found:
            print("Customer ID not found.")

    except ValueError:
        print("Please enter a valid numeric customer ID.")

    except Exception as e:
        print("Error while deleting customer:", e)


# ---------- MAIN PROGRAM ----------
def main():

    print("\n==========================================")
    print("       CUSTOMER MANAGEMENT SYSTEM")
    print("==========================================")

    while True:

        print("\n------------- MENU -------------")
        print("1. Add Customer")
        print("2. View Customers")
        print("3. Search Customer")
        print("4. Update Customer")
        print("5. Delete Customer")
        print("6. Exit")
        print("--------------------------------")

        try:

            choice = input("Enter your choice (1-6): ").strip()

            if choice == "1":
                add_customer()

            elif choice == "2":
                view_customers()

            elif choice == "3":
                search_customer()

            elif choice == "4":
                update_customer()

            elif choice == "5":
                delete_customer()

            elif choice == "6":
                print("\nThank you for using Customer Management System!")
                print("Program ended successfully.")
                break

            else:
                print("Invalid choice!")
                print("Please enter a number between 1 and 6.")

        except KeyboardInterrupt:
            print("\nProgram stopped by user.")
            break

        except Exception as e:
            print("Unexpected error:", e)


# ---------- RUN PROJECT ----------
main()
