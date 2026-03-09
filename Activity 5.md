## Activity 5: Hash Tables
You can see my direct findings recorded in the video explanation, but the gist of it is that the random string hash table had the highest average and max bucket size, followed by the sequential string hash table, and finally the shared prefix hash table which had the lowest average bucket size. This most likely has to do with the way that the hashing function we chose works, and it might be different if we used an alternate hashing function. Another interesting data point is that despite being having the lowest final average bucket size, the shared prefix hash table actually had a higher total number of collision than the sequential one. I don't exactly know why this is, but its a neat quirk of the way hash tables opperate. It makes sense to me that the random strings ended up having the highest max bucket count, but its a little surprising that it is twice as large as the other twos highest bucket count (random was 4, the other ones were both 2). Overall this assignment took a very long time, but I found the process of developing the hash table to be very interesting. 

Video Explanation of Assignment: https://drive.google.com/file/d/14s50ZDOLoVNDyKLpU5DUTXWqymXbwr2v/view?usp=sharing 

Code:
```c++
#include <vector>
#include <list>
#include <string>
#include <iostream>
#include <random>
using namespace std;

class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;
    int totalCollisions;

    int hashFunction(const string& key) const;
    void rehash();

public:
    HashTable(int size = 11);

    void insert(const string& key, int value);
    bool remove(const string& key);
    int search(const string& key) const;
    double loadFactor() const;
    int size() const { return currentSize; }
    bool isEmpty() const;
    void printTable() const;
    int getCapacity() const { return capacity; }
    int getTotalCollisions() const { return totalCollisions; }
    int getCollisionCount() const { return collisionCount; }
    int maxBucketSize() const;
    double averageBucketSize() const;
};

HashTable::HashTable(int size) {
    vector<list<pair<string, int>>> v(size);
    table = v;
    capacity = size;
    currentSize = 0;
    collisionCount = 0;
    totalCollisions = 0;
}

int HashTable::hashFunction(const string& key) const {
    const int prime = 31;
    long long hash = 0;

    for (char c : key) {
        hash = hash * prime + c;
    }

    return hash % capacity;
}

void HashTable::insert(const string& key, int value) {
    int index = hashFunction(key);
    pair<string, int> p(key, value);
    if (!table[index].empty()) {
        collisionCount++;
    }
    table[index].push_back(p);
    currentSize++;
    if (this->loadFactor() > .75) {
        this->rehash();
    }
}

bool HashTable::remove(const string& key) {
    int index = hashFunction(key);
    for (auto i = table[index].begin(); i != table[index].end(); i++) {
        if (i->first == key) {
            table[index].erase(i);
            return true;
        }
    }
    return false;
}

int HashTable::search(const string& key) const {
    int index = hashFunction(key);
    for (auto i = table[index].begin(); i != table[index].end(); i++) {
        if (i->first == key) {
            return i->second;
        }
    }
    return -1;
}

double HashTable::loadFactor() const {
    return (double)currentSize / (double)capacity;
}

bool HashTable::isEmpty() const {
    bool ret = true;
    for (int i = 0; i < table.size(); i++) {
        if (!table[i].empty()) {
            ret = false;
            break;
        }
    }
    return ret;
}

void HashTable::rehash() {
    vector<list<pair<string, int>>> v(capacity * 2);
    int collisions = 0;
    for (int i = 0; i < table.size(); i++) {
        for (auto it = table[i].begin(); it != table[i].end(); it++) {            
            pair<string, int> p = *it;
            int index = hashFunction(p.first);
            if (!v[index].empty()) {
                collisions++;
            }
            v[index].push_back(p);
        }
    }
    table = v;
    capacity *= 2;
    totalCollisions += collisionCount;
    collisionCount = collisions;
}

void HashTable::printTable() const {
    for (int i = 0; i < table.size(); i++) {
        for (auto it = table[i].begin(); it != table[i].end(); it++) {
            cout << "[" << it->first << "," << it->second << "]" << endl;
        }
    }
}

int HashTable::maxBucketSize() const {
    int max = -1;
    for (int i = 0; i < table.size(); i++) {
            if ((int)table[i].size() > max) {
                max = table[i].size();
            }
    }
    return max;
}

double HashTable::averageBucketSize() const {
    double bucketCount = 0;
    for (int i = 0; i < table.size(); i++) {
        if (!table[i].empty()) {
            bucketCount++;
        }
    }
    return (double)currentSize / bucketCount;
}

int main() {
    cout << "Testing Hash Table with random strings" << endl;
    HashTable r;
    static const char alphanum[] =
        "0123456789"
        "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        "abcdefghijklmnopqrstuvwxyz";
    
    for (int i = 0; i < 100; i++) {
        string s = "";
        for (int j = 0; j < rand() % 15 + 1; j++) {
            s += alphanum[rand() % 62];
        }
        r.insert(s, i);
    }
    cout << "RANDOM STRING HASH INFO:" << endl;
    cout << "Capacity: " << r.getCapacity() << endl;
    cout << "Number of elements: " << r.size() << endl;
    cout << "Load Factor: " << r.loadFactor() << endl;
    cout << "Total collisions: " << r.getTotalCollisions() << endl;
    cout << "Max bucket size: " << r.maxBucketSize() << endl;
    cout << "Average bucket size: " << r.averageBucketSize() << endl;
    
    cout << endl << "Testing Hash Table with sequential strings" << endl;
    HashTable seq;
    for (int i = 0; i < 100; i++) {
        string str = "student" + to_string(i);
        seq.insert(str, i);
    }
    cout << "SEQUENTIAL STRING HASH INFO:" << endl;
    cout << "Capacity: " << seq.getCapacity() << endl;
    cout << "Number of elements: " << seq.size() << endl;
    cout << "Load Factor: " << seq.loadFactor() << endl;
    cout << "Total collisions: " << seq.getTotalCollisions() << endl;
    cout << "Max bucket size: " << seq.maxBucketSize() << endl;
    cout << "Average bucket size: " << seq.averageBucketSize() << endl;

    cout << endl << "Testing Hash Table with same prefix strings" << endl;
    HashTable prefix;
    for (int i = 0; i < 100; i++) {
        string str;
        if (i / 10 == 0) {
            str = "data_000" + to_string(i);
        }
        else {
            str = "date_00" + to_string(i);
        }
        prefix.insert(str, i);
    }
    cout << "SHARED PREFIX STRING HASH INFO:" << endl;
    cout << "Capacity: " << prefix.getCapacity() << endl;
    cout << "Number of elements: " << prefix.size() << endl;
    cout << "Load Factor: " << prefix.loadFactor() << endl;
    cout << "Total collisions: " << prefix.getTotalCollisions() << endl;
    cout << "Max bucket size: " << prefix.maxBucketSize() << endl;
    cout << "Average bucket size: " << prefix.averageBucketSize() << endl;

    cout << endl << "Demonstration of Search and Removal" << endl;
    cout << "Searching sequential table for known value..." << endl;
    cout << "student16 key gives us the value " << seq.search("student16") << endl;
    cout << "Searching sequential table for incorrect value..." << endl;
    cout << "student800 key gives us the value " << seq.search("student800") << " because it does not exist" << endl;
    cout << "Removing student16..." << endl;
    cout << "Did it work? answer: " << seq.remove("student16") << endl;
    cout << "Verifying student16 is gone..." << endl;
    cout << "student16 key now gives us the value " << seq.search("student16") << " meaning it has been properly removed" << endl;


}
```
