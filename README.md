# List of Employees

Table of Contents
1. [Overview](#overview)
2. [DataSource](#datasource)
3. [Results](#results)
   * [Employee Attributes](#employee_attributes)
   * [Employee Class](#employee_class)
   * [Operation Menu](#operation_menu)
   * [Functions in main.cpp](#functions_in_main.cpp)
   * [File I/O](#file_i\o)
   * [Data Validation](#data_validation)
   * [Formatting](#formatting)
5. [Summary](#summary)

## Overview

This is a *menu-driven program* that implements a linked list of employees.

Each employee has an ID, full name, SSN(last 4 digits), wage, department, and date of hire, including the employee’s attributes. 
The ID is an integer and unique for a specific employee. 

Menu includes following operations:
-  Add a new employee to anywhere in the list, for a just hired employee.
-  Search for an existing employee in the list, for a real employee.
-  Display information for all employees in the list, in tabular format with appropriate
headers that include Id, full name, SSN, wage, department, and hire date.
-  Edit any information of an existing employee in the list, for up-to-date data.
-  Delete an existing employee in the list, for a moved-out employee.
-  All data can be saved to an external data file, for reusing the just-processed data later.
-  All data can be read from an external data file, for retrieving previously-saved data.
-  Quit the program, for doing something else.

## DataSource
Sample file : [Employees Data.txt](https://github.com/CelineWW/List_of_Employees/blob/main/Employees%20Data.txt)

## Result
### Employee Attributes
Each employee has the following attributes:
- ID (integer and unique)
- full name 
    -  first name 
    -  last name
- SSN(last 4 digits)
- wage
- department- 
- date of hire 
    - hire year
    - hire month
    - hire day

### Employee Class
Member and member functions in Emloyee Class
```
    class Employee {
    private:
        int employee_id = 0;
        std::string first_name = "";
        std::string last_name = "";
        int ssn = 0;
        double wage = 0.00;
        std::string department = "";
        int hire_year = 0;
        int hire_month = 0;
        int hire_day = 0;
        
    public:
        // setter member function
        void set_employee_id(int);
        void set_first_name(std::string);
        void set_last_name(std::string);
        void set_ssn(int);
        void set_wage(double);
        void set_department(std::string);
        void set_hire_year(int);
        void set_hire_month(int);
        void set_hire_day(int);
        
        // getter member function
        int get_employee_id() const;
        std::string get_first_name() const;
        std::string get_last_name() const;
        std::string get_full_name() const;
        int get_ssn() const;
        double get_wage() const;
        std::string get_department() const;
        int get_hire_year() const;
        int get_hire_month() const;
        int get_hire_day() const;
        std::string get_hire_date() const;
        bool operator==(const Employee&);
        static std::string map_month(int);
    };
```

### Operation Menu
```
display_menu();
        cout << "Enter your choice (1-8): ";
        cin >> choice;
        switch (choice) {
            case 1:
                add_employee(employees);
                break;
            case 2:
                search_employee(employees);
                break;
            case 3:
                display_employees(employees);
                break;
            case 4:
                update_employee(employees);
                break;
            case 5:
                delete_employee(employees);
                break;
            case 6:
                write_file(employees);
                break;
            case 7:
                read_file(employees);
                break;
            case 8:
                break;
            default:
                cout << "Invalid choice! Back to Menu!";
        }
```

### Functions in main.cpp
-  Regular functions
    ```
    void display_title();
    void display_menu();
    void display_employees(const vector<Employee>&);
    void read_file(vector<Employee>&);
    void write_file(const vector<Employee>&);
    void add_employee(vector<Employee>&);
    void search_employee(const vector<Employee>&);
    void update_employee(vector<Employee>&);
    void delete_employee(vector<Employee>&);
    ```
- Helper functions
    1. Get a set of employee IDs for searching.
    ```
    set<int> get_ids(const vector<Employee>&);
    ```

    2. Set new employee information to update employee attributes.
    ```
    void set_new_first_name(Employee&);
    void set_new_last_name(Employee&);
    void set_new_ssn(Employee&);
    void set_new_wage(Employee&);
    void set_new_department(Employee&);
    void set_new_hire_year(Employee&);
    void set_new_hire_month(Employee&);
    void set_new_hire_day(Employee&);
    ```
    3. Display individual Employee information after add, search, edit, delete employee option.
    ```
    void display_employee_info(Employee&);
    ```
    4. Convert month number to month name.
    ```
    string Employee::map_month(int month_param){
    map<int, string> months {{1, "January"}, {2,"February"}, {3, "March"},
        {4, "April"}, {5, "May"}, {6, "June"}, {7, "July"}, {8, "August"},
        {9, "September"}, {10, "October"}, {11, "November"}, {12, "December"}
        };
    string month_name;
    for(pair<int, string> m: months){
        if (m.first == month_param) {
            month_name = m.second;
        }
    }
    return  month_name;
}
    ```

    
### File I/O
-  Input file 
    ```
    while (getline(input_file, emp_id, ' ') &&
        getline(input_file, emp_first_name, ' ') &&
        getline(input_file, emp_last_name,  ' ') &&
        getline(input_file, emp_ssn, ' ') &&
        getline(input_file, emp_wage, ' ') &&
        getline(input_file, emp_department, ' ') &&
        getline(input_file, emp_month, '/') &&
        getline(input_file, emp_day, '/') &&
        getline(input_file, emp_year)){
    
    // convert some string input to integer or double data type
    int emp_id_int = stoi(emp_id);
    int emp_ssn_int = stoi(emp_ssn);
    double emp_wage_double = stod(emp_wage);
    int emp_day_int = stoi(emp_day);
    int emp_month_int = stoi(emp_month);
    int emp_year_int = stoi(emp_year);
    
    // set employee information
    emp.set_employee_id(emp_id_int);
    emp.set_first_name(emp_first_name);
    emp.set_last_name(emp_last_name);
    emp.set_ssn(emp_ssn_int);
    emp.set_wage(emp_wage_double);
    emp.set_department(emp_department);
    emp.set_hire_day(emp_day_int);
    emp.set_hire_month(emp_month_int);
    emp.set_hire_year(emp_year_int);
    
    // add employee to employee list
    employees.push_back(emp);
    }
    ```
-  Output file
    ```
    output_file.open(output_file_name, ios::out | ios::trunc);
    // if file exists, remove existing file content. Save new data to the file
    if (output_file) {
        for (Employee employee: employees) {
            output_file << employee.get_employee_id() << ' '
            << employee.get_first_name() << ' '
            << employee.get_last_name() << ' '
            << employee.get_ssn() << ' '
            << employee.get_wage() << ' '
            << employee.get_department() << ' '
            << employee.get_hire_month() << '/'
            << employee.get_hire_day() << '/'
            << employee.get_hire_year() << "\n";
        }
        cout << "All data were saved to file \"" << output_file_name << "\" successfully!\n";
        output_file.close();
    }
    else {      // if file not exist, create new file and save data to the new file
        cout << "New file " << output_file_name << " created.\n";
        cout << "All data were saved to file \"" << output_file_name << "\" successfully!\n";
    }
    ```

### Data Validation
    1. file name (look for external data source)
    2. menu option (default case)
    3. ID (number, 0 ~ 99)
    4. ssn (4 digit number: 0 <= ssn < 10000)
    5. wage (3 digit number: 0 <= wage < 1000)
    6. hire year (number: 1799 < hire year < 2025)
    7. hire month (number: 0 < hire month < 13)
    8. hire day (number: 0 < hire day < 31)
    9. add row number (row_add < employees.size() + 1)
    10. search employee (id match and employee match)
    ```
    void search_employee(const vector<Employee>& employees){
        Employee employee_search;
        set<int> ids = get_ids(employees);
        int id_search;
        cout << "Enter employee's ID to search: ";
        if (cin.fail()){
            cout << "Invalid ID. Please enter an id to search.\n";
        }
        else if(cin >> id_search){
            auto iter = find(ids.begin(), ids.end(), id_search);
            // search id not found
            if (iter == ids.end()){
                cout << "Employee ID does not exist.\n";
            }
            // id is found, locate the employee whose id is the same to *iter
            else {
                for (Employee employee: employees) {
                    if (employee.get_employee_id() == *iter) {
                        employee_search = employee;
                    }
                }
                display_employee_info(employee_search);
            }
        }
    }
    ```
    11. update employee (id match and employee match)
    12. delete employee (id match and employee match)

### Formatting
    1. Tabulea table of list of employees
    ```
    cout << setw(6) << left << "ID"
    << setw(16) << left << "Employee Name"
    << setw(4) << right << "SSN"
    << setw(9) << right << "Wage"
    << setw(4) << "    "
    << setw(14) << left << "Department"
    << setw(18) << left << "Hired Date"
    << endl;
```

    2. Hire date
    - option 1:
    ```
    << Employee::map_month(e.get_hire_month()) << " " << setw(2) << setfill('0')
    << e.get_hire_day()  << setfill(' ') << ", " << e.get_hire_year()
    ```
    - option 2:
    ```
        string hire_date;
    if (hire_day > 9){
        hire_date = map_month(hire_month) + " " + to_string(hire_day) + ", " + to_string(hire_year);
    }
    // or use cout & setfill('0') to fill 0 to the single digit day
    else if (hire_day <= 9){
        hire_date = map_month(hire_month) + " 0" + to_string(hire_day) + ", " + to_string(hire_year);
    }
    ```

![PA15_list_of_employees_RUN_1.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_1.png)
![PA15_list_of_employees_RUN_2.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_2.png)
![PA15_list_of_employees_RUN_3.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_3.png)
![PA15_list_of_employees_RUN_4.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_4.png)
![PA15_list_of_employees_RUN_5.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_5.png)
![PA15_list_of_employees_RUN_6.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_6.png)
![PA15_list_of_employees_RUN_7.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_7.png)
![PA15_list_of_employees_RUN_8.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_8.png)