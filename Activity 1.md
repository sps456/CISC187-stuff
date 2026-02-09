## Activity 1: Arrays
1. In order to create an array of 100 elements you could declare an array and include 100 individual elements in the declaration statement, but this is obviously not a very feasable way of going about it. A better way would be to declare an array of size 100 and then use a loop to populate it with elements. Here is an example for an int array:

```c++
int arr[100];
for (int i = 0; i < 100; i++) {
    arr[i] = i;
}
```
2. I'm not quite sure what this question is asking so I will provide two answers. If you are asking about the size of each individual element in an array, then that would depend on the data type and what elements are in the array. For example a string array could have different elements of different lengths depending on the string. You could use the sizeof() operator to find the total memory that the array takes up. If you are asking about the size of the array itself (which I assume is the case it's just written kinda unclear) then that is the number of data elements the array is capable of holding. So an array of size 100 can hold 100 elements within it. Here is a code example of this: The output of this program would be "Array arr has a size: 100"

```c++
    int arr[100];
    for (int i = 0; i < 100; i++) {
        arr[i] = i;
    }
    std::cout << "Array arr has a size: " << std::size(arr) << std::endl;
```
3. For an array of size 100, these are the number of steps it would take for each of these processes:
- Reading: 1 step
- Searching for a value not contained in the array: 100 steps
- Insertion at the beginning of the array: 101 steps
- Insertion at the end of the array: 1 step
- Deletion at the beggining of the array: 100 steps
- Deletion at the end of the array: 1 step
4. In order to find all of the apples in an array, it is necessary to check every single index in order to count every apple. For this reason, it would take N steps to check every index and then add one to our apple count if an apple is located at that index.
5. In c++, the array name can be treated like a pointer for the first element of the array, so if you want to find the memory address of an array you can output the array variable. Alternatively you can access the memory address like you would with any pointer in c++ by using the & symbol with the array itself. Here is the code examples:

```c++
int arr[100];
std::cout << arr << std::endl;
std::cout << &arr[0] << std::endl;
```
Both of these would print out the same memory address of the array.

Here is the video explanation of the code/assignment: 
https://drive.google.com/file/d/1YR-p2Hm-J_catlw_tSG4T06SuKhPodTd/view?usp=sharing 
