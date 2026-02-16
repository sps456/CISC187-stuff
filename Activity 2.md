## Activity 2: Searching
1. It would take 4 steps to find the number 8 in the array [2, 4, 6, 8, 10, 12, 13] using a linear search. The linear search will start at index 0 and the value 8 lies at index 3, so it will take 4 steps total.
2. It would only take 1 step to find the number 8 using a binary search on the above array. Since the binary search starts at the middle index of the array and the array contains 7 values, m = (6-0)/2 = 3. Since 8 happens to lie at index 3 it would only take one step to find it.
3. Binary search is complexity O(log_2 n), so the maximum number of steps it would take to search a 100,000 element array with this algorithm would be log_2(100,000) = 17 when rounded to the nearest whole number.
4. This program demonstrates both the linear and binary search across an ordered, 100000 element array of integers. We can clearly see the Big-O complexity of each of the search algorithms by setting our target value to be at the last possible index. The linear search will have to search through every single of the 100000 indices, meaning its worst case complexity is O(N). The binary search will only end up checking 17 of the indices before finding the target value, and 17 = log_2 (100000), demonstrating that the binary search is indeed O(log_2 N) complexity.

Question 4 Code:
```c++
#include <iostream>
#include <vector>
#include <random>


int main()
{
    using namespace std;
    const int N = 100000;
    int arr[N];
    int linearSteps = 0;
    int binarySteps = 0;
    int target = N;
    for (int i = 0; i < N; i++) {
        arr[i] = (i+1);
    }
// Linear Search
    for (int i = 0; i < N; i++) {
        linearSteps++;
        if (arr[i] == target) {
            cout << "Linear Search: The target value has been found at index " << i << endl;
            break;
        }
    }
    cout << "The Linear Search took " << linearSteps << " steps" << endl;
// Binary Search
    int L = 0;
    int R = N - 1;
    int m;
    while (L <= R) {
        m = (R + L) / 2;
        binarySteps++;
        if (arr[m] < target) {
            L = m + 1;
        }
        else if (arr[m] > target) {
            R = m - 1;
        }
        else {
            cout << "Binary Search: The target value has been found at index " << m << endl;
            break;
        }
    }
    cout << "The Binary Search took " << binarySteps << " steps" << endl;

}
```
5. In order to keep track of our randomized indices, we will have to use another vector to make sure that we dont use the same indices twice. Other than this the random sort will be similar to a linear search except the indices are in a random order.

Pseudocode:
```
function random_search(vector numbers, vector usedIndices, int randoTarget)
  steps = 0  
  usedIndex = false  
  while(usedIndices size == 0)  
    index = random between 0 and 99999    
    for(i = 0; i < usedIndices size; i++)    
      if(usedIndices at i == index)      
        usedIndex = true        
        break        
      else      
        usedIndex = false        
    if(usedIndex is not true)    
      steps++      
      if(numbers at index == randoTarget)      
        output "target is found at index " index " and it took " steps " steps"        
        break        
      else      
        add index to usedIndices
```
This random search algorithm will have a best case complexity of O(1) in the case that at the first random index you find the target. Its worst case in terms of steps is the same as liner O(N) since if you have to check every single index it will take N steps. The average number of indices you would have to check is n/2, so its average complexity would be O(N) as well since the 1/2 becomes part of the O. 

Implementation of Code in c++ (in the same file as the linear and binary code just tacked onto the end):
```c++
    vector<int> numbers;
    vector<int> usedIndices;
    bool valueUsed = false;
    int steps = 0;
    int index;
    int randoTarget = 82343;
    for (int i = 0; i < N; i++) {
        numbers.push_back(i + 1);
    }
    while (usedIndices.size() < N) {
        index = rand() % N;
        for (int i = 0; i < usedIndices.size(); i++) {
            if (usedIndices.at(i) == index) {
                valueUsed = true;
                break;
            }
            else {
                valueUsed = false;
            }
        }
        if (!valueUsed) {
            steps++;
            if (numbers.at(index) == randoTarget) {
                cout << "Random Search: The target value has been found at index " << index << endl;
                break;
            }
            else {
                usedIndices.push_back(index);
            }
        }
    }
    cout << "The Random Search took " << steps << " steps" << endl;
    
}
```
Overall, the random search algorithm is not very practical. It has the same time complexity as a linear search (O(N)), yet it is far more complicated to implement. There is also the added time component of making sure that the new random index hasn't been checked before, so theoritically if the random number generator keeps rolling an already selected value it can take a very long time, especially with larger arrays. It can be superior to a linear search in the case that you know the array is ordered and the target value is in the second half of the array, since the random algorithm could search the end of the array first. However if you know the array is ordered, binary search is a far better and faster option with time complexity O(log_2 N). If the array isn't ordered, linear and random searches will theoretically take the same amount of time, but the linear search is far simpler and doesnt run the risk of taking a long time to cycle random indices. If the list is ordered, binary search is far better than random search, though the added effort required to have a sorted array might make one consider using the random search on a small, unsorted array over a binary search on a sorted one. The only time I would suggest using a random search is if you are feeling reallllly lucky.

Video Explanation of code:
https://drive.google.com/file/d/1HlWM2FG55qoryt53Ulfx2tFdXogF5FzA/view?usp=sharing 
