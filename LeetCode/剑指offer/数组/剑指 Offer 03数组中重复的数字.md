#题目描述
找出数组中重复的数字。
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
####示例 1：
```输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```
##我的解法：set+foreach
```java
 public int findRepeatNumber(int[] nums) {
      Set<Integer>set=new HashSet<>();
      for(int i=0;i<nums.length;i++){
          if(!set.contains((Integer)nums[i])) {
             set.add(nums[i]);
          }else{
              return nums[i];
          }
      }
      return -1;
  }
  ```
##解法一：set+foreach
``` java 
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        int repeat = -1;
        for (int num : nums) {
            if (!set.add(num)) {//直接加，失败则返回
                repeat = num;
                break;
            }
        }
        return repeat;
    }
}
```
##解法二：原地交换
```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while(i < nums.length) {
            if(nums[i] == i) {
                i++;
                continue;
            }
            if(nums[nums[i]] == nums[i]) return nums[i];//如果nums[i]超过nums.length会越界，但是nums 里的所有数字都在 0～n-1
            int tmp = nums[i];
            nums[i] = nums[tmp];
            nums[tmp] = tmp;
        }
        return -1;
    }
}
```
