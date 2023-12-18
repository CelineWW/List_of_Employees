//
//  Employee.h
//  PA15_list_of_employees
//
//  Created by Celine Wang on 12/8/23.
//

#ifndef Employee_h
#define Employee_h
//#include <map>

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


#endif /* Employee_h */
