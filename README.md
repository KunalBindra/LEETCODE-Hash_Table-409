# LEETCODE-Hash_Table-409
Let's perform a dry run of the given `longestPalindrome` method in the `Solution` class. The goal is to find the length of the longest palindrome that can be built with the letters in the given string `s`.

Here is the code for reference:

```java
class Solution {
  public int longestPalindrome(String s) {
    int ans = 0;
    int[] count = new int[128];

    for (final char c : s.toCharArray())
      ++count[c];

    for (final int freq : count)
      ans += freq % 2 == 0 ? freq : freq - 1;

    final boolean hasOddCount = Arrays.stream(count).anyMatch(freq -> freq % 2 == 1);
    return ans + (hasOddCount ? 1 : 0);
  }
}
```

### Dry Run Example

Let's use the input string `s = "abccccdd"` for this dry run.

1. **Initialization:**
   - `ans = 0`
   - `count = new int[128]` (an array to count the frequency of each character)

2. **First loop (count frequencies):**
   - Convert the string `s` to a character array and iterate through each character:
     - `s.toCharArray() = ['a', 'b', 'c', 'c', 'c', 'c', 'd', 'd']`
     - For each character, increment its corresponding frequency in the `count` array:
       - `count['a']++` → `count[97] = 1` (ASCII of 'a' is 97)
       - `count['b']++` → `count[98] = 1` (ASCII of 'b' is 98)
       - `count['c']++` → `count[99] = 4` (ASCII of 'c' is 99)
       - `count['d']++` → `count[100] = 2` (ASCII of 'd' is 100)

   The `count` array now looks like this (only relevant entries shown):
   ```
   count[97] = 1  // 'a'
   count[98] = 1  // 'b'
   count[99] = 4  // 'c'
   count[100] = 2 // 'd'
   ```

3. **Second loop (calculate the length of the longest palindrome):**
   - Iterate through each frequency in the `count` array:
     - If the frequency is even, add it directly to `ans`:
       - `count[99] = 4` → `ans += 4` → `ans = 4`
       - `count[100] = 2` → `ans += 2` → `ans = 6`
     - If the frequency is odd, add the largest even number less than the frequency:
       - `count[97] = 1` → `ans += 0` (1 - 1 = 0) → `ans = 6`
       - `count[98] = 1` → `ans += 0` (1 - 1 = 0) → `ans = 6`

4. **Final adjustment (add one if there is any character with an odd frequency):**
   - Check if there is any odd frequency in the `count` array:
     - `count[97] % 2 == 1` → true (since `count[97] = 1`)
   - Since there is at least one odd frequency, add 1 to `ans`:
     - `ans = 6 + 1` → `ans = 7`

### Conclusion

The length of the longest palindrome that can be built with the letters in the string `"abccccdd"` is `7`. The method returns `7`.

### Summary

The dry run reveals that the method works by:
1. Counting the frequency of each character in the input string.
2. Adding the maximum possible even counts to `ans`.
3. Adding an extra `1` if there is at least one character with an odd frequency to account for the center character in the palindrome.

The code correctly calculates the length of the longest palindrome that can be constructed from the given string.
