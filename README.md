# MotorPH-Payroll-README
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
/**
 * Attendance class - records when an employee clocks in and out for the day.
 * Multiple Attendance records can be tied to a single Employee.
 */
public class Attendance {
    // Attributes
    private int attendanceID;
    private String timeIn;
    private String timeOut;
    private int employeeID; // links the record back to the Employee

    // Constructor
    public Attendance(int attendanceID, int employeeID) {
        this.attendanceID = attendanceID;
        this.employeeID = employeeID;
        this.timeIn = null;
        this.timeOut = null;
    }

    // ----- Methods from the class diagram -----

    /**
     * Records the clock-in time as an HH:mm string.
     */
    public void recordTimeIn(String time) {
        this.timeIn = time;
        System.out.println("[Attendance] Employee " + employeeID + " timed IN at " + time);
    }

    /**
     * Records the clock-out time as an HH:mm string.
     */
    public void recordTimeOut(String time) {
        this.timeOut = time;
        System.out.println("[Attendance] Employee " + employeeID + " timed OUT at " + time);
    }

    /**
     * Calculates the number of hours worked between timeIn and timeOut.
     * Expects HH:mm 24-hour format. Returns 0 if either value is missing.
     */
    public double hoursWorked() {
        if (timeIn == null || timeOut == null) return 0.0;
        int in = toMinutes(timeIn);
        int out = toMinutes(timeOut);
        if (out < in) return 0.0;
        return (out - in) / 60.0;
    }

    private int toMinutes(String hhmm) {
        String[] parts = hhmm.split(":");
        return Integer.parseInt(parts[0]) * 60 + Integer.parseInt(parts[1]);
    }

    // ----- Getters and setters -----

    public int getAttendanceID() { return attendanceID; }
    public void setAttendanceID(int attendanceID) { this.attendanceID = attendanceID; }

    public String getTimeIn() { return timeIn; }
    public void setTimeIn(String timeIn) { this.timeIn = timeIn; }

    public String getTimeOut() { return timeOut; }
    public void setTimeOut(String timeOut) { this.timeOut = timeOut; }

    public int getEmployeeID() { return employeeID; }
    public void setEmployeeID(int employeeID) { this.employeeID = employeeID; }

    @Override
    public String toString() {
        return "Attendance{id=" + attendanceID + ", employeeID=" + employeeID
                + ", timeIn=" + timeIn + ", timeOut=" + timeOut + "}";
    }
}
