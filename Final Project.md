# CISC187 Final Project
## Task 1
To optimize this problem in order to have a time complexity of O(N+M), we can create a set then loop through both sport arrays first checking if the player exists in the set and if not adding them to the set. If ever a player already exists in the set, this means that they must play both sports so we can add them to our return array. I also created a player object to store the three strings for each player in order to simplify the implementation of the two sport arrays:
Task 1 code:
```c++
#include <iostream>
#include <set>
#include <vector>
using namespace std;

class player
{
private:
    string first_name;
    string last_name;
    string team;
public:
    player(string f, string l, string t) {
        first_name = f;
        last_name = l;
        team = t;
    }
    string getFirstName() { return first_name; }
    string getLastName() { return last_name; }
};

vector<string> compareSports(vector<player> football, vector<player> basketball) {
    set<string> players;
    vector<string> ret;
    for (int i = 0; i < football.size(); i++) {
        string fullname = football[i].getFirstName() + " " + football[i].getLastName();
        if (players.count(fullname) == 1) {
            ret.push_back(fullname);
        }
        else {
            players.insert(fullname);
        }
    }
    for (int i = 0; i < basketball.size(); i++) {
        string fullname = basketball[i].getFirstName() + " " + basketball[i].getLastName();
        if (players.count(fullname) == 1) {
            ret.push_back(fullname);
        }
        else {
            players.insert(fullname);
        }
    }
    return ret;
}

int main()
{
    vector<player> basketball = {player("Jill","Huang","Gators"),player("Janko","Barton","Sharks"),player("Wanda","Vakulskas","Sharks"),
        player("Jill","Moloney","Gators"),player("Luuk","Watkins","Gators") };
    vector<player> football = { player("Jill","Huang","Barleycorns"),player("Tina","Watkins","Barlycorns"),
        player("Wanda","Vakulskas","Barleycorns"),player("Hanzla","Radosti","32ers"),player("Alex","Patel","32ers") };
    vector<string> both = compareSports(football, basketball);
    for (int i = 0; i < both.size(); i++) {
        cout << both[i] << endl;
    }
    return 0;
}
```
The compare sports funtion is out O(N+M) function which returns a vector containing only the names of the players who play both sports and the code as a whole outputs those names (Jill Huang and Wanda Vakulskas).
# Task 2
In order to determine missing value with a time complexity of O(N), we can loop through our array summing up each of its elements, then subtract that from our expected sum of integers from 0 to N, which is given by the formula n(n+1)/2.
Task 2 Code:
```c++
#include <iostream>
#include <iterator>
using namespace std;

int missingInteger(int numbers[], int size) {
    int sum = 0;
    for (int i = 0; i < size;  i++) {
        sum += numbers[i];
    }
    return size * (size+1) / 2 - sum;
}
int main()
{
    int numbers[] = {2,3,0,6,1,5};
    cout << missingInteger(numbers,size(numbers));
    return 0;
}
```
The missingInteger function is our O(N) function to determine which integer is missing from the array and the main method tests this function with a sample array, which correctly returns 4 as the missing integer.
# Task 3
