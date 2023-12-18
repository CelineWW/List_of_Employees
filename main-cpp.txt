//
//  main.cpp
//  PA15_list_of_employees
//
//  Created by Celine Wang on 12/7/23.
//

#include <iostream>
#include <iomanip>
#include <fstream>
#include <set>
#include <vector>
#include "Employee.h"

using namespace std;

// function declarations
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

int main() {
    
    display_title();
    vector<Employee> employees;
    
    char read;
    while(true) {
    cout << "Reuse existing data previously saved in external file (y/n)? ";
    cin >> read;
    cin.clear();
        if (read == 'y') {
            read_file(employees);
            break;
        }
        else if (read == 'n'){
            break;
        }
        else {
            cout << "Invalid! Re-enter please!\n";
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            continue;
        }
    }

    
    // choose from menu
    int choice = 0;
    while (choice != 8){
        cout << "Press <Enter> key to continue...";
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
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
    }
    //    display_employees(employees);
    cout << "\nGood Bye!!!\n";
    cout << "Thank you for utilizing Celine's Employee List System.\n";
    cout << "Press <Enter> key to end...\n";
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    cout << endl;
    return 0;
}


// display_title() function definition
void display_title() {
    cout << endl
    << "                **** ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ ****  \n"
    << "                ****                                                     ****  \n"
    << "                **           Welcome to CELINE WANG's Employee List        **  \n"
    << "                ****                                                     ****  \n"
    << "                **** ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ = ~-~ ****  \n\n\n";
}


// display_menu() function definition
void display_menu() {
    cout << endl
    << "                                            M E N U                            \n"
    << "                                            =======                            \n"
    << "                              1. Add New Employee                              \n"
    << "                              2. Search Existing Employee                      \n"
    << "                              3. Display Employee List                         \n"
    << "                              4. Update Existing Employee                      \n"
    << "                              5. Delete Existing Employee                      \n"
    << "                              6. Save to file                                  \n"
    << "                              7. Read from file                                \n"
    << "                              8. Quit                                          \n\n\n";
}

// display_employees function definition
void display_employees(const vector<Employee>& employees_list) {
    cout << setw(6) << left << "ID"
    << setw(16) << left << "Employee Name"
    << setw(4) << right << "SSN"
    << setw(9) << right << "Wage"
    << setw(4) << "    "
    << setw(14) << left << "Department"
    << setw(18) << left << "Hired Date"
    << endl;
    
    cout << setw(6) << left << "=="
    << setw(16) << left << "============="
    << setw(4) << right << "==="
    << setw(9) << right << "===="
    << setw(4) << "    "
    << setw(14) << left << "==========="
    << setw(18) << left << "=========="
    << endl;
    
    for (Employee e: employees_list) {
        cout << setw(6) << left << e.get_employee_id()
        << setw(16) << left << e.get_full_name()
        << setw(4) << right << e.get_ssn()
        << setw(9) << right << e.get_wage()
        << setw(4) << "    "
        << setw(14) << left << e.get_department()
        << setw(18) << left << e.get_hire_date()      // or use following code instead
//        << Employee::map_month(e.get_hire_month()) << " " << setw(2) << setfill('0')
//        << e.get_hire_day()  << setfill(' ') << ", " << e.get_hire_year()
        << endl;
    }
    cout << "\nNumber of records in the list: " << employees_list.size() << endl;
}

// read_file function definition
void read_file(vector<Employee>& employees){
    employees.clear();        // clear the existing employees in the vector
    string input_file_name;
    ifstream input_file;
    while(true) {
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        cout << "Enter file name to read data: ";
        getline(cin, input_file_name);
        input_file.open(input_file_name, ios::in);
        if (input_file) {
            cout << "\nAll data were read back from file \"" << input_file_name << "\" successfully!\n\n";
            Employee emp;
            string emp_id;
            string emp_first_name;
            string emp_last_name;
            string emp_ssn;
            string emp_wage;
            string emp_department;
            string emp_day;
            string emp_month;
            string emp_year;
            
            // while (!input_file.eof()) will get extra line (last row show 2 times)
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
            input_file.close();
            display_employees(employees);
            break;
        }
        else {
            cout << "Unable to open file. Try again!\n";
        }
    }
    return;
}

// write_file function definition
void write_file(const vector<Employee>& employees){
    string output_file_name;
    ofstream output_file;
    cout << "Enter file name to save data: ";
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    getline(cin, output_file_name);
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
    return;
}

// add_employee function definition
void add_employee(vector<Employee>& employees){
    
    // create new variables to save employee information
    int row_add;
    int id_add;
    string first_name_add;
    string last_name_add;
    int ssn_add;
    double wage_add;
    string department_add;
    int hire_year_add;
    int hire_month_add;
    int hire_day_add;
    
    // add employee
    Employee employee;
    
    // set added employee id
    while (true) {
        cout << "What's the new employee's ID? ";
        if ((cin >> id_add) && (id_add > 0) && (id_add < 99)){
            employee.set_employee_id(id_add);
            break;
        }
        else {
            cout << "Invalid ID! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    
    // set added employee's first name
    cout << "What's the new employee's first name? ";
    cin >> first_name_add;
    employee.set_first_name(first_name_add);
    
    // set added employee's last name
    cout << "What's the new employee's last name? ";
    cin >> last_name_add;
    employee.set_last_name(last_name_add);
    
    // set added employee ssn
    while (true) {
        cout << "What's the new employee's ssn (last 4 digits)? ";
        if ((cin >> ssn_add) && (ssn_add >= 0) && (ssn_add < 10000)){
            employee.set_ssn(ssn_add);
            break;
        }
        else {
            cout << "Invalid SSN! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    // set added employee wage
    while (true) {
        cout << "What's the new employee's wage? ";
        if ((cin >> wage_add) && (wage_add >= 0) && (wage_add < 1000)){
            employee.set_wage(wage_add);
            break;
        }
        else {
            cout << "Invalid wage! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    // set added employee's department
    cout << "What's the new employee's department? ";
    cin >> department_add;
    employee.set_department(department_add);
    
    // set added employee hire year
    while (true) {
        cout << "What's the new employee's hire year? ";
        if ((cin >> hire_year_add) && (hire_year_add > 1799) && (hire_year_add < 2025)){
            employee.set_hire_year(hire_year_add);
            break;
        }
        else {
            cout << "Invalid year! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    // set added employee hire month
    while (true) {
        cout << "What's the new employee's hire month? ";
        if ((cin >> hire_month_add) && (hire_month_add < 13) && (hire_month_add > 0)){
            employee.set_hire_month(hire_month_add);
            break;
        }
        else {
            cout << "Invalid month! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    // set added employee hire day
    while (true) {
        cout << "What's the new employee's hire day? ";
        if ((cin >> hire_day_add) && (hire_day_add < 31) && (hire_day_add > 0)){
            employee.set_hire_day(hire_day_add);
            break;
        }
        else {
            cout << "Invalid day! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
    
    // set row number to added employee
    while (true) {
        cout << "Which row do you want to add? ";
        if (cin >> row_add && row_add < employees.size() + 1){
            employees.insert(employees.begin() + row_add - 1, employee);
            break;
        }
        else {
            cout << "Invalid row number! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}

// search_employee function definition
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

// update_employee function definition
void update_employee(vector<Employee>& employees){
    Employee employee_update;
    set<int> ids = get_ids(employees);
    int id_update;
    while(true) {
    cout << "Enter employee's ID to update: ";
        if (cin.fail()){
            cout << "Invalid ID. Please enter an id to update.\n";
            continue;
        }
        else if(cin >> id_update){
            auto iter = find(ids.begin(), ids.end(), id_update);
            // update id not found
            if (iter == ids.end()){
                cout << "Employee ID does not exist.\n";
               continue;
            }
            // id is found, locate the employee whose id is the same to *iter
            else {
                for (Employee employee: employees) {
                    if (employee.get_employee_id() == *iter) {
                        employee_update = employee;
                    }
                }
            }
        }
        set_new_first_name(employee_update);
        set_new_last_name(employee_update);
        set_new_ssn(employee_update);
        set_new_wage(employee_update);
        set_new_department(employee_update);
        set_new_hire_year(employee_update);
        set_new_hire_month(employee_update);
        set_new_hire_day(employee_update);
        cout << "Employee with ID " << employee_update.get_employee_id() << " updated successfully.\n" << endl;
        display_employee_info(employee_update);
        break;
    }
}

// delete_employee function definition
void delete_employee(vector<Employee>& employees){
    Employee employee_delete;
    set<int> ids = get_ids(employees);
    int id_delete;
    cout << "Enter employee's ID to delete: ";
    if (cin.fail()){
        cout << "Invalid ID. Please enter an ID to delete.\n";
    }
    else if(cin >> id_delete){
        auto iter = find(ids.begin(), ids.end(), id_delete);
        if (iter == ids.end()){
            cout << "Employee ID does not exist.\n";
        }
        else {
            for (Employee employee: employees) {
                // use operator++ to locate and delete the employee
                if (employee.get_employee_id() == id_delete) {
                    employee_delete = employee;
                }
            }
            display_employee_info(employee_delete);
            employees.erase(remove(employees.begin(), employees.end(), employee_delete), employees.end());
            cout << "Employee with ID " << employee_delete.get_employee_id() << "deleted successfully." << endl;
            
//            // Use pointer to locate employee and delete the employee
//            auto exist = [&](const Employee& employee){
//                return employee.get_employee_id() == id_delete;
//            };
//            
//            auto iter_remove = remove_if(employees.begin(), employees.end(), exist);
//            if (iter_remove != employees.end()){
//                employee_delete = *iter_remove;
//                employees.erase(iter_remove, employees.end());
//                
//                display_employee_info(employee_delete);
//                cout << "Employee with ID " << employee_delete.get_employee_id() << "deleted successfully." << endl;
//            }
//            else {
//                cout << "Employee with ID " << id_delete << " not found.\n";
//            }
        }
    }

}

// get_ids function definition - create a set of employee ids
set<int> get_ids(const vector<Employee>& employees){
    set<int> ids;
    for(Employee employee: employees){
        int id = employee.get_employee_id();
        ids.insert(id);
    }
    return ids;
}

// display_employee_info function definition
void display_employee_info(Employee& employee){
    cout << "\nEmployee's information:" << endl;
    cout << setw(12) << right << "ID: " << employee.get_employee_id() << endl
    << setw(12) << right << "Name: " << employee.get_full_name() << endl
    << setw(12) << right << "SSN: " << employee.get_ssn() << endl
    << setw(12) << right << "Wage: " << "$"<< employee.get_wage() << "/hr" << endl
    << setw(12) << right << "Department: " << employee.get_department() << endl
    << setw(12) << right << "Date Hire: " << employee.get_hire_date() << endl << endl;
}

// set_new_first_name function definition
void set_new_first_name(Employee& employee){
    string new_first_name;
    cout << "What's the employee's new first name? ";
    cin >> new_first_name;
    employee.set_first_name(new_first_name);
}

// set_new_last_name function definition
void set_new_last_name(Employee& employee){
    string new_last_name;
    cout << "What's the employee's new last name? ";
    cin >> new_last_name;
    employee.set_last_name(new_last_name);
}

// set_new_ssn function definition
void set_new_ssn(Employee& employee){
    int new_ssn;
    while (true) {
        cout << "What's the employee's new ssn (last 4 digits)? ";
        if ((cin >> new_ssn) && (new_ssn >= 0) && (new_ssn < 10000)){
            employee.set_ssn(new_ssn);
            break;
        }
        else {
            cout << "Invalid SSN! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}

// set_new_wage function definition
void set_new_wage(Employee& employee){
    double new_wage;
    while (true) {
        cout << "What's the employee's new wage? ";
        if ((cin >> new_wage) && (new_wage >= 0) && (new_wage < 1000)){
            employee.set_wage(new_wage);
            break;
        }
        else {
            cout << "Invalid wage! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}

// set_new_department function definition
void set_new_department(Employee& employee){
    string new_department;
    cout << "What's the employee's new department? ";
    cin >> new_department;
    employee.set_department(new_department);
}

// set_new_hire_year function definition
void set_new_hire_year(Employee& employee){
    double new_hire_year;
    while (true) {
        cout << "What's the employee's new hire year? ";
        if ((cin >> new_hire_year) && (new_hire_year > 1799) && (new_hire_year < 2025)) {
            employee.set_hire_year(new_hire_year);
            break;
        }
        else {
            cout << "Invalid hire year! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}

// set_new_hire_month function definition
void set_new_hire_month(Employee& employee){
    double new_hire_month;
    while (true) {
        cout << "What's the employee's new hire month? ";
        if ((cin >> new_hire_month) && (new_hire_month < 13) && (new_hire_month > 0)){
            employee.set_hire_month(new_hire_month);
            break;
        }
        else {
            cout << "Invalid hire month! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}

// set_new_hire_day function definition
void set_new_hire_day(Employee& employee){
    double new_hire_day;
    while (true) {
        cout << "What's the employee's new hire day? ";
        if ((cin >> new_hire_day) && (new_hire_day < 31) && (new_hire_day > 0)){
            employee.set_hire_day(new_hire_day);
            break;
        }
        else {
            cout << "Invalid hire day! Try again!\n";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        }
    }
}
