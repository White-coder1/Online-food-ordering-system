# Online-food-ordering-system

#include <iostream>
#include <string>
using namespace std;

struct customer_detail {
    string name;
    string email;
    string password;
    string address;
};

customer_detail customers[10000];

void registration();
void login();
void displayUsers();  // Added function to display user details

int main() {
    // Initializing the customers array
    for (int k = 0; k < 10000; k++) {
        customers[k].name = "0";
        customers[k].email = "0";
        customers[k].password = "0";
        customers[k].address = "0";
    }

    cout << "* Welcome to Spicy Kitchen *" << endl;
    cout << "If you are an existing user, enter 'l' for login." << endl;
    cout << "If you don't have an account, enter 'r' for registration." << endl;
    char choice;
    cin >> choice;

    switch (choice) {
    case 'l':
        login();
        break;
    case 'r':
        registration();
        break;
    default:
        cout << "Invalid choice" << endl;
        break;
    }
    displayUsers();  // Display users after login or registration
    return 0;
}

void registration() {
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

    for (int i = 0; i < 10000; i++) {
        if (customers[i].name == "0") {
            customers[i].name = customer_name;
            customers[i].email = customer_email;
            customers[i].password = customer_password;
            customers[i].address = customer_address;
            cout << "Registration successful" << endl;
            return;
        }
    }
    cout << "Customer database is full. Cannot register." << endl;
}

void login() {
    cout << "Enter your name: ";
    string login_name;
    cin >> login_name;

    cout << "Enter your password: ";
    string login_password;
    cin >> login_password;

    for (int i = 0; i < 10000; i++) {
        if (login_name == customers[i].name &&  login_password == customers[i].password) {
            cout << "Login successful" << endl;
            return;
        }
    }

    cout << "User not found or incorrect password. Please register or try again." << endl;
}

void displayUsers() {
    cout << "User details:" << endl;
    for (int i = 0; i < 10000; i++) {
        if (customers[i].name != "0") {
            cout << "Name: " << customers[i].name << ", Email: " << customers[i].email << ", Address: " << customers[i].address << endl;
        }
    }
}




