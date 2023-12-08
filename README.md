// Online-food-ordering-system

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
    char choice1;
    cin >> choice1;

    switch (choice1) {
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

int choice2;
    do {
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
void displayMenu() {
    cout << "*** Menu ****" << endl;
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


void fries(){

cout<<"Fries: "<<endl;
 
 cout<<"1. Simple Fries      Rs350"<<endl;
 int sf = 350;
 cout<<"2. Curly Fries       Rs400"<<endl;
 int cf = 400;
 cout<<"3. Mayo Garlic Fries Rs500"<<endl;
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

void drinks(){
    cout<<"Drinks: "<<endl;
 
 cout<<"1.Coca Cola         Rs200"<<endl;
 int cc=200;
 cout<<"2.Sprite            Rs200"<<endl;
 int spr=200;
 cout<<"3.Fanta             Rs200"<<endl;
 int fant=200;
 cout<<"4.Mineral Water     Rs100"<<endl;
 int mw=100;
 cout<<"5.Mint Margarita    Rs800"<<endl;
 int mm=800;
 cout<<"6.Pina Colada       Rs800"<<endl;
 int pc=800;
 
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
            total_price +=mw;
            break;
        case 5:
            total_price +=mm;
            break;
        case 6:
            total_price += pc;
            break;
                
        }
    } while (choice != 0);
}

void desserts(){
    cout<<"Desserts: "<<endl;
    
    cout<<"1.Molten Lava Cake         Rs600"<<endl;
    int mlc=600;
    cout<<"2.Lotus Cheese Cake        Rs650"<<endl;
    int icc=650;
    cout<<"3.Red Velvet Cake          Rs500 "<<endl;
    int rvc=500;
    cout<<"4.Cookie Skillet           Rs999 "<<endl;
    int cs=999;
    cout<<"5.Nutella Sundae           Rs350  "<<endl;
    int ns=350;

    int choice;
    do {
        cout << "Enter your choice in drinks (0 to finish ordering): ";
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
            total_price +=cs;
            break;
        case 5:
            total_price +=ns;
            break;
                
        }
    } while (choice != 0);
}
