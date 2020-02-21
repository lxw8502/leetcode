# 345. Reverse Vowels of a String

Write a function that takes a string as input and reverse only the vowels of a string.

### Example 1:

Input: "hello"   
Output: "holle"
### Example 2:

Input: "leetcode"   
Output: "leotcede"
### Note:
The vowels does not include the letter "y".

### Solution 1

```java
//将原有字符串转换成一个字符数组
class Solution {
    public String reverseVowels(String s) {
        Set<Character> vowels = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
        char[] arr = s.toCharArray();
        int m = 0, n = arr.length - 1;
        while(m < n){
            if(!vowels.contains(arr[m])){
                m++;
            }else if(!vowels.contains(arr[n])){
                n--;
            }else{
                char temp = arr[m];
                arr[m++] = arr[n];
                arr[n--] = temp;
            }
        }
        return String.valueOf(arr);
    }
}
```

### Solution 2
```java
//新建一个和字符串s一样长的字符数组，然后进行填充
class Solution {
    private final static HashSet<Character> vowels = new HashSet<>(
            Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));

    public String reverseVowels(String s) {
        if (s == null) return null;
        int i = 0, j = s.length() - 1;
        char[] result = new char[s.length()];
        while (i <= j) {
            char ci = s.charAt(i);
            char cj = s.charAt(j);
            if (!vowels.contains(ci)) {
                result[i++] = ci;
            } else if (!vowels.contains(cj)) {
                result[j--] = cj;
            } else {
                result[i++] = cj;
                result[j--] = ci;
            }
        }
        return new String(result);
    }
}
```
