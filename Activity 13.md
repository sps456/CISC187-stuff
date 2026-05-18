## Activity 13: Space Constraints
1. This function will create a new array and fill it with n(n-1) values, with n being the size of the initial array. n(n-1) = n^2 - n so the function has a space complexity of O(N^2).
2. This array reversing function creates an entirely new array in order to fill it with values starting at the back of the original array ending at the front. Since it creates an entirely new array with the same size as the initial array, this function has a space complexity of O(N).
3. In order to create an array reversing function with space complexity O(1) we must swap the values within the original array without creating a new one:
```c++
function spaceReverse(array) { 
  for (int i = 0; i < array.size()/2 - 1; i++) {
    int temp = array[i];
    array[i] = array[array.size()-1-i];
    array[array.size()-1-i] = temp;
  }
  return array;
}
```
Since this function only creates a single temporary variable in order to preserve the values in the swap, it has a space complexity of O(1).

4. 
| Version    | Time complexity | Space complexity |
| ---------- | --------------- | ---------------- |
| Version #1 | O(N)               | O(N)                |
| Version #2 | O(N)               | O(1)                |
| Version #3 | O(N)               | O(N)                |

The first function creates a new array then loops through each value of the original array, multiplying it by 2, then adding it to the new array. Since it loops through N times and creates an entirely new array containing N values, it has a time complexity of O(N) and a space complexity of O(N).

The second function still loops through each value of the original array, but it doubles those values without creating a new array so it has a time complexity of O(N) and a space complexity of O(1).

The last function will have N recursive steps with each step completing one task (doubling the array value at the current index). Each of these recursive steps adds a method stored to the call stack, so this function has a time complexity of O(N) and a space complexity of O(N).
