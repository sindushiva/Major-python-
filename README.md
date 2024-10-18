class Student:
    def _init_(self, name, roll_number):
        self.name = name
        self.roll_number = roll_number
        self.grades = {}  # Dictionary to store subject-wise grades
    
    def add_grade(self, subject, grade):
        if 0 <= grade <= 100:  # Ensure grade is valid
            self.grades[subject] = grade
        else:
            print("Invalid grade! Must be between 0 and 100.")
    
    def calculate_average(self):
        if self.grades:
            total = sum(self.grades.values())
            return total / len(self.grades)
        return 0.0
    
    def display_details(self):
        print(f"Name: {self.name}")
        print(f"Roll Number: {self.roll_number}")
        print("Grades:")
        for subject, grade in self.grades.items():
            print(f"{subject}: {grade}")
        print(f"Average Grade: {self.calculate_average()}\n")


class StudentTracker:
    def _init_(self):
        self.students = []
    
    def add_student(self, name, roll_number):
        # Check for unique roll number
        if any(student.roll_number == roll_number for student in self.students):
            print("Roll number must be unique!")
        else:
            student = Student(name, roll_number)
            self.students.append(student)
            print(f"Student {name} added successfully.")
    
    def find_student(self, roll_number):
        for student in self.students:
            if student.roll_number == roll_number:
                return student
        return None
    
    def add_grades(self, roll_number):
        student = self.find_student(roll_number)
        if student:
            subject = input("Enter subject name: ")
            grade = float(input(f"Enter grade for {subject}: "))
            student.add_grade(subject, grade)
            print("Grade added successfully.")
        else:
            print("Student not found.")
    
    def view_student_details(self, roll_number):
        student = self.find_student(roll_number)
        if student:
            student.display_details()
        else:
            print("Student not found.")
    
    def calculate_average_for_all(self):
        if self.students:
            for student in self.students:
                print(f"{student.name}'s Average Grade: {student.calculate_average()}")
        else:
            print("No students found.")


# Functions to interact with users
def menu():
    tracker = StudentTracker()
    
    while True:
        print("\n--- Student Performance Tracker ---")
        print("1. Add Student")
        print("2. Add Grades")
        print("3. View Student Details")
        print("4. Calculate Average for All Students")
        print("5. Exit")
        
        choice = input("Select an option: ")
        
        if choice == '1':
            name = input("Enter student's name: ")
            roll_number = input("Enter roll number: ")
            tracker.add_student(name, roll_number)
        
        elif choice == '2':
            roll_number = input("Enter student's roll number to add grades: ")
            tracker.add_grades(roll_number)
        
        elif choice == '3':
            roll_number = input("Enter student's roll number to view details: ")
            tracker.view_student_details(roll_number)
        
        elif choice == '4':
            tracker.calculate_average_for_all()
        
        elif choice == '5':
            print("Exiting...")
            break
        
        else:
            print("Invalid choice. Please try again.")


if _name_ == "_main_":
    menu()
