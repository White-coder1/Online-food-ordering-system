#include <iostream>
#include <string>

using namespace std;

const int MAX_CUSTOMERS = 1000;//
const int MAX_ORDERS = 1000;//

struct customer_detail {
    string name;
    string email;
    string password;
    string address;
};

struct order_detail {
    string itemName;
    int quantity;
    float price;
};

float total_price = 0.0;

void displayMenu();
void burgers(int& ordercount);
void fries(int& ordercount);
void drinks(int& ordercount);
void desserts(int& ordercount);
void generateReceipt(order_detail orders[], int orderCount, string deliveryOption, const customer_detail& customer);
int registration(customer_detail customers[], int& customerCount);
int login(customer_detail customers[], int customerCount);
string getDeliveryOption();

int main() {
    customer_detail customers[MAX_CUSTOMERS];
    order_detail orders[MAX_ORDERS];
    char choice1 = '0';
    int choice2 = 0;
    int customerCount = 0;
    int orderCount = 0;
    int loggedInCustomerIndex = 0;

    cout << "* Welcome to Spicy Kitchen *" << endl;
    cout << "If you are an existing user, enter 'l' for login." << endl;
    cout << "If you don't have an account, enter 'r' for registration." << endl;

    cin >> choice1;
    choice1 = tolower(choice1);
    while ((choice1 != 'r') && (choice1 != 'l')) {
        cout << "Invalid character. Enter again." << endl;
        cin >> choice1;
    }
    
    switch (choice1) {
    case 'l': {
        loggedInCustomerIndex = login(customers, customerCount);
        break;
    }
    case 'r': {
        loggedInCustomerIndex = registration(customers, customerCount);
        loggedInCustomerIndex = login(customers, customerCount);
        break;
    }
    default: {
        cout << "Invalid choice" << endl;
        break;
    }
    }
     
    bool ordering = true; // Flag to control ordering loop

    while (loggedInCustomerIndex != -1 && ordering) {
        do {
            
            displayMenu();
            cin >> choice2;

            switch (choice2) {
            case 1:
                burgers(orderCount);
                break;
            case 2:
                fries(orderCount);
                break;
            case 3:
                drinks(orderCount);
                break;
            case 4:
                desserts(orderCount);
                break;
            case 0:
                generateReceipt(orders, orderCount, getDeliveryOption(), customers[loggedInCustomerIndex]);
                ordering = false;//set the flag to exit the ordering loop.
                break;
            default:
                cout << "Enter a valid value" << endl;
                break;
            }

        } while (choice2 != 0 && ordering);
    }
    return 0;
}                      //main ends here
// function definitions
int registration(customer_detail customers[], int& customerCount) {
    cout << "REGISTRATION" << endl;
    customer_detail newCustomer;

    cout << "Enter your name: ";
    cin.ignore();
    getline(cin, newCustomer.name);

    cout << "Enter your email address: ";
    cin >> newCustomer.email;

    cout << "Enter your password: ";
    cin >> newCustomer.password;

    cout << "Enter your address: ";
    cin.ignore();
    getline(cin, newCustomer.address);

    if (customerCount < MAX_CUSTOMERS) {
        customers[customerCount++] = newCustomer;
        
        cout << "Registration successful" << endl;
        return customerCount - 1; // Return the index of the newly registered customer
    }
    else {
        cout << "Maximum number of customers reached" << endl;
        return -1; // Return -1 to indicate registration failure
    }
}

int login(customer_detail customers[], int customerCount) {
    int loggedInCustomerIndex = -1;

    cout << "LOGIN" << endl;
    cout << "Enter your name: ";
    string login_name;
    cin >> login_name;

}





