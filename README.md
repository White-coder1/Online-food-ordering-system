// online food odering system
#include <iostream>
#include <string>
using namespace std;

struct customer_detail {
    string name;
    string email;
    string password;
    string address;
};

float total_price = 0; // Initialize total_price

void displayMenu();
void burgers();
void fries();
void drinks();
void desserts();

void registration(customer_detail customers[100]);
bool login(customer_detail customers[100]);

int main() {
    bool value1 = false;

    customer_detail customers[100];
    // Initializing the customers array
    for (int k = 0; k < 100; k++) {
        customers[k].name = "0";
        customers[k].email = "0";
        customers[k].password = "0";
        customers[k].address = "0";
    }

    cout << "* Welcome to Spicy Kitchen *" << endl;
    cout << "If you are an existing user, enter 'l' for login." << endl;
    cout << "If you don't have an account, enter 'r' for registration." << endl;

    char choice1;
    cin >> choice1;
    choice1 = toupper(choice1);

    switch (choice1) {
    case 'L':
        value1 = login(customers);
        break;
    case 'R':
        registration(customers);
        break;
    default:
        cout << "Invalid choice" << endl;
        break;
    }

    int choice2;
    if (value1 == true) {
        do {
            cout << "Login successful" << endl;
            displayMenu();
            cin >> choice2;

            switch (choice2) {
            case 1:
                burgers();
                break;
            case 2:
                fries();
                break;
            case 3:
                drinks();
                break;
            case 4:
                desserts();
                break;
            case 0:
                break; // Exit the loop when the user finishes ordering
            default:
                cout << "Enter a valid value" << endl;
                break;
            }

        } while (choice2 != 0);

        cout << "Total Price: Rs" << total_price << endl;

    } else {
    cout << "login unsucessful" << endl;
}
        return 0;
}

void registration(customer_detail customer[100]) {
    cout << "*REGISTRATION*" << endl;
    cout << "Enter your name: ";
    string customer_name;
    cin >> customer_name;

    cout << "Enter your email address: ";
    string customer_email;
    cin >> customer_email;

    cout << "Enter your password: ";
    string customer_password;
    cin >> customer_password;

    cout << "Enter your address: ";
    string customer_address;
    cin >> customer_address;

    for (int i = 0; i < 100; i++) {
        if (customer[i].name == "0") {
            customer[i].name = customer_name;
            customer[i].email = customer_email;
            customer[i].password = customer_password;
            customer[i].address = customer_address;
            cout << "Registration successful" << endl;
            break;
        }
    }
    login(customer);
}

bool login(customer_detail customer[100]) {
    bool value = false; // Initialize value to false

    cout << "*LOGIN*" << endl;
    cout << "Enter your name: " << endl;
    string login_name;
    cin >> login_name;

    cout << "Enter your password: " << endl;
    string login_password;
    cin >> login_password;

    for (int i = 0; i < 100; i++) {
        if (login_name == customer[i].name && login_password == customer[i].password) {
            value = true;
            break;
        }
        else if (login_name == customer[i].name   || login_password == customer[i].password) {
            value = false;
            

            break;
        }
    }

    return value;
}

void displayMenu() {
    cout << "* Menu **" << endl;
    cout << " ENTER 1 TO display burgers " << endl;
    cout << " ENTER 2 TO display fries " << endl;
    cout << " ENTER 3 TO display drinks " << endl;
    cout << " ENTER 4 TO display desserts " << endl;
    cout << " ENTER 0 TO finish ordering " << endl;
}

void burgers() {
    cout << "Burgers: " << endl;
    cout << "1. Chicken Burger                  Rs500" << endl;
    int chb = 500;
    cout << "2. Beef Burger                     Rs1000" << endl;
    int bb = 700;
    cout << "3. Spicy Chicken Burger            Rs600" << endl;
    int scb = 600;
    cout << "4. Fish-O-Fillet Burger            Rs400" << endl;
    int ffb = 400;

    int choice;
    do {
        cout << "Enter your choice burgers (0 to finish ordering): ";
        cin >> choice;

        switch (choice) {
        case 1:
            total_price += chb;
            break;
        case 2:
            total_price += bb;
            break;
        case 3:
   



