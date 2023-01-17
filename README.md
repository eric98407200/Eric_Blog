# 紀錄leetCode 75 刷題過程

## Two Sum 
### 問題
* 給一個陣列，返回兩個數字的索引，使它們相加到特定目標
### 範例:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
* 需從 nums 中找出兩數相加等於 target 的兩數索引值，並回傳兩數索引值組成的容器
### 解答1 : 使用兩個for迴圈達成
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i = 0; i < nums.length; i++){
            for(int j = i+1; j < nums.length; j++){
                if(nums[i]+nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }
        return null;
    }
}
```
* 因使用兩個for迴圈，時間複雜度是O(n^2)
### 解答2 : 建立一個HashMap，在for迴圈中利用差值所得到另一個數值，查詢HashMap內是否有存在，如果有的話則返回其索引值。
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(map.containsKey(target - nums[i])){
                return new int[]{map.get(target - nums[i]) , i};
            }
            map.put(nums[i],i);
        }
        return null;
    }
}
```
* 因只使用一個for迴圈，時間複雜度是O(n)
