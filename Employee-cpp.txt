//
//  Employee.cpp
//  PA15_list_of_employees
//
//  Created by Celine Wang on 12/8/23.
//

#include <stdio.h>
#include <iostream>
#include <string>
#include <map>
#include "Employee.h"


using namespace std;

// setter member function definition
void Employee::set_employee_id(int id_param){
    employee_id = id_param;}
void Employee::set_first_name(std::string first_name_param) {
    first_name = first_name_param;}
void Employee::set_last_name(std::string last_name_param) {
    last_name = last_name_param;}
void Employee::set_ssn(int ssn_param)  {
    ssn = ssn_param; }
void Employee::set_wage(double wage_param) {
    wage = wage_param; }
void Employee::set_department(std::string department_param) {
    department = department_param; }
void Employee::set_hire_year(int hire_year_param) {
    hire_year = hire_year_param; }
void Employee::set_hire_month(int hire_month_param) {
    hire_month = hire_month_param; }
void Employee::set_hire_day(int hire_day_param) {
    hire_day = hire_day_param; }

// getter member function definition
int Employee::get_employee_id() const {
    return employee_id;}

string Employee::get_first_name() const {
    return first_name;}

string Employee::get_last_name() const {
    return last_name;}

string Employee::get_full_name() const {
    return first_name + " " + last_name;}

int Employee::get_ssn() const {
    return ssn;}

double Employee::get_wage() const {
    return wage;}

string Employee::get_department() const {
    return department;}

int Employee::get_hire_year() const {
        return hire_year;}

int Employee::get_hire_month() const {
    return hire_month;}

int Employee::get_hire_day() const {
    return hire_day;}

string Employee::get_hire_date() const {
    string hire_date;
    if (hire_day > 9){
        hire_date = map_month(hire_month) + " " + to_string(hire_day) + ", " + to_string(hire_year);
    }
    // or use cout & setfill('0') to fill 0 to the single digit day
    else if (hire_day <= 9){
        hire_date = map_month(hire_month) + " 0" + to_string(hire_day) + ", " + to_string(hire_year);
    
    }
    return hire_date;
}

bool Employee::operator== (const Employee& employee_to_compare){
        return (employee_id == employee_to_compare.employee_id);
}

// helper function
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
