import os

FILE_NAME = "expenses.txt"

def add_expense():
    amount = input("Enter amount: ")
    category = input("Enter category (food, travel, etc): ")
    note = input("Enter note: ")

    with open(FILE_NAME, "a") as f:
        f.write(f"{amount},{category},{note}\n")

    print("✅ Expense added successfully!\n")


def view_expenses():
    if not os.path.exists(FILE_NAME):
        print("No expenses found.\n")
        return

    with open(FILE_NAME, "r") as f:
        for line in f:
            amount, category, note = line.strip().split(",")
            print(f"₹{amount} | {category} | {note}")
    print()


def total_expense():
    total = 0

    if not os.path.exists(FILE_NAME):
        print("No expenses found.\n")
        return

    with open(FILE_NAME, "r") as f:
        for line in f:
            amount, _, _ = line.strip().split(",")
            total += float(amount)

    print(f"💰 Total Expense: ₹{total}\n")


def category_summary():
    summary = {}

    if not os.path.exists(FILE_NAME):
        print("No expenses found.\n")
        return

    with open(FILE_NAME, "r") as f:
        for line in f:
            amount, category, _ = line.strip().split(",")
            amount = float(amount)

            if category in summary:
                summary[category] += amount
            else:
                summary[category] = amount

    print("📊 Category-wise Summary:")
    for cat, amt in summary.items():
        print(f"{cat}: ₹{amt}")
    print()


def menu():
    while True:
        print("==== Expense Tracker ====")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Total Expense")
        print("4. Category Summary")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_expense()
        elif choice == "2":
            view_expenses()
        elif choice == "3":
            total_expense()
        elif choice == "4":
            category_summary()
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice\n")


if __name__ == "__main__":
    menu()
