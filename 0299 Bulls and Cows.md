# 299 Bulls and Cows
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

### Example 1:

Input: secret = "1807", guess = "7810"      

Output: "1A3B"     

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.

### Example 2:

Input: secret = "011", guess = "110"

Output: "1A2B"

### Example 3:

Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.

### Example 4:

Input: secret = "10", guess = "01"

Output: "0A2B"

Note: You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

### Solution 1:
```java
//
class Solution {
    public String getHint(String secret, String guess) {
        char[] arr1 = secret.toCharArray();
        char[] arr2 = guess.toCharArray();
        int bulls = 0, cows = 0;
        for(int i = 0; i < arr2.length; i++){
            if(arr2[i] == arr1[i]){
                bulls++;
                arr1[i] = '#';
            }else{
                for(int j = 0; j < arr1.length; j++){
                    if(arr2[i] == arr1[j] && arr2[j] != arr1[j]){
                        cows++;
                        arr1[j] = '#';
                        break;
                    }
                }               
            }
        }

        return bulls + "A" +cows + "B";
    }
}
```

### Solution 2 
```java
//使用哈希表，来建立数字和其出现次数的映射。
class Solution {
    public String getHint(String secret, String guess) {
        int m[] = new int[256], bulls = 0, cows = 0;
        for (int i = 0; i < secret.length(); ++i) {
            if (secret.charAt(i) == guess.charAt(i)) ++bulls;
            else {
                if (m[secret.charAt(i)]++ < 0) ++cows;
                if (m[guess.charAt(i)]-- > 0) ++cows;
            }
        }
        return bulls + "A" +cows + "B";
    }
}
```
