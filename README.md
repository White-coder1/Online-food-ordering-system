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
void burgers(order_detail orders[], int &orderCount);
void fries(order_detail orders[], int &orderCount);
void drinks(order_detail orders[], int &orderCount);
void desserts(order_detail orders[], int &orderCount);
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
                burgers(orders,orderCount);
                break;
            case 2:
                fries(orders,orderCount);
                break;
            case 3:
                drinks(orders,orderCount);
                break;
            case 4:
                desserts(orders,orderCount);
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
    cout << "Enter your password: ";
    string login_password;
    cin >> login_password;

    for (int i = 0; i < customerCount; ++i) {
        if (login_name == customers[i].name && login_password == customers[i].password) {
            loggedInCustomerIndex = i;
            break;
        }
    }

    if (loggedInCustomerIndex == -1) {
        cout << "Login unsuccessful" << endl;
        cout << "Exit program" << endl;
    }
    else {
        cout << "Login successful" << endl;
    }

    return loggedInCustomerIndex;
}


string getDeliveryOption() {
    cout << "Choose delivery option:" << endl;
    cout << "1. Pickup" << endl;
    cout << "2. Delivery" << endl;

    int option;
    cin >> option;

    return (option == 2) ? "Delivery" : "Pickup";
}

void generateReceipt(order_detail orders[], int orderCount, string deliveryOption, const customer_detail& customer) {
    cout << "\n** Receipt **\n";

    if (orderCount == 0) {
        cout << "No items ordered.\n";
    } else {
        cout << "Customer Name: " << customer.name << endl;
        cout << "Items Ordered: " << orderCount<<endl;
          cout << "Address: " << customer.address<<endl;
           cout << "order detail \n";
            for (int i = 0; i < orderCount; ++i) {
            cout << orders[i].quantity << "x " << orders[i].itemName << " - Rs" << orders[i].price * orders[i].quantity << endl;
        }
       
    }
    cout << "Delivery Option: " << deliveryOption << endl;
    cout << "Total Price: Rs" << total_price << endl;

}

void displayMenu() {
    cout << "* Menu **" << endl;
    cout << " ENTER 1 TO display burgers " << endl;
    cout << " ENTER 2 TO display fries " << endl;
    cout << " ENTER 3 TO display drinks " << endl;
    cout << " ENTER 4 TO display desserts " << endl;
    cout << " ENTER 0 TO finish ordering " << endl;
}

void burgers(order_detail orders[],int &ordercount) {
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
        case 1: {
            cout << "How many chicken burgers do you want? ";
            int num1;
            cin >> num1;
            orders[ordercount].itemName = "Chicken Burger";
            orders[ordercount].quantity = num1;
            orders[ordercount].price = chb * num1;

            total_price += orders[ordercount].price;
            ordercount += num1;
            break;
        }
        case 2: {
            cout << "How many beef burgers do you want? ";
            int num2;
            cin >> num2;
            orders[ordercount].itemName = "Beef Burger";
            orders[ordercount].quantity = num2;
            orders[ordercount].price = bb * num2;

            total_price += orders[ordercount].price;
            ordercount += num2;
            break;
            break;
        }
        case 3: {
            cout << "How many spicy chicken burgers do you want? ";
            int num3;
            cin >> num3;
         orders[ordercount].itemName = " Spicy Chicken Burger";
            orders[ordercount].quantity = num3;
            orders[ordercount].price = scb * num3;

            total_price += orders[ordercount].price;
            ordercount += num3;
            break;
        }
        case 4: {
            cout << "How many fish-o-fillet burgers do you want? ";
            int num4;
            cin >> num4;
           orders[ordercount].itemName = "fish-0-fillet Burger";
            orders[ordercount].quantity = num4;
            orders[ordercount].price = chb * num4;

            total_price += orders[ordercount].price;
            ordercount += num4;
            break;
        }
        }
    } while (choice != 0);
}
void fries(order_detail orders[],int &ordercount) {    // &ordercount means address of the variable in main/ it would make changes to the main variable too directly
    cout << "Fries: " << endl;
    cout << "1. Simple Fries      Rs350" << endl;
    int sf = 350;
    cout << "2. Curly Fries       Rs400" << endl;
    int cf = 400;
    cout << "3. Mayo Garlic Fries Rs500" << endl;
    int mgf = 500;

    int choice;
    do {
        cout << "Enter your choice in fries (0 to finish ordering): ";
        cin >> choice;

        switch (choice) {
        case 1: {
            cout << "How many simple fries do you want? ";
            int num1;
            cin >> num1;
         orders[ordercount].itemName = "simple fries";
            orders[ordercount].quantity = num1;
            orders[ordercount].price = sf * num1;

            total_price += orders[ordercount].price;
            ordercount += num1;
            break;
        }
        case 2: {
            cout << "How many curly fries do you want? ";
            int num2;
            cin >> num2;

                 orders[ordercount].itemName = "Curly Fries";
            orders[ordercount].quantity = num2;
            orders[ordercount].price = cf * num2;

            total_price += orders[ordercount].price;
            ordercount += num2;
            break;
        }
        case 3: {
            cout << "How many mayo garlic fries do you want? ";
            int num3;
            cin >> num3;
           orders[ordercount].itemName = "Mayo Garlic Fries";
            orders[ordercount].quantity = num3;
            orders[ordercount].price = mgf * num3;

            total_price += orders[ordercount].price;
            ordercount += num3;
            break;
        }
        }
    } while (choice != 0);
}

void drinks(order_detail orders[],int &ordercount) {
    cout << "Drinks: " << endl;
    cout << "1.Coca Cola         Rs200" << endl;
    int cc = 200;
    cout << "2.Sprite            Rs200" << endl;
    int spr = 200;
    cout << "3.Fanta             Rs200" << endl;
    int fant = 200;
    cout << "4.Mineral Water     Rs100" << endl;
    int mw = 100;
    cout << "5.Mint Margarita    Rs800" << endl;
    int mm = 800;
    cout << "6.Pina Colada       Rs800" << endl;
    int pc = 800;

    int choice;
    do {
        cout << "Enter your choice in drinks (0 to finish ordering): ";
        cin >> choice;

        switch (choice) {
        case 1: {
            cout << "How many coca colas do you want? ";
            int num1;
            cin >> num1;
             orders[ordercount].itemName = "Cola Cola ";
            orders[ordercount].quantity = num1;
            orders[ordercount].price = cc * num1;

            total_price += orders[ordercount].price;
            ordercount += num1;
            break;
        }
        case 2: {
            cout << "How many sprites do you want? ";
            int num2;
            cin >> num2;
            total_price += num2 * spr;
            ordercount += num2;
            break;
        }
        case 3: {
            cout << "How many fantas do you want? ";
            int num3;
            cin >> num3;
            total_price += num3 * fant;
            ordercount += num3;
            break;
        }
        case 4: {
            cout << "How many mineral waters do you want? ";
            int num4;
            cin >> num4;
            total_price += num4 * mw;
            ordercount += num4;
            break;
        }
        case 5: {
            cout << "How many mint margaritas do you want? ";
            int num5;
            cin >> num5;
            total_price += num5 * mm;
            ordercount += num5;
            break;
        }
        case 6: {
            cout << "How many pina coladas do you want? ";
            int num6;
            cin >> num6;
            total_price += num6 * pc;
            ordercount += num6;
            break;
        }
        }
    } while (choice != 0);
}

void desserts(order_detail orders[],int &ordercount) {
    cout << "Desserts: " << endl;
    cout << "1.Molten Lava Cake         Rs600" << endl;
    int mlc = 600;
    cout << "2.Lotus Cheese Cake        Rs650" << endl;
    int lcc = 650;
    cout << "3.Red Velvet Cake          Rs500 " << endl;
    int rvc = 500;
    cout << "4.Cookie Skillet           Rs999 " << endl;
    int cs = 999;
    cout << "5.Nutella Sundae           Rs350  " << endl;
    int ns = 350;

    int choice;
    do {
        cout << "Enter your choice in desserts (0 to finish ordering): ";
        cin >> choice;

        switch (choice) {
        case 1: {
            cout << "How many molten lava cakes do you want? ";
            int num1;
            cin >> num1;
            total_price += num1 * mlc;
            ordercount += num1;
            break;
        }
        case 2: {
            cout << "How many lotus cheese cakes do you want? ";
            int num2;
            cin >> num2;
            total_price += num2 * lcc;
            ordercount += num2;
            break;
        }
        case 3: {
            cout << "How many red velvet cakes do you want? ";
            int num3;
            cin >> num3;
            total_price += num3 * rvc;
            ordercount += num3;
            break;
        }
        case 4: {
            cout << "How many cookie skillets do you want? ";
            int num4;
            cin >> num4;
            total_price += num4 * cs;
            ordercount += num4;
            break;
        }
        case 5: {
            cout << "How many nutella sundaes do you want? ";
            int num5;
            cin >> num5;
            total_price += num5 * ns;
            ordercount += num5;
            break;
        }
        }

    } while (choice != 0);
}








