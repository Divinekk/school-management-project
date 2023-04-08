# school-management-project
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;

public class SchoolManagementSystem {
    // Define student class
    static class Student {
        String name;
        int id;
        ArrayList<String> timetable;
        HashMap<String, Integer> attendance;
        int studyHours;

        public Student(String name, int id, ArrayList<String> timetable) {
            this.name = name;
            this.id = id;
            this.timetable = timetable;
            attendance = new HashMap<>();
            for (String course : timetable) {
                attendance.put(course, 0);
            }
            studyHours = 0;
        }

        public void markAttendance(String course) {
            if (attendance.containsKey(course)) {
                attendance.put(course, attendance.get(course) + 1);
                System.out.println("Attendance marked for " + course);
            } else {
                System.out.println("Invalid course");
            }
        }

        public void viewTimetable() {
            System.out.println("Your timetable:");
            for (String course : timetable) {
                System.out.println(course);
            }
        }

        public void viewAttendance() {
            System.out.println("Your attendance:");
            for (String course : attendance.keySet()) {
                System.out.println(course + ": " + attendance.get(course));
            }
        }

        public void addStudyHours(int hours) {
            studyHours += hours;
            System.out.println("Study hours added: " + hours);
        }

        public void viewStudyHours() {
            System.out.println("Your study hours: " + studyHours);
        }
    }

    public static void main(String[] args) {
        // Create a list of students and their timetables
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 1, new ArrayList<String>() {{
            add("Math");
            add("English");
            add("Science");
        }}));
        students.add(new Student("Bob", 2, new ArrayList<String>() {{
            add("Math");
            add("History");
            add("Art");
        }}));

        // Allow students to access the system by entering their ID
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter your student ID: ");
        int id = scanner.nextInt();

        // Find the student with the matching ID
        Student student = null;
        for (Student s : students) {
            if (s.id == id) {
                student = s;
                break;
            }
        }

        // If no matching student found, exit the program
        if (student == null) {
            System.out.println("Invalid student ID");
            System.exit(1);
        }

        // Allow the student to perform actions on their account
        while (true) {
            System.out.println("\nEnter a number to perform an action:");
            System.out.println("1. View timetable");
            System.out.println("2. Mark attendance");
            System.out.println("3. View attendance");
            System.out.println("4. Add study hours");
            System.out.println("5. View study hours");
            System.out.println("6. Exit");

            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1:
                    student.viewTimetable();
                    break;
                case 2:
                    System.out.print("Enter course to mark attendance: ");
                    String course = scanner.nextLine();
                    student.markAttendance(course);
                    break;
                case 3:
                    student.viewAttendance();
                    break;
                case 4:
                    System.out.print("Enter number of study hours to add: ");
                    int hours
