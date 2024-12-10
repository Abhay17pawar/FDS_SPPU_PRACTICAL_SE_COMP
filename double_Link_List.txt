#include <iostream>
#include <cmath>
using namespace std;

// Definition of the Node for Doubly Linked List
class Node {
public:
    int data;
    Node* prev;
    Node* next;
    Node(int data) : data(data), prev(nullptr), next(nullptr) {}
};

// Class for managing the Doubly Linked List and binary number operations
class BinaryNumber {
public:
    Node* head;
    Node* tail;

    BinaryNumber() : head(nullptr), tail(nullptr) {}

    // Function to insert a binary digit at the front (for original binary representation)
   void insertDigit(int digit) {
    Node* newNode = new Node(digit);
    if (!head) {
        head = tail = newNode; // If the list is empty, both head and tail point to the new node
    } else {
        newNode->next = head; // New node points to current head
        head = newNode; // Head now points to the new node
    }
}


    // Function to print the binary number (in original order)
    void printBinary() {
        Node* temp = head;
        while (temp) {
            cout << temp->data;
            temp = temp->next;
        }
        cout << endl;
    }

    // Function to convert binary number to decimal
    int toDecimal() {
        int decimalValue = 0;
        int power = 0;
        Node* temp = head;
        while (temp) {
            decimalValue += temp->data * pow(2, power);
            power++;
            temp = temp->next;
        }
        return decimalValue;
    }

    // Function to convert decimal to binary and store in the linked list
    void fromDecimal(int decimalValue) {
        if (decimalValue == 0) {
            insertDigit(0);  // Special case for 0
            return;
        }
        while (decimalValue > 0) {
            insertDigit(decimalValue % 2);
            decimalValue /= 2;
        }
    }

    // Function to add two binary numbers
    BinaryNumber addBinary(BinaryNumber& other) {
        int decimal1 = this->toDecimal();
        int decimal2 = other.toDecimal();
        int sum = decimal1 + decimal2;

        BinaryNumber result;
        result.fromDecimal(sum);
        return result;
    }
};

// Main function to demonstrate adding two binary numbers
int main() {
    BinaryNumber bin1, bin2;

    // Input first binary number
    cout << "Enter the first binary number (from most significant bit to least significant bit): ";
    string binary1;
    cin >> binary1;
    for (char c : binary1) {
        bin1.insertDigit(c - '0');
    }

    // Input second binary number
    cout << "Enter the second binary number (from most significant bit to least significant bit): ";
    string binary2;
    cin >> binary2;
    for (char c : binary2) {
        bin2.insertDigit(c - '0');
    }

    // Add the two binary numbers
    BinaryNumber result = bin1.addBinary(bin2);

    // Print the result
    cout << "Sum of the binary numbers: ";
    result.printBinary();

    return 0;
}