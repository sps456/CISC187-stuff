## Activity 10: Graphs
1. This is my theoretical graph:
<img width="761" height="687" alt="image" src="https://github.com/user-attachments/assets/e2e0c2a5-39ba-45cf-93bd-7baefacf1725" />

2. Here is a simple implementation of a Graph class in which I created the graph drawn in part 1, then had it search for data contained at node K using both a Bredth First Search and a Depth First Search:

Code:
```c++
#include <iostream>
#include <stack>
#include <queue>
#include <set>
using namespace std;

class Node
{
private:
    string name;
    int data;
    vector<Node*> adjacents;
public:
    Node(string n, int d);
    Node();
    void addConnection(Node* n);
    string getName();
    const int getData();
    vector<Node*> getAdjacents();
};

class Graph
{
private:
    Node* root;

public:
    Graph(Node* startNode);
    void connect(Node& a, Node& b);
    void BFS(int searchData);
    void DFS(int searchData);
};

Node::Node(string n, int d) {
    name = n;
    data = d;
}

Node::Node() {

}

void Node::addConnection(Node* n) {
    this->adjacents.push_back(n);
}

string Node::getName() {
    return name;
}

const int Node::getData() {
    return data;
}

vector<Node*> Node::getAdjacents() {
    return adjacents;
}

Graph::Graph(Node* startNode) {
    root = startNode;
}

void Graph::connect(Node& a, Node& b) {
    a.addConnection(&b);
    b.addConnection(&a);
}

void Graph::BFS(int searchData) {
    int checks = 0;
    Node currentNode;
    vector<Node*> currentV;
    set<Node*> discovered;
    queue<Node*> frontierQueue;
    frontierQueue.push(root);
    discovered.insert(root);
    while (!frontierQueue.empty()) {
        currentNode = *frontierQueue.front();
        frontierQueue.pop();
        checks++;
        if (currentNode.getData() == searchData) {
           cout << "data found at node " << currentNode.getName() << " taking " << checks << " steps" << endl;
           break;
        }
        currentV = currentNode.getAdjacents();
        for (int i = 0; i < currentV.size(); i++) {
            if (!discovered.count(currentV.at(i))) {
                frontierQueue.push(currentV.at(i));
                discovered.insert(currentV.at(i));
            }
        }
    }
}

void Graph::DFS(int searchData) {
    int checks = 0;
    Node currentNode;
    vector<Node*> currentV;
    set<Node*> discovered;
    stack<Node*> frontierStack;
    frontierStack.push(root);
    discovered.insert(root);
    while (!frontierStack.empty()) {
        currentNode = *frontierStack.top();
        frontierStack.pop();
        checks++;
        if (currentNode.getData() == searchData) {
            cout << "data found at node " << currentNode.getName() << " taking " << checks << " steps" << endl;
            break;
        }
        currentV = currentNode.getAdjacents();
        for (int i = 0; i < currentV.size(); i++) {
            if (!discovered.count(currentV.at(i))) {
                frontierStack.push(currentV.at(i));
                discovered.insert(currentV.at(i));
            }
        }
    }
}


int main()
{
    Node A("A", 0);
    Node B("B", 0);
    Node C("C", 0);
    Node D("D", 0);
    Node E("E", 0);
    Node F("F", 0);
    Node G("G", 0);
    Node H("H", 0);
    Node I("I", 0);
    Node J("J", 0);
    Node K("K", 1);
    Graph web(&A);
    web.connect(A, B);
    web.connect(A, C);
    web.connect(A, D);
    web.connect(A, E);
    web.connect(A, F);
    web.connect(B, G);
    web.connect(C, H);
    web.connect(D, I);
    web.connect(E, J);
    web.connect(F, K);
    web.BFS(1);
    web.DFS(1);
    return 0;
}
```
Output:
<img width="448" height="57" alt="image" src="https://github.com/user-attachments/assets/a68b2074-6841-4f60-8e71-e114f3b258b0" />

3. Despite the vastly different number of steps in this instance, both BFS and DFS have the same big O time complexities of O(V + E) where V is the number of vertices and E is the number of edges. In the worst case of both situations, every node will be searched so they will have the same worst case time complexity. Depending on the structure of the graph their space complexities may differ, but in terms of time complexity it will mostly come down to preference for unweighted graphs.  
