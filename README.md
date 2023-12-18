# List of Employees

Table of Contents
1. [Overview](#overview)
2. [DataSource](#datasource)
3. [Results](#results)
   * [Data Preprocessing](#data-preprocessing)
   * [Data Visualization](#data-visualization)
   * [Machine Learning](#machine-learning)
5. [Summary](#summary)

## Overview

This is a *menu-driven program* that implements a linked list of employees.

Each employee has an ID, full name, SSN(last 4 digits), wage, department, and date of hire, including the employee’s attributes. 
The ID is an integer and unique for a specific employee. 

Menu includes following operations:
• Add a new employee to anywhere in the list, for a just hired employee.
• Search for an existing employee in the list, for a real employee.
• Display information for all employees in the list, in tabular format with appropriate
headers that include Id, full name, SSN, wage, department, and hire date.
• Edit any information of an existing employee in the list, for up-to-date data.
• Delete an existing employee in the list, for a moved-out employee.
• All data can be saved to an external data file, for reusing the just-processed data later.
• All data can be read from an external data file, for retrieving previously-saved data.
• Quit the program, for doing something else.

## DataSource
External file : 

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

```
    // function declarations main.cpp
    void display_title();
    void display_menu();
    void display_employees(const vector<Employee>&);
    void read_file(vector<Employee>&);
    void write_file(const vector<Employee>&);
    void add_employee(vector<Employee>&);
    void search_employee(const vector<Employee>&);
    void update_employee(vector<Employee>&);
    void delete_employee(vector<Employee>&);
    set<int> get_ids(const vector<Employee>&);
    void display_employee_info(Employee&);

    void set_new_first_name(Employee&);
    void set_new_last_name(Employee&);
    void set_new_ssn(Employee&);
    void set_new_wage(Employee&);
    void set_new_department(Employee&);
    void set_new_hire_year(Employee&);
    void set_new_hire_month(Employee&);
    void set_new_hire_day(Employee&);
```

![PA15_list_of_employees_RUN_1.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_1.png)
![PA15_list_of_employees_RUN_2.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_2.png)
![PA15_list_of_employees_RUN_3.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_3.png)
![PA15_list_of_employees_RUN_4.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_4.png)
![PA15_list_of_employees_RUN_5.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_5.png)
![PA15_list_of_employees_RUN_6.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_6.png)
![PA15_list_of_employees_RUN_7.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_7.png)
![PA15_list_of_employees_RUN_8.png](https://github.com/CelineWW/CPP_Programming/blob/main/PA15_list_of_employees/PA15_list_of_employees_RUN_8.png)