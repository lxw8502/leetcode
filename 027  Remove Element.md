# 27. Remove Element

Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

### Example 1:

Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.

### Example 2:

Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.

### 解法1：
//我最初的想法，用俩个指针，m指在数组开头，n指在数组结尾，然后将nums[m]的值和val进行比较。
//如果等于val的话就将nums[n]的值赋值给nums[m]，并将n--。注意这里并不能给m++，因为新赋值给nums[m]的值仍然有可能等于val。
//如果不等于val的话，则将m++。现在，m指针之前的值就都不等于val了。
//这样一直循环下去直到m > n,停止循环。
//那么最后应该返回哪个值呢，因为现在m指针之前的所有值组成的新数组就是需要求得的新数组，所以m就是新数组的长度，直接返回m即可。
//最后需要考虑一下当nums为空数组时的情况，发现不用特殊考虑，所以完成！
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int m = 0, n = nums.length - 1;
        while(m <= n){
            if(nums[m] == val){
                nums[m] = nums[n];
                n--;
            }else{
                m++;
            }
        }
        return m;
    }
}
```
### 解法2：
```java
//另外一种解法，这种解法也用到了俩个变量m和i。
//m和上一种解法中的m作用一样，记录新数组的长度，i用来遍历数组nums。
//当nums[i] != val时，将nums[i]赋值给nums[m]，并将m++。
//当nums[i] == val时，什么也不用做。
//当遍历完数组后，返回m。
class Solution {
    public int removeElement(int[] nums, int val) {
        int m = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != val){
                nums[m++] = nums[i];
            }
        }
        return m;
    }
}
```

