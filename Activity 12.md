## Activity 2: Recursions
1. The base case situation is when the low input is greater than the high input in which case the recursion ends. This could either happen if the initial run has the low value set to something greater than the high value, or if after enough recursions the low value is incremented to value which is greater than the initial high value.
2. You will get infinite recursion since n will never equal 1 in this case. You will pass 10, which passes 8, then 6, then 4, then 2, then 0 and so on until you get a stack overflow error.
3. The base case will simply return high when high and low are equal to one another:
```c++
def sum(low, high)
    if(high == low)
      return high;
    return high + sum(low, high - 1);
end
```
4. In order to print all of the numbers in the array, we will create a function which loops from the start of an array to the end, and if the current array index contains a number it prints the number but if the current array index contains another array, it recursively passes that array to the array printer function.
```c++
def recursiveArrayPrinter(array)
    for(int i = 0; i < array.size(); i++){
      if(std::is_array<array[i]>::value)
        recursiveArrayPrinter(array[i]);
      else
        std::cout << array[i] << std::endl;
```
