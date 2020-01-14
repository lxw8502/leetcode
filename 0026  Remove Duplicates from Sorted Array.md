# 26. Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

### Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.

### Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.

### Solution 1

```java
//第一次刷的时候的思路是使用n来记录重复项的个数
class Solution {
    public int removeDuplicates(int[] nums) {
        int n = 0;  //use a number n to record the number of Duplicate items
        for(int i = 1; i< nums.length; i++){
            if(nums[i] == nums[i-1]){
                n++;
                nums[i-n] = nums[i];
            }else{
                nums[i-n] = nums[i];
            }
        }
        return nums.length-n;
    }
}
```

### Solution 2
```java
//快慢指针，快指针用来遍历数组，慢指针指向新数组的最后一项
//当快指针和它的前一项相同时，将cur++
//当快指针和它的前一项不相同时，先将pre加一，再将nums[cur]的值赋值给nums[pre],最后再将cur++
//最后要对数组nums为空数组时特殊处理一下
//注 ：这种解法也可以将nums[cur]和nums[pre]进行比较
class Solution {
    public int removeDuplicates(int[] nums) {
        int pre = 0, cur = 1, n = nums.length;
        while(cur < n){
            if(nums[cur] == nums[cur - 1]) cur++;
            else nums[++pre] = nums[cur++];
        }
        return  nums.length == 0 ? 0 : pre + 1;
    }
}

class Solution {
    public int removeDuplicates(int[] nums) {
        int pre = 0, cur = 1, n = nums.length;
        while(cur < n){
            if(nums[cur] == nums[pre]) cur++;
            else nums[++pre] = nums[cur++];
        }
        return  nums.length == 0 ? 0 : pre + 1;
    }
}

class Solution {
    public int removeDuplicates(int[] nums) {
        //1
        int pre = 1, cur = 1, n = nums.length;
        while(cur < n){
            //2
            if(nums[cur] == nums[pre - 1]) cur++;
            //3
            else nums[pre++] = nums[cur++];
        }
        //4
        return  nums.length == 0 ? 0 : pre;
    }
}

//for循环写法
//注意这里是将num和nums[i - 1]进行比较
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        for (int num : nums) {
            if (i < 1 || num > nums[i - 1]) {
                nums[i++] = num;
            }
        }
        return i;
    }
};
```
