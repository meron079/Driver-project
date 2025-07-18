#include <iostream>
#include <string>
using namespace std;

struct Driver {
    int id;
    string fname, lname;
    string licenseNo;
    string licenseExpiry;
};

const int MAX = 100;
Driver drivers[MAX];
int n = 0;

void addDriver() {
    Driver d;
    cout << "ID: "; cin >> d.id;
    cout << "First name: "; cin >> d.fname;
    cout << "Last name: "; cin >> d.lname;
    cout << "License Number: "; cin >> d.licenseNo;
    cout << "License Expiry (YYYY-MM-DD): "; cin >> d.licenseExpiry;
    drivers[n++] = d;
}

void showAll() {
    for(int i = 0; i < n; i++) {
        cout << "ID: " << drivers[i].id << ", "
             << "Name: " << drivers[i].fname << " " << drivers[i].lname << ", "
             << "License No: " << drivers[i].licenseNo << ", "
             << "Expiry: " << drivers[i].licenseExpiry << "\n";
    }
}

int findByID(int id) {
    for(int i = 0; i < n; i++) {
        if(drivers[i].id == id) return i;
    }
    return -1;
}

void updateDriver() {
    int id;
    cout << "Enter Driver ID to update: ";
    cin >> id;
    int idx = findByID(id);
    if(idx == -1) {
        cout << "Driver not found.\n";
        return;
    }
    cout << "New License Number: ";
    cin >> drivers[idx].licenseNo;
    cout << "New License Expiry (YYYY-MM-DD): ";
    cin >> drivers[idx].licenseExpiry;
}

void deleteDriver() {
    int id;
    cout << "Enter Driver ID to delete: ";
    cin >> id;
    int idx = findByID(id);
    if(idx == -1) {
        cout << "Driver not found.\n";
        return;
    }
    for(int i = idx; i < n - 1; i++) {
        drivers[i] = drivers[i + 1];
    }
    n--;
}

int main() {
    int choice;
    do {
        cout << "\nDriver Management System\n";
        cout << "1. Add Driver\n";
        cout << "2. Show All Drivers\n";
        cout << "3. Update Driver\n";
        cout << "4. Delete Driver\n";
        cout << "0. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: addDriver(); break;
            case 2: showAll(); break;
            case 3: updateDriver(); break;
            case 4: deleteDriver(); break;
            case 0: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice.\n";
        }
    } while(choice != 0);

    return 0;
}
