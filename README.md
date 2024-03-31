import java.util.ArrayList;
import java.util.Scanner;

class Student {
    private String firstName;
    private String lastName;

    public Student(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String getLastName() {
        return lastName;
    }

    public String getFullName() {
        return firstName + " " + lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<Student> studentList = new ArrayList<>();

        boolean running = true;
        while (running) {
            System.out.println("1. Enter student list");
            System.out.println("2. Find students by last name");
            System.out.println("3. Find and edit students by full name");
            System.out.println("4. End");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Clear the newline character from the input buffer

            switch (choice) {
                case 1:
                    enterStudentList(scanner, studentList);
                    break;
                case 2:
                    findStudentsByLastName(scanner, studentList);
                    break;
                case 3:
                    findAndEditStudentsByFullName(scanner, studentList);
                    break;
                case 4:
                    running = false;
                    System.out.println("Program ended.");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a number between 1 and 4.");
            }
        }
        scanner.close();
    }

    private static void enterStudentList(Scanner scanner, ArrayList<Student> studentList) {
        System.out.print("Enter the number of students: ");
        int numberOfStudents = scanner.nextInt();
        scanner.nextLine(); // Clear the newline character from the input buffer

        for (int i = 0; i < numberOfStudents; i++) {
            System.out.println("Enter details for student #" + (i + 1) + ":");
            System.out.print("First name: ");
            String firstName = scanner.nextLine();
            System.out.print("Last name: ");
            String lastName = scanner.nextLine();
            studentList.add(new Student(firstName, lastName));
        }
        System.out.println("Student list updated.");
    }

    private static void findStudentsByLastName(Scanner scanner, ArrayList<Student> studentList) {
        System.out.print("Enter last name to search: ");
        String searchLastName = scanner.nextLine();
        System.out.println("Students with last name '" + searchLastName + "':");
        boolean found = false;
        for (Student student : studentList) {
            if (student.getLastName().equalsIgnoreCase(searchLastName)) {
                System.out.println(student.getFullName());
                found = true;
            }
        }
        if (!found) {
            System.out.println("No students found with the last name '" + searchLastName + "'.");
        }
    }

    private static void findAndEditStudentsByFullName(Scanner scanner, ArrayList<Student> studentList) {
        System.out.print("Enter full name to search: ");
        String searchFullName = scanner.nextLine();
        System.out.print("Enter new last name: ");
        String newLastName = scanner.nextLine();
        boolean found = false;
        for (Student student : studentList) {
            if (student.getFullName().equalsIgnoreCase(searchFullName)) {
                student.setLastName(newLastName);
                System.out.println("Student information updated.");
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("No students found with the full name '" + searchFullName + "'.");
        }
    }
}
