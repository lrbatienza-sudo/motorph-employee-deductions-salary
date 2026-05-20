# Motorph-employee-salary-deductions-GROUP14CP2
import java.util.ArrayList;
import java.util.List;

/**
 * Employee class - represents an employee in the MotorPH Payroll System.
 * Holds basic identity info and is the central entity that attendance and
 * payroll records belong to.
 */
public class Employee {
    // Attributes (private, per class diagram)
    private int employeeID;
    private String name;
    private String position;
    private String password; // simple credential for the login() demo

    // An employee can have many attendance records (1..*)
    private List<Attendance> attendanceRecords;

    // Constructor
    public Employee(int employeeID, String name, String position, String password) {
        this.employeeID = employeeID;
        this.name = name;
        this.position = position;
        this.password = password;
        this.attendanceRecords = new ArrayList<>();
    }

    // Convenience constructor without password (defaults to "1234")
    public Employee(int employeeID, String name, String position) {
        this(employeeID, name, position, "1234");
    }

    // ----- Methods from the class diagram -----

    /**
     * Authenticates the employee. Returns true if the provided password matches.
     */
    public boolean login(String inputPassword) {
        boolean ok = this.password != null && this.password.equals(inputPassword);
        System.out.println(ok
                ? "[Login] " + name + " logged in successfully."
                : "[Login] Failed login attempt for employeeID=" + employeeID);
        return ok;
    }

    /**
     * Prints the employee's profile to the console.
     */
    public void viewProfile() {
        System.out.println("=== Employee Profile ===");
        System.out.println("ID:       " + employeeID);
        System.out.println("Name:     " + name);
        System.out.println("Position: " + position);
        System.out.println("Records:  " + attendanceRecords.size() + " attendance entries");
        System.out.println("========================");
    }

    // ----- Relationship helpers -----

    public void addAttendance(Attendance a) {
        this.attendanceRecords.add(a);
    }

    public List<Attendance> getAttendanceRecords() {
        return attendanceRecords;
    }

    // ----- Getters and setters -----

    public int getEmployeeID() { return employeeID; }
    public void setEmployeeID(int employeeID) { this.employeeID = employeeID; }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public String getPosition() { return position; }
    public void setPosition(String position) { this.position = position; }

    @Override
    public String toString() {
        return "Employee{id=" + employeeID + ", name='" + name + "', position='" + position + "'}";
    }
}
