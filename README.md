# MotorPH Payroll System

A simple Java implementation of the MotorPH Payroll System class diagram for **MO-IT103 Computer Programming 2** (Group No. 14, H1101).

The project models an employee payroll workflow with five core classes and demonstrates basic OOP concepts: encapsulation, class collaboration, and one-to-many relationships.

## Class Diagram Overview

| Class | Responsibility |
| --- | --- |
| `Employee` | Holds employee identity (ID, name, position) and supports `login()` / `viewProfile()` |
| `Attendance` | Records `timeIn` / `timeOut` for an employee and calculates hours worked |
| `Payroll` | Calculates gross and net pay using attendance records and deductions |
| `Deduction` | Stores tax and SSS amounts; `computeTax()` returns 10% of gross pay |
| `Admin` | Manages employees and runs payroll via `addEmployee()` and `processPayroll()` |

### Relationships

- `Employee` **1 — \*** `Attendance` (one employee, many attendance records)
- `Payroll` **1 — \*** `Deduction` (one payroll, many deductions)
- `Admin` — — →  `Employee` (dependency: Admin manages Employees)

## Project Structure

```
motorph-payroll-system/
├── README.md
├── .gitignore
└── src/
    ├── Employee.java
    ├── Attendance.java
    ├── Payroll.java
    ├── Deduction.java
    ├── Admin.java
    ├── Main.java                  # demo program
    └── MotorPHPayrollTest.java    # unit tests
```

## Requirements

- **JDK 8 or higher** (tested on OpenJDK 21)

Check with:
```bash
javac -version
java -version
```

## How to Compile and Run

From the repository root:

```bash
# 1. Move into the source folder
cd src

# 2. Compile every .java file
javac *.java

# 3. Run the demo program
java Main

# 4. Run the unit tests
java MotorPHPayrollTest
```

## Sample Demo Output

```
============================================
 MotorPH Payroll System - Demo
============================================

[Admin 9001] Added employee: Juan dela Cruz
[Admin 9001] Added employee: Maria Santos

[Login] Juan dela Cruz logged in successfully.
=== Employee Profile ===
ID:       1
Name:     Juan dela Cruz
Position: Software Engineer
========================

[Payroll] Calculated for employee 1: gross=4500.0, net=3550.0 (18.0 hrs @ 250.0/hr)
======== PAYSLIP ========
Payroll ID:  1000
Employee ID: 1
Gross Pay:   PHP 4500.00
Deductions:
  - Tax: PHP 450.00, SSS: PHP 500.00
Net Pay:     PHP 3550.00
=========================
```

## Tests

`MotorPHPayrollTest` uses a tiny built-in assertion runner (no external libraries) and currently includes **16 tests** covering:

- Employee creation, successful login, failed login
- Attendance time recording and hours-worked calculation
- Deduction tax computation and total deductions
- Payroll gross-pay calculation and net-pay calculation with deductions
- Admin employee management and end-to-end payroll processing

Expected output ends with:
```
 Results: 16 passed, 0 failed
```

## Author

**Group No. 14** — MO-IT103 Computer Programming 2 (H1101)

## License

Educational use only. This project implements an assignment template under the Mapua-Malayan Digital College curriculum.
