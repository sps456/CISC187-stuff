## Activity 8: Binary Search Trees
1. Binary Tree Diagram
  <img width="265" height="367" alt="image" src="https://github.com/user-attachments/assets/84fe8f95-d4fd-4e62-94ce-58257ea89f9b" />

2. Searching a well balanced binary search tree takes O(log N) so it will take approximately log_2(1000) steps to search for the deepest (lowest level) value within it, which equals about 10 steps. This is the maximum amount of steps to search for a value within the tree since any value located on a higher level would be found before this.
3. The largest value contained within a binary search tree will be the deepest value along the far right of the tree, so our algorithm will look something like this in pseudocode:
```
node equals rootNode
while(node.right doesnt equal nothing)
  node equals node.right
print "the largest value is " node
```
4. BinarySearchTree implementation with insert
``` c++
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* right = nullptr;
    Node* left = nullptr;
};

class BinarySearchTree
{
private:
    Node* root;

public:
    BinarySearchTree(int value);
    void insert(int val);
};

BinarySearchTree::BinarySearchTree(int value) {
    Node* n = new Node;
    n->data = value;
    root = n;
}
void BinarySearchTree::insert(int val) {
    Node* searchNode = root;
    bool cont = true;
    while (cont) {
        if (val > searchNode->data) {
            if (searchNode->right != nullptr) {
                searchNode = searchNode->right;
            }
            else {
                Node* n = new Node;
                n->data = val;
                searchNode->right = n;
                cont = false;
            }
        }
        else if (val < searchNode->data) {
            if (searchNode->left != nullptr) {
                searchNode = searchNode->left;
            }
            else {
                Node* n = new Node;
                n->data = val;
                searchNode->left = n;
                cont = false;
            }
        }
        else {
            cout << "This data point already exists in the tree" << endl;
            cont = false;
        }
    }
}

int main()
{
    BinarySearchTree T(1);
    T.insert(5);
    T.insert(9);
    T.insert(2);
    T.insert(4);
    T.insert(10);
    T.insert(6);
    T.insert(3);
    T.insert(8);
    cout << " The Tree Has Been Created" << endl;
    return 0;
}
```
