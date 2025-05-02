#include <iostream>
#include <string>
#include <limits>


using namespace std;

const int MAX_TRIPS = 3; 
const int MAX_SEATS_PER_TRIP = 10;

struct Seat {
    bool isTaken;
    string passengerName;
};

void displayMenu() {
    cout << "\nSakarya Railways\n";
    cout << "1. Reserve a Seat\n";
    cout << "2. Cancel a Reservation\n";
    cout << "3. Exit\n";
}

void displayTrips() {
    cout << "Available Trips:\n";
    cout << "1. Istanbul\n";
    cout << "2. Ankara\n";
    cout << "3. Izmir\n";
}

int getValidChoice() {
    int choice;
    while (true) {
        cout << "Enter your choice: ";
        cin >> choice;

        if (cin.fail() || cin.peek() != '\n') {
            //  If the user did not enter a valid number
            cin.clear();   //Clear the error flag 
            cin.ignore(numeric_limits<streamsize>::max(), '\n');  // Discard invalid input
            cout << "Invalid input. Please enter a number.\n";
        }
        else {
            // It's a valid input!
            break;
        }
    }

    return choice;
}

void reserveSeat(Seat seats[MAX_TRIPS][MAX_SEATS_PER_TRIP]) {
    cout << "\nReserve a Seat\n";
    displayTrips();

    // Get user input for trip selection
    int tripNumber;
    do {
        cout << "Select Trip (1-" << MAX_TRIPS << "): ";
        tripNumber = getValidChoice();
    } while (tripNumber < 1 || tripNumber > MAX_TRIPS);

    // Check if all seats are taken for the selected trip
    bool allSeatsTaken = true;
    for (int i = 0; i < MAX_SEATS_PER_TRIP; ++i) {
        if (!seats[tripNumber - 1][i].isTaken) {
            allSeatsTaken = false;
            break;
        }
    }

     if (allSeatsTaken) {
        cout << "All seats are taken for Trip " << tripNumber << ". Cannot reserve more seats.\n";
        return;  // Exit the function if all seats are taken
    }


    // Display available seats for the selected trip
    cout << "\nAvailable Seats for Trip " << tripNumber << ":\n";
    for (int i = 0; i < MAX_SEATS_PER_TRIP; ++i) {
        if (!seats[tripNumber - 1][i].isTaken) {
            cout << i + 1 << ". Available\n";
        }
        else {
            cout << i + 1 << ". Taken by " << seats[tripNumber - 1][i].passengerName << "\n";
        }
    }

    // User input for seat number
    int seatNumber;
    do {
        cout << "Select Seat Number (1-" << MAX_SEATS_PER_TRIP << "): ";
        seatNumber = getValidChoice() - 1;

        if (seatNumber < 0 || seatNumber >= MAX_SEATS_PER_TRIP || seats[tripNumber - 1][seatNumber].isTaken) {
            cout << "Invalid selection. Please enter a valid seat number.\n";
        }

    } while (seatNumber < 0 || seatNumber >= MAX_SEATS_PER_TRIP || seats[tripNumber - 1][seatNumber].isTaken);

    // Passenger Name
    string passengerName;
    do {
        cout << "Enter Passenger Name: ";
        getline(cin,passengerName); //was cin>> passengerName;
    } while (passengerName.empty());

    // Reserve the seat for the selected trip
    seats[tripNumber - 1][seatNumber].isTaken = true;
    seats[tripNumber - 1][seatNumber].passengerName = passengerName;

    cout << "Seat reserved successfully for " << passengerName << " on Trip " << tripNumber << "!\n";
}

void cancelReservation(Seat seats[MAX_TRIPS][MAX_SEATS_PER_TRIP]) {
    cout << "\nCancel a Reservation\n";
    displayTrips();

    // Get user input for trip selection
    int tripNumber;
    do {
        cout << "Select Trip (1-" << MAX_TRIPS << "): ";
        tripNumber = getValidChoice();
    } while (tripNumber < 1 || tripNumber > MAX_TRIPS);

    // Display available seats for the selected trip
    cout << "\nAvailable Seats for Trip " << tripNumber << ":\n";
    bool anySeatTaken = false;  // Flag to check if any seat is taken

    for (int i = 0; i < MAX_SEATS_PER_TRIP; ++i) {
        if (seats[tripNumber - 1][i].isTaken) {
            anySeatTaken = true;
            cout << i + 1 << ". Taken by " << seats[tripNumber - 1][i].passengerName << "\n";
        }
    }

    if (!anySeatTaken) {
        cout << "No available seats to cancel for Trip " << tripNumber << ".\n";
        return;  // Exit the function if no seats are taken
    }

    // Get user input for seat number to cancel
    int seatNumber;
    do {
        cout << "Select Seat Number to Cancel (1-" << MAX_SEATS_PER_TRIP << "): ";
        seatNumber = getValidChoice() - 1;

        if (seatNumber < 0 || seatNumber >= MAX_SEATS_PER_TRIP || !seats[tripNumber - 1][seatNumber].isTaken) {
            cout << "Invalid selection. Please enter a valid seat number.\n";
        }

    } while (seatNumber < 0 || seatNumber >= MAX_SEATS_PER_TRIP || !seats[tripNumber - 1][seatNumber].isTaken);

    // Cancel the reservation for the selected trip
    cout << "Canceled reservation for " << seats[tripNumber - 1][seatNumber].passengerName
        << " on Trip " << tripNumber << "!\n";
    seats[tripNumber - 1][seatNumber].isTaken = false;
    seats[tripNumber - 1][seatNumber].passengerName = "";
}

int main() {
    Seat seats[MAX_TRIPS][MAX_SEATS_PER_TRIP] = { 0 }; // Initialize seats to not taken

    int choice;
    do {
        displayMenu();
        choice = getValidChoice();

        switch (choice) {
        case 1:
            reserveSeat(seats);
            break;
        case 2:
            cancelReservation(seats);
            break;
        case 3:
            cout << "Exiting the program. Goodbye!\n";
            break;
        default:
            cout << "Invalid choice. Please try again.\n";
        }

    } while (choice != 3);

    return 0;
}
