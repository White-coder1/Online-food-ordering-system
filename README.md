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
       



