## Activity 4b: Adaptive Sorting
Part C Documentation:

To determine the scenario the array was sorted in, I looped through the array from index 1 til the end comparing each value to the one to its left. If the value to the left was greater than the one to the right, that represented an error in the sorting which would cause a swap to take place. If none of these errors exist, that means that the array is already sorted. If the number of errors is equal to N-1, then the array is in descending order which is the worst case scenario. I put the average threshhold at errors = (n-1) / 2 since its right in the middle of the worst amount of errors and the best amount of errors. If you have more errors than that, it is a worse than average scenario, and if you have less errors than that it is a better than average scenario. I still chose the selection sort for all scenarios except the best case scenario since the average number of steps for the selection sort is about half that of the insertion sort, though they both have an O(N^2) time complexity so it doesnt really matter. If you wanted a more accurate adaptive sorting pattern you would have to break smaller sub devisions, since if the array is very close to being sorted the insertion sort is probably better, but past the average case and beyond the selection sort is slightly faster. The threshhold I chose was more so to determine the exact average scenario, since on average the selection sort will be better since the amount of swaps the insertion sort has to do in bad scenarios takes up more time. The insertion sort has a faster best case, but a less consistent average case becasue of this.

Code:
```c++
#include <iostream>
#include <random>

void insertionSort(int arr[], int size) {
    for (int i = 1; i < size; i++) {
        for (int j = i; j > 0; j--) {
            if (arr[j - 1] > arr[j]) {
                int temp = arr[j];
                arr[j] = arr[j - 1];
                arr[j - 1] = temp;
            }
            else {
                break;
            }
        }
    }
}

void selectionSort(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        int mindex = i;
        for (int j = i; j < size; j++) {
            if (arr[j] < arr[mindex]) {
                mindex = j;
            }
        }
        int temp = arr[i];
        arr[i] = arr[mindex];
        arr[mindex] = temp;
    }
}

int arrayScenario(int arr[], int size){
    int errors = 0;
    for (int i = 1; i < size; i++) {
        if (arr[i - 1] > arr[i]) {
            errors++;
        }
    }
    if (errors == 0) {
        return 0; //best case scenario
    }
    else if (errors <= (size-1) / 2) {
        return 1; //average case scenario
    }
    else if (errors == (size - 1)){
        return 2; //worst case scenario
    }
    else {
        return 3; //worse than average case scenario
    }
}

int main()
{
    using namespace std;
    srand(4);  
    int arr[50];
    int choice;
    cout << "Which part of the assignment are you utilizing? 1 for A, 2 for B" << endl;
    cin >> choice;
    if (choice == 1) {
        int fastOrRandom;
        cout << "Would you like to demonstrate the best case scenario (0) or a random scenario (1)?" << endl;
        cin >> fastOrRandom;
        if (fastOrRandom != 0) {
            for (int i = 0; i < 50; i++) {
                arr[i] = rand() % 100;
            }
        }
        else {
            for (int i = 0; i < 50; i++) {
                arr[i] = i;
            }
        }
        int scenario = arrayScenario(arr, 50);
        if (scenario == 0) {
            cout << "This is the best case scenario, so an insertion sort will be faster" << endl;
            insertionSort(arr, 50);
            cout << "[";
            for (int i = 0; i < 50; i++) {
                cout << arr[i] << ", ";
            }
            cout << "]" << endl;
        }
        else if (scenario == 1) {
            cout << "This is a good to average scenario, so a selection sort is usually faster" << endl;
            selectionSort(arr, 50);
            cout << "[";
            for (int i = 0; i < 50; i++) {
                cout << arr[i] << ", ";
            }
            cout << "]" << endl;
        }
        else {
            cout << "This is a worse than average scenario, so a selection sort is usually faster" << endl;
            selectionSort(arr, 50);
            cout << "[";
            for (int i = 0; i < 50; i++) {
                cout << arr[i] << ", ";
            }
            cout << "]" << endl;
        }
    }
    else if (choice == 2) {
        cout << "Please input 50 integers and I will determine which sorting algorithm would be faster:\n";
        int num;
        for (int i = 0; i < 50; i++) {
            cin >> num;
            arr[i] = num;
        }
        int scenario = arrayScenario(arr, 50);
        if (scenario == 2) {
            cout << "This is the worst case scenario. Your array is in descending order. A selection sort will be faster but its up to you I guess\n";
        }
        else if( scenario != 0) {
            cout << "This is an average case scenario. Both sorting algorithms will perform about as well as one another on average\n";
        }
        else {
            cout << "This is the best case scenario. Your array is in ascending order and there is no reason to sort it\n";
        }
    }
    else {
        cout << "STOP TROLLING INPUT A REAL CHOICE!!!!!!!!!!!!!!!!!!!!!";
    }
    
}
```
Video Explanation of Code:
https://drive.google.com/file/d/1iOle63mOjS9n_Z0Xvwfc-jCLf12Yy4On/view?usp=sharing 
