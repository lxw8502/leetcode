# 41. First Missing Positive
Given an unsorted integer array, find the smallest missing positive integer.

### Example 1:

Input: [1,2,0]    
Output: 3    

### Example 2:

Input: [3,4,-1,1]       
Output: 2       

### Example 3:

Input: [7,8,9,11,12]      
Output: 1      

### Solution 1 
```java
//4ms  NOT constant space
class Solution {
    public int firstMissingPositive(int[] nums) {
        TreeSet<Integer> ts = new TreeSet<>();
        for(int i = 1; i <= nums.length+1; i++){
            ts.add(i);
        }
        for(int j = 0; j < nums.length; j++){
            ts.remove(nums[j]);
        }
        return (int) ts.first();
    }
}

//2ms  NOT constant space
class Solution {
    public int firstMissingPositive(int[] nums) {
        LinkedHashSet<Integer> ts = new LinkedHashSet<>();
        for(int i = 1; i <= nums.length+1; i++){
            ts.add(i);
        }
        for(int j = 0; j < nums.length; j++){
            ts.remove(nums[j]);
        }
        Iterator<Integer> it = ts.iterator();
        if(it.hasNext()){
            return it.next();
        }
        return 0;
    }
}

//1ms  NOT constant space
class Solution {
    public int firstMissingPositive(int[] nums) {
        HashSet<Integer> st = new HashSet<>();
        for(int i = 0; i < nums.length; i++){
            st.add(nums[i]);
        }
        int res = 1, n = nums.length;
        while (res <= n) {
            if (!st.contains(res)) return res;
            ++res;
        }
        return res;
    }
}
```


### Solution 2
```java
//0ms  constant space
//因为限制了空间复杂度为常数个额外空间，所以只能覆盖原有数组，思路是把 nums[i] 放在 nums[nums[i] - 1]上，
//遍历整个数组，如果 nums[i] != i + 1, 而 nums[i] 为正整数且不大于n，另外 nums[i] 不等于 nums[nums[i] - 1] 的话，将两者位置调换，
//如果不满足上述条件直接跳过，最后再遍历一遍数组，如果对应位置上的数不正确则返回正确的数
//需要注意的点：1. nums[i] > 0 && nums[i] <= n  是小于等于n   2.第一个for循环内的是一个while循环而不是if
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;
        for (int i = 0; i < n; ++i) {
            while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                swap(nums, i, nums[i] - 1);
            }
        }
        for (int i = 0; i < n; ++i) {
            if (nums[i] != i + 1) return i + 1;
        }
        return n + 1;
    }
    
    private void swap(int[] nums, int m, int n){
        int tmp = nums[m];
        nums[m] = nums[n];
        nums[n] = tmp;
    }
}  
```
