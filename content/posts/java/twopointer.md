+++
date = '2025-02-21T16:51:24-05:00'
draft = true
title = 'Two pointer Pattern'
+++

## All about Two pointers

### Why to use two pointer technique?
- Solve problems  involving sorting, searching, manipulating arrays or lists. 
- Reduce time complexity from O(n2) to O(n) and space complexity is O(1)
  - Ex: Two Sum, Three sum, Closes two sum, four sum, trapping rain water

### Types of Two pointer techniques:
- Opposite ends approach:
  - One pointer starts from left and other on right. Used for problems like **finding pairs** in a sorted array.
      - Opposite pairs helps identify pairs efficiently if sum is too small move left pointer forward.
  - Same Direction approach: Both pointers move in same direction at different speeds. Ex:** Remove duplicates** from a sorted array or **fast and slow pointer** approach

Naive method might take more time or space to execute but two pointer take less time and space.

**Two pointer** works well with **sorted arrays**

### How to use it?
- Use two index left and right.
- Initialize left = 0 and right = n - 1
- Compute sum =  arr[left] + arr[right]
- If sum equals target, we've found the pair
- If sum < target move left pointer forward to increase the sum
- If sum > target move right pointer backward to decrease the sum

### Understand while loop

While loop in java is used to repeatedly execute a block of code as long as given condition is true. It is used when number of iterations is not known in advance and loop should continue until certain condition is met.

```
while(condition){}
```
```
int i = 0;
while (i < 5) {
    System.out.println(i);  // Prints numbers from 0 to 4
    i++;  // Increment i to avoid an infinite loop
}
```

Pallindrome is the one which on converting all uppercase to lowercase and removing any non alphanumeric characters reads same from front and back.

**Remember: string != String. In java String is class**

String replace('a', 'b') method replaces b with a in a string and returns a new string. It does not modify original string

```
String s = "R:aveena";
String new = s.replace(":", "");
System.out.println(new); //returns new string
```

To convert a string into character array: Use toCharArray()
```
String s = "Raveena";
char[] arr = s.toCharArray();
```

Character has `isLetterOrDigit` which tell us if a character is digit or letter or not

----------------------

## 3Sum problem
