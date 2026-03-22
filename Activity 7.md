## Activity 7: Linked-lists
# Reflection Questions
1. A linked list is very efficient for stack implementation because the nature of a stack negates the poor time efficiencies for searching and interacting with a list at the end/middle. Linked lists are very fast at inserting and reading elements from the first node of the list, but they are less efficient at searching for elements deep in the list since you have to travel from one node to the next. In a stack however you only ever need to interact with the list from the top of the stack, meaning you get all the benefits of super efficient insertion and deletion without having to worry about the downsides normally associated with singly linked lists.
2. The push and pop operations both have time complexities of O(1) because they never have to search for an item to remove or make space for an item to add. No matter what you add or remove, it will always only take one step.
3. If memory isn't deallocated after pop, the data will just sit there unused and unlinked to the list until the garbage collector eventually dumps it. Depending on the IDE, this could take a while so if you have a lot of rapid adding and deleting operations without properly deallocating your data, that buildup of wasted memory could cause issues for you.
4. A stack implemented with an array would be far slower at inserting new values since arrays always have a fixed size. You would start with a certain size array, but once you fill it up you would need to create a larger array and move all of the elements into this new array to add more values on top of it. This added cost would come with no benefits, because a stack structure will never make use of an array's ability to add and remove data at any location. For this reason a linked list is far more efficient for stack implementation.
# Code
``` c++
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* next;
};

class Stack
{
private:
    Node* top;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};

Stack::Stack() {
    top = nullptr;
}

void Stack::push(int value) {
    Node* n = new Node{ value,top };
    top = n;
}

void Stack::pop() {
    if (!this->isEmpty()) {
        Node* temp = top;
        top = top->next;
        delete temp;
    }
    else {
        cout << "Stack Underflow\n";
    }
}

int Stack::peek() {
    return top->data;
}

bool Stack::isEmpty() {
    if (top == nullptr) {
        return true;
    }
    else {
        return false;
    }
}

void Stack::display() {
    Node* n = top;
    cout << "Stack elements:\n";
    while (n != nullptr) {
        cout << n->data << endl;
        n = n->next;
    }
}

int main()
{
    Stack s;

    s.pop();
    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);
    cout << "Top element: " << s.peek() << endl;
    s.display();
    s.pop();
    cout << "Top element: " << s.peek() << endl;
    s.display();

    return 0;
}
```
