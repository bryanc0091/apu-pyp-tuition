import os
import datetime

#forms is used by admin and receptionist
forms = {
    "1" : [
        'Bahasa Melayu',
        'English',
        'Mathematics',
        'Science'
    ],
    "2" : [
        'Bahasa Melayu',
        'English',
        'Mathematics',
        'Science'
    ],
    "3" : [
        'Bahasa Melayu',
        'English',
        'Mathematics',
        'Science'
    ],
    "4" : [
        'Bahasa Melayu',
        'English',
        'Mathematics',
        'Science',
        'Add Maths',
        'Economics',
        'Accounting'
    ],
    "5" : [
        'Bahasa Melayu',
        'English',
        'Mathematics',
        'Science',
        'Add Maths',
        'Economics',
        'Accounting'
    ]
}



#admin's code

def login():
    attempts = 0
    content = []
    while attempts < 3:
        username = input('Enter your username: ')
        password = input('Enter your password: ')

        file_list = ['users.txt', 'tutors.txt', 'receptionist.txt']
        for file in file_list:
            with open(file, "r") as f:
                for line in f:
                    content.append(line.strip().split(","))

        for user_info in content:
            if username == user_info[0] and password == user_info[1]:
                print('Login successful!')
                menu()
                attempts = 4
                break

        if attempts < 3:
            print('Invalid username or password. Please try again.')
        attempts += 1

    if attempts == 3:
        print('Maximum login attempts reached.')

def menu():
    print("Please choose one of the following options:")
    print("1. Register and delete tutors. Assign tutors to respective levels and subjects.")
    print("2. Register and delete the receptionist.")
    print("3. View monthly income report based on level and subject.")
    print("4. Update own profile.")
    print("5. Exit.")
    choice = input("Enter your choice: ")

    if choice == "1":
        manage_tutors()
    elif choice == "2":
        manage_receptionist()
    elif choice == "3":
        view_income_report()
    elif choice == "4":
        update_profile()
    elif choice == "5":
        print("Exiting. Goodbye!")
        exit()
    else:
        print("Invalid choice. Please try again.")

def manage_tutors():
    print("Please choose one of the following options:")
    print("1. Register a new tutor.")
    print("2. Delete an existing tutor.")
    print("3. Assign a tutor to a level and a subject.")
    print("4. Go back to the main menu.")
    choice = input("Enter your choice: ")
    if choice == "1":
        register_tutor()
    elif choice == "2":
        delete_tutor()
    elif choice == "3":
        assign_tutor()
    elif choice == "4":
        return
    else:
        print("Invalid choice. Please try again.")

def register_tutor():
    username = input("Enter the username of the tutor: ")
    password = input("Enter the password of the tutor: ")

    # Save tutor data to the file
    with open("tutors.txt", "a") as file:
        file.write(f"{username},{password}\n")

    print(f"Tutor {username} has been registered successfully.")

def delete_tutor():
    try:
        with open("tutors.txt", "r") as file:
            lines = file.readlines()
            tutors = {}
            for line in lines:
                data = line.strip().split(",")
                if len(data) == 2:
                    username, password = data
                    tutors[username] = {
                        "password": password
                    }
    except FileNotFoundError:
        tutors = {}

    print("The list of tutors are:")
    for username in tutors:
        print(username)

    username = input("Enter the username of the tutor to be deleted: ")
    if username in tutors:
        del tutors[username]
        with open("tutors.txt", "w") as file:
            for tutor_username, tutor_info in tutors.items():
                file.write(f"{tutor_username},{tutor_info['password']}\n")
        print(f"Tutor {username} has been deleted successfully.")
    else:
        print(f"Tutor {username} does not exist.")

def assign_tutor():
    try:
        with open("tutors.txt", "r") as file:
            lines = file.readlines()
            tutors = {}
            for line in lines:
                data = line.strip().split(",")
                if len(data) == 2:
                    username, password = data
                    tutors[username] = {
                        "password": password
                    }
    except FileNotFoundError:
        tutors = {}

    print("The list of tutors are:")
    for username in tutors:
        print(username)

    username = input("Enter the username of the tutor: ")
    if username in tutors:
        level = input("Enter the level to assign (e.g., 'Intermediate', 'Advanced'): ")
        subject = input("Enter the subject to assign (e.g., 'Math', 'Science'): ")

        tutors[username]["level"] = level
        tutors[username]["subject"] = subject

        with open("tutors.txt", "w") as file:
            for tutor_username, tutor_info in tutors.items():
                file.write(
                    f"{tutor_username},{tutor_info['password']},{tutor_info['level']},{tutor_info['subject']}\n")

        print(f"Tutor {username} has been assigned to {level} {subject}.")
    else:
        print(f"Tutor {username} does not exist.")

def manage_receptionist():
    print("Please choose one of the following options:")
    print("1. Register a new receptionist.")
    print("2. Delete an existing receptionist.")
    print("3. Go back to the main menu.")
    choice = input("Enter your choice: ")
    if choice == "1":
        register_receptionist()
    elif choice == "2":
        delete_receptionist()
    elif choice == "3":
        return
    else:
        print("Invalid choice. Please try again.")
def register_receptionist():
    username = input("Enter the username of the tutor: ")
    password = input("Enter the password of the tutor: ")

    # Save tutor data to the file
    with open("receptionist.txt", "a") as file:
        file.write(f"{username},{password}\n")

    print(f"Receptionist {username} has been registered successfully.")
def delete_receptionist():
    try:
        with open("receptionist.txt", "r") as file:
            lines = file.readlines()
            receptionist = {}
            for line in lines:
                data = line.strip().split(",")
                if len(data) == 2:
                    username, password = data
                    receptionist[username] = {
                        "password": password
                    }
    except FileNotFoundError:
        receptionist = {}

    print("The list of receptionists are:")
    for username in receptionist:
        print(username)

    username = input("Enter the username of the receptionist to be deleted: ")
    if username in receptionist:
        del receptionist[username]
        with open("receptionist.txt", "w") as file:
            for receptionist_username, receptionist_info in receptionist.items():
                file.write(f"{receptionist_username},{receptionist_info['password']}\n")
        print(f"Receptionist {username} has been deleted successfully.")
    else:
        print(f"Receptionist {username} does not exist.")

def view_income_report():
    


login()
