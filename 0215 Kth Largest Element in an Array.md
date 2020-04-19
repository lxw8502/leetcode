# Kth Largest Element in an Array

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

### Example 1:

Input: [3,2,1,5,6,4] and k = 2   
Output: 5   
### Example 2:

Input: [3,2,3,1,2,4,5,5,6] and k = 4   
Output: 4   
### Note:   
You may assume k is always valid, 1 ≤ k ≤ array's length.   


### solution 1
```java
// usr the quicksort mind, partition function.
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int left = 0, right = nums.length - 1;
        while(true){
            int num = partition(nums, left, right);
            if(num == k-1) return nums[num];
            else if(num < k-1) left = num + 1;
            else right = num - 1;
        }
    }
    public int partition(int[] nums, int left, int right){
        int pivot = left, l = left + 1, r = right;
        while(l <= r){
            if(nums[l] < nums[left] && nums[r] > nums[left]) swap(nums, l++, r--);
            else if(nums[l] >= nums[left]) l++;
            else r--;
        }
        swap(nums, left, r);
        return r;
    }
    public void swap(int[] nums, int m, int n){
        int temp = nums[m];
        nums[m] = nums[n];
        nums[n] = temp;
    }
}
```

### solution 2
``` java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int val : nums) {
            pq.add(val);
            if (pq.size() > k)
                pq.poll();
        }
        return pq.peek();
    }
    
}
```

### solution 3
```java
class Solution{
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length - k];
    }
}

