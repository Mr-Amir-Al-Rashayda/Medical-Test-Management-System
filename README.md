# Birzeit University - Medical Test Management System

## Overview

This project implements a **Medical Test Management System** using **Object-Oriented Python**. It provides a system for storing, managing, retrieving, updating, and deleting medical test data for individual patients, reading and writing data to text files.

## Files

*   `MedicalTest.py`: The main Python script containing the classes and functions for the system.
*   `MedicalRecord.txt`: The primary data file storing all patient medical test records. Each line represents a single test entry.
*   `MedicalTest.txt`: A reference file containing details about available medical tests, including their normal ranges, units, and turnaround times.
*   `Project_Description.pdf`: The original project assignment description and requirements document.

## Data File Formats

*   `MedicalRecord.txt`: Stores patient test records. Each line represents one record and follows the format:
    `PatientID: TestName, TestDate, Result, Unit, Status[, CompletedDateTime]`
    - `PatientID`: 7-digit integer.
    - `TestName`: String (e.g., Hgb, BGT, LDL, systole, diastole).
    - `TestDate`: String in `YYYY-MM` format (or `YYYY-MM-DD hh:mm` if status is Completed, as per PDF, though the code might handle `YYYY-MM` consistently or add a separate time field). *Based on code and provided MedicalRecord.txt, the core format seems to be 5 fields, with a potential 6th field (date/time) added if status is completed.*
    - `Result`: Floating-point number.
    - `Unit`: String (e.g., mg/dL, g/dL, mm Hg). *The code adds this field when adding records.*
    - `Status`: String (`Pending`, `Completed`, or `Reviewed`).
    - `CompletedDateTime`: Optional field, a string in `YYYY-MM-DD hh:mm` format, present only if Status is `Completed`. *The Python code attempts to add the current date/time string here when status is set to 'completed'.*

    Example (based on provided `MedicalRecord.txt` and code's structure):
    ```
    1300500: Hgb, 2024-05, 14.2, g/dL, Completed, 2024-05-15 10:30
    1300511: LDL, 2024-06, 115.0, mg/dL, Pending
    ```

*   `MedicalTest.txt`: Describes available medical tests. Each line contains details about a test:
    `FullName (ShortName); Range: ...; Unit: UnitValue, TurnaroundTime`
    - `FullName`: Full name of the test (e.g., Hemoglobin).
    - `ShortName`: Abbreviated name of the test (e.g., Hgb).
    - `Range`: Description of the normal range (e.g., `> 13.8, < 17.2`).
    - `Unit`: The unit of measurement for the test result (e.g., `g/dL`).
    - `TurnaroundTime`: Time required to complete the test in `DD-HH-MM` format.

    Example (based on `MedicalTest.txt` and PDF):
    ```
    Hemoglobin (Hgb); Range: > 13.8, < 17.2; Unit: g/dL, 00-03-04
    Blood Glucose Test (BGT); Range: > 70, < 99; Unit: mg/dL, 00-12-06
    ```

## Features

The system provides a menu-driven interface with the following functionalities, implemented using Python classes (`MedicalTestRecord`, `Patient`, `MedicalRecordSystem`) and file I/O:

1.  **Add a new medical test record:** Prompts for patient ID, test name, date, result, and status with input validation (ID format, test name existence in `MedicalTest.txt`, date format/validity, numeric result, valid status). Stores the record in `MedicalRecord.txt`.
2.  **Update a medical test record:** Allows updating the Result, Date, or Status for a specific record identified by Patient ID, Test Name, and Date. Includes validation for existing records and new input formats. Updates the record in `MedicalRecord.txt`.
3.  **Add a new medical test:** Prompts for full name, short name, range details, unit, and turnaround time. Saves the new test definition to `MedicalTest.txt`.
4.  **Update a medical test:** Allows updating the Range, Unit, or Time Format for an existing test definition in `MedicalTest.txt`.
5.  **Filter medical tests:** Retrieves and displays records based on one or more criteria:
    *   By Patient ID
    *   By Test Name
    *   Abnormal tests (results outside the defined range in `MedicalTest.txt`)
    *   In a specific date period (YYYY-MM)
    *   By Test Status (Pending, Completed, Reviewed)
    *   By Test turnaround time within a period (DD-HH-MM)
6.  **Generate a summary for tests' values:** Calculates and displays the minimum, maximum, and average result value for each type of test recorded in `MedicalRecord.txt`.
7.  **Generate a summary for tests' turnaround time:** Calculates and displays the minimum, maximum, and average turnaround time (based on data in `MedicalTest.txt`).
8.  **Delete a medical test record:** Removes a specific record identified by Patient ID, Test Name, and Date after user confirmation. Updates the `MedicalRecord.txt` file.
9.  **Exit:** Quits the application.

The system includes error handling and data validation throughout the input process and file operations.

## Requirements

*   Python 3.x
*   Standard Python libraries (`re`, `datetime`, `sys`)
*   `MedicalRecord.txt` and `MedicalTest.txt` files located in the same directory as the script. (`MedicalRecord.txt` can be empty initially, but `MedicalTest.txt` must contain test definitions).

## How to Run

1.  Save the provided Python code content as `MedicalTest.py`.
2.  Ensure the `MedicalRecord.txt` and `MedicalTest.txt` files are present in the same directory as `MedicalTest.py`.
3.  Open a terminal or command prompt.
4.  Navigate to the directory where the files are saved.
5.  Run the script using the Python interpreter:
    ```bash
    python MedicalTest.py
    ```
6.  Follow the on-screen menu prompts to interact with the system.

## Implementation Details

-   **Object-Oriented Design:** The system is structured using classes: `MedicalTestRecord` to represent a single test entry, `Patient` to manage a collection of records for one patient, and `MedicalRecordSystem` to handle file loading, validation, and coordinating operations.
-   **Data Storage:** Patient records and test definitions are stored persistently in plain text files (`MedicalRecord.txt` and `MedicalTest.txt`).
-   **File I/O:** The script uses standard Python file operations (`open`, `read`, `write`, `readlines`, `writelines`) to interact with the data files.
-   **Validation:** Extensive use of loops and string manipulation (`isdigit`, `len`, `re.match`, `split`) is employed for input validation and data parsing.
-   **Filtering & Reporting:** Functions implement filtering logic based on various criteria and calculate summary statistics.

## Author

*   Name: Amir Rasmi Al-Rashayda
