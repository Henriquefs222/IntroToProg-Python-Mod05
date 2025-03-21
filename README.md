# IntroToProg-Python-Mod05
Python 100
jetbrains://pycharm/navigate/reference?project=PythonProject&path=.venv%2FAssignment5.py
[A05.zip](https://github.com/user-attachments/files/19344329/A05.zip)


# Assignment05.py
# Author: [Your Name]
# Date: [Current Date]

import json

# Constants
MENU = """---- Course Registration Program ----
Select from the following menu:  
1. Register a Student for a Course
2. Show current data  
3. Save data to a file
4. Exit the program
-----------------------------------------"""

FILE_NAME = "Enrollments.json"

# Variables
student_first_name = ""
student_last_name = ""
course_name = ""
file = None
menu_choice = ""
student_data = {}
students = []


# Function to load existing data from the JSON file
def load_data():
    try:
        with open(FILE_NAME, 'r') as file:
            return json.load(file)
    except FileNotFoundError:
        print("File not found. Starting with an empty list.")
        return []
    except json.JSONDecodeError:
        print("Error decoding JSON. Starting with an empty list.")
        return []


# Function to display the menu and get user choice
def display_menu():
    print(MENU)
    return input("Enter your choice: ")


# Function to register a student
def register_student():
    global student_first_name, student_last_name, course_name
    try:
        student_first_name = input("Enter the student's first name: ")
        if not student_first_name.strip():
            raise ValueError("First name cannot be empty.")

        student_last_name = input("Enter the student's last name: ")
        if not student_last_name.strip():
            raise ValueError("Last name cannot be empty.")

        course_name = input("Enter the course name: ")

        # Create a dictionary for the student data
        student_data = {
            "first_name": student_first_name,
            "last_name": student_last_name,
            "course": course_name
        }
        students.append(student_data)
        print(f"Registered: {student_first_name} {student_last_name} for {course_name}")

    except ValueError as e:
        print(f"Error: {e}")


# Function to display current student data
def show_current_data():
    if not students:
        print("No student registrations found.")
    else:
        print("Current Student Registrations:")
        for student in students:
            print(f"{student['first_name']} {student['last_name']} - {student['course']}")


# Function to save data to a JSON file
def save_data():
    try:
        with open(FILE_NAME, 'w') as file:
            json.dump(students, file)
        print(f"Data saved to {FILE_NAME}.")
    except Exception as e:
        print(f"Error saving data: {e}")


# Main program loop
def main():
    global menu_choice
    students.extend(load_data())  # Load existing data

    while True:
        menu_choice = display_menu()

        if menu_choice == '1':
            register_student()
        elif menu_choice == '2':
            show_current_data()
        elif menu_choice == '3':
            save_data()
        elif menu_choice == '4':
            print("Exiting the program.")
            break
        else:
            print("Invalid choice. Please select a valid option.")


if __name__ == "__main__":
    main()
