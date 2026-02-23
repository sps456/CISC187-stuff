## Activity 3a: Sorting-I
1. An algorithm that takes 4N + 16 steps would have a big O complexity of O(N) since the constant would be dropped and the coefficient is absorbed into O.
2. An algorithm that takes 2N^2 steps would have a big O complexity of O(N^2) since the coefficient is absorbed into big O.
3. In this function, there will be 2 pass throughs of an array, one to double the values within the array and then one to add up each value to a total sum. Since each added value in the array has 2 steps associated with it, it will take 2N steps to complete the function, meaning it has a time complexity of O(N) since the coefficient gets absorbed into O.
4. This function prints three differently cased strings for each element within the array, meaning it will have 3N steps. Therefore its time complexity is O(N).
5. This function will loop through each index of the array and if the index is even it will loop through the array again to sum the numbers. So for each element in the array, it will add another initial comparison and every two elements itll add another arrays worth of comparisons, meaning its time complexity will be O(N^2).

Video Explanation of Assignment:
https://drive.google.com/file/d/1bZRswDxY8fYUxGnGM7SDKIl9kaq4UA-q/view?usp=sharing 
