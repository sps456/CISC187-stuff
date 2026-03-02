## Activity 4a: Sorting-II
1. To determine the average time complexity for the insertion sort, I will take a half sorted array of 6 elements. This is because the best case scenario begins with a fully sorted array and the worst case scenario begins with a reversed order array, so if we consider the array spacially, the average scenario will be a half sorted array. Take for instance A=[1, 2, 3, 6, 5, 4]:

First we will compare index 1 to index 0 and since 2 > 1 no swap will take place: [1 | 2, 3, 6, 5, 4] comparisons = 1, swaps = 0.

Next we will compare index 2 to index 1 and since 3 > 2 no swap will take place:  [1, 2 | 3, 6, 5, 4] comparisons = 2, swaps = 0.

Next we will compare index 3 to index 2 and since 6 > 3 no swap will take place:  [1, 2, 3 | 6, 5, 4] comparisons = 3, swaps = 0.

Next we will compare index 4 to index 3 and since 5 < 6 we will swap the values, then we will compare our new index 3 to index 2 and since 5 > 3 no swap will take place:  [1, 2, 3, 6 | 5, 4]  ->  [1, 2, 3 | 5, 6, 4] comparisons = 5, swaps = 1.

Next we will compare index 5 to index 4 and since 4 < 6 we will swap the values, then we will compare our new index 4 to index 3 and since 4 < 5 we will swap the values, and then we will compare our new index 3 to index 2 and since 4 > 3 no swap will take place:  [1, 2, 3, 5, 6 | 4]  ->  [1, 2, 3, 5 | 4, 6]  ->  [1, 2, 3 | 4, 5, 6] comparisons = 8, swaps = 3.

Now we have a fully sorted array and it took 8 comparisons and 3 swaps, leaving us with a total of 11 steps, which is a little under half of the max number of steps as seen in the reading, which would be n^2 - n. So if our number of steps is about (n^2 - n) / 2, we would drop the lower degree n and the coefficient and will be left with O(n^2).

2. When I properly sorted the array starting at index i = 1 it did indeed take 20 steps. When I started at i = 2, it only took 18 steps but the array was not properly sorted at the end. The same problem occured when I started at i = 3; it took 14 steps but only half of the array ended up sorted.

Insertion Sort Code:
```c++
#include <iostream>
int main()
{
    using namespace std;
    int arr[] = { 5, 4, 3, 2, 1 };
    int comparisons = 0;
    int swaps = 0;
    for (int i = 3; i < 5; i++) {
        for (int j = i; j > 0; j--) {
            comparisons++;
            if (arr[j - 1] > arr[j]) {
                int temp = arr[j];
                arr[j] = arr[j - 1];
                arr[j - 1] = temp;
                swaps++;
            }
            else {
                break;
            }
        }
    }
    cout << "Sorted Array: [";
    for (int i = 0; i < 5; i++) {
        cout << arr[i] << ", ";
    }
    cout << "]\nNumber of steps: " << (comparisons + swaps) << endl;
}
```
3. The time complexity for this function is O(N) wether or not the string actually contains the letter X. The loop will always check every index of the string even if it has already determined that the string contains 'X', and each check is a comparison so it will always take N steps no matter what. You can easily improve the best and average case runtimes by adding a break in the loop once you have found the letter X. This makes your best case run time (when X is the first character in the string) O(1), while your average case run time will still be O(N) but it will on average take half the number of steps.

Updated function code:
```c++
function containsX(string) {
	foundX = false;
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			foundX = true;
            break;
		}
	}
	return foundX; 
}
```
Video Explanation of Assignment: https://drive.google.com/file/d/1ml3kgu7a9g-wfYYUPh0Bfl9YvTkimY0C/view?usp=sharing 
