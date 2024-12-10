#include <iostream>
using namespace std;

class Cqueue {
public: 
    int* queue;
    int size;
    int front;
    int rear;
    int capacity;

    Cqueue(int capacity) {
        this->capacity = capacity;
        size = 0;
        front = -1;
        rear = -1;
        queue = new int[capacity];
    }

    bool isfull() {
        return size == capacity;
    }

    bool isempty() {
        return size == 0;
    }

    void enqueue(int x) {
        if (isfull()) {
            cout << "Queue is already full!" << endl;
            return;
        }
        
        if (isempty()) {
            front = 0;
        }
        
        rear = (rear + 1) % capacity;
        queue[rear] = x;
        size++;
    }

    void remove() {
        if (isempty()) {
            cout << "Queue is empty!" << endl;
            return;
        }

        // Print the element being removed
        cout << queue[front] << " dequeued from queue" << endl;

        // If only one element is left
        if (size == 1) {
            front = -1;
            rear = -1;
        } else {
            // Move front to next position circularly
            front = (front + 1) % capacity;
        }
        
        // Decrease size
        size--;
    }

    void display() {
        if (isempty()) {
            cout << "Queue is empty!" << endl;
            return;
        }

        int current = front;
        for (int count = 0; count < size; count++) {
            cout << queue[current] << " ";
            current = (current + 1) % capacity;
        }
        cout << endl;
    }

    int peek() {
        if (isempty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        return queue[front];
    }

    // Destructor to free dynamically allocated memory
    ~Cqueue() {
        delete[] queue;
    }
};

int main() {
    int capacity, choice, value;
    cout << "Enter the capacity of the circular queue: ";
    cin >> capacity;
    Cqueue q(capacity);
    
    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Enqueue\n";
        cout << "2. Dequeue\n";
        cout << "3. Peek\n";
        cout << "4. Display\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1:
                cout << "Enter the value to enqueue: ";
                cin >> value;
                q.enqueue(value);
                break;
            case 2:
                q.remove();
                break;
            case 3:
                value = q.peek();
                if (value != -1) 
                    cout << "Front element: " << value << endl;
                break;
            case 4:
                q.display();
                break;
            case 5:
                cout << "Exiting program..." << endl;
                return 0;
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }
}