// online food odering system
#include <iostream>
#include <string>
using namespace std;
//add login unsucessful condition to int main
//receipt function
//ask user to choose between pick up or delivery
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

float total_price = 0; // Initialize total_price

void displayMenu();
void burgers(int &ordercount);
void fries(int &ordercount);
void drinks(int &ordercount);
void desserts(int &ordercount);
void generateReceipt(order_detail orders[], int orderCount, string deliveryOption, const customer_detail& customer);
int registration(customer_detail customers[], int& customerCount);
int login(customer_detail customers[], int customerCount);
string getDeliveryOption();


void registration(customer_detail customers[100]);  //// should be removed
bool login(customer_detail customers[100]);         //// should be removed

int main() {
    bool value1 = false;

    customer_detail customers[100];
    // Initializing the customers info array
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
    choice1 = tolower(choice1);
    while(choice1 != 'r' && choice1 != 'l'){
    cout<<"Invalid character.Enter again."<<endl;
    cin>>choice1;
    }
    switch (choice1) {
    case 'l':{
        loggedInCustomerIndex = login(customers, customerCount);
        break;
		}
    case 'r':{
        loggedInCustomerIndex = registration(customers, customerCount);
        break;
		}
    default:{
        cout << "Invalid choice" << endl;
        break;
		}
    }
    switch (choice1) {   //// remove as well
    case 'l':
        value1 = login(customers);
        break;
    case 'r':
        registration(customers);
        break;
    default:
        cout << "Invalid choice" << endl;
        break;
    }

    int choice2;
    do {
      do{
            cout << "Login successful" << endl;
            displayMenu();
            cin >> choice2;

            switch (choice2) {
            case 1:
                burgers();        /// add &ordercount in ()
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
            generateReceipt(orders, orderCount, getDeliveryOption(), customers[loggedInCustomerIndex]);
            break;
            default:
                cout << "Enter a valid value" << endl;
                break;
            }

        } while (choice2 != 0);

        cout << "Total Price: Rs" << total_price << endl;
} while(value1==true);

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
        /*for (int i = 0; i < orderCount; ++i) {
            cout << orders[i].quantity << "x " << orders[i].itemName << " - Rs" << orders[i].price * orders[i].quantity << endl;
        }*/
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
               total_price += scb;
            break;
        case 4:
            total_price += ffb;
            break;
        }
    } while (choice != 0);
}
void fries() {
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
        case 1:
            total_price += sf;
            break;
        case 2:
            total_price += cf;
            break;
        case 3:
            total_price += mgf;
            break;
        }
    } while (choice != 0);
}

void drinks() {
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
        case 1:
            total_price += cc;
            break;
        case 2:
            total_price += spr;
            break;
        case 3:
            total_price += fant;
            break;
        case 4:
            total_price += mw;
            break;
        case 5:
            total_price += mm;
            break;
        case 6:
            total_price += pc;
            break;
        }
    } while (choice != 0);
}

void desserts() {
    cout << "Desserts: " << endl;
    cout << "1.Molten Lava Cake         Rs600" << endl;
    int mlc = 600;
    cout << "2.Lotus Cheese Cake        Rs650" << endl;
    int icc = 650;
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
        case 1:
            total_price += mlc;
            break;
        case 2:
            total_price += icc;
            break;
        case 3:
            total_price += rvc;
            break;
        case 4:
            total_price += cs;
            break;
        case 5:
            total_price += ns;
            break;
        }

    } while (choice != 0);
}




