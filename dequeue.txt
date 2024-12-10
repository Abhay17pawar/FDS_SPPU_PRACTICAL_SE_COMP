#include <iostream>
using namespace std;

class Deque {
private:
    int* arr;
    int front;
    int rear;
    int capacity;
    int size;

public:
    // Constructor to initialize the deque
    Deque(int cap) {
        capacity = cap;
        arr = new int[capacity];
        front = -1;
        rear = -1;
        size = 0;
    }

    // Destructor to clean up dynamic memory
    ~Deque() {
        delete[] arr;
    }

    // Check if the deque is empty
    bool isEmpty() {
        return size == 0;
    }

    // Check if the deque is full
    bool isFull() {
        return size == capacity;
    }

    // Insert at the front of the deque
    void enqueueFront(int value) {
        if (isFull()) {
            cout << "Deque is full! Cannot insert at front." << endl;
            return;
        }
        if (front == -1) { // If deque is empty
            front = 0;
            rear = 0;
        } else {
            front = (front - 1 + capacity) % capacity; // Circular move
        }
        arr[front] = value;
        size++;
        cout << value << " inserted at front." << endl;
    }

    // Insert at the rear of the deque
    void enqueueRear(int value) {
        if (isFull()) {
            cout << "Deque is full! Cannot insert at rear." << endl;
            return;
        }
        if (front == -1) { // If deque is empty
            front = 0;
            rear = 0;
        } else {
            rear = (rear + 1) % capacity; // Circular move
        }
        arr[rear] = value;
        size++;
        cout << value << " inserted at rear." << endl;
    }

    // Remove from the front of the deque
    void dequeueFront() {
        if (isEmpty()) {
            cout << "Deque is empty! Cannot remove from front." << endl;
            return;
        }
        cout << arr[front] << " removed from front." << endl;
        if (front == rear) { // If there is only one element left
            front = -1;
            rear = -1;
        } else {
            front = (front + 1) % capacity; // Circular move
        }
        size--;
    }

    // Remove from the rear of the deque
    void dequeueRear() {
        if (isEmpty()) {
            cout << "Deque is empty! Cannot remove from rear." << endl;
            return;
        }
        cout << arr[rear] << " removed from rear." << endl;
        if (front == rear) { // If there is only one element left
            front = -1;
            rear = -1;
        } else {
            rear = (rear - 1 + capacity) % capacity; // Circular move
        }
        size--;
    }

    // Get the front element of the deque
    int peekFront() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return arr[front];
    }

    // Get the rear element of the deque
    int peekRear() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return arr[rear];
    }

    // Display the elements of the deque
    void display() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return;
        }
        cout << "Deque elements: ";
        int i = front;
        while (i != rear) {
            cout << arr[i] << " ";
            i = (i + 1) % capacity; // Circular move
        }
        cout << arr[rear] << endl; // Last element
    }
};

int main() {
    int capacity, choice, value;

    cout << "Enter the capacity of the deque: ";
    cin >> capacity;

    Deque dq(capacity);

    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Enqueue Front\n";
        cout << "2. Enqueue Rear\n";
        cout << "3. Dequeue Front\n";
        cout << "4. Dequeue Rear\n";
        cout << "5. Peek Front\n";
        cout << "6. Peek Rear\n";
        cout << "7. Display\n";
        cout << "8. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
	if (choice == 1) {
            cout << "Enter the value to enqueue at front: ";
            cin >> value;
            dq.enqueueFront(value);
        }
        else if (choice == 2) {
            cout << "Enter the value to enqueue at rear: ";
            cin >> value;
            dq.enqueueRear(value);
        }
        else if (choice == 3) {
            dq.dequeueFront();
        }
        else if (choice == 4) {
            dq.dequeueRear();
        }
        else if (choice == 5) {
            cout << "Front element: " << dq.peekFront() << endl;
        }
        else if (choice == 6) {
            cout << "Rear element: " << dq.peekRear() << endl;
        }
        else if (choice == 7) {
            dq.display();
        }
        else if (choice == 8) {
            cout << "Exiting program..." << endl;
            break;
        }
        else {
            cout << "Invalid choice! Please try again." << endl;
        }
    }

    return 0;
}