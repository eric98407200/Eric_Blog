# 淺淺地紀錄leetCode 75 刷題過程

## 1.Two Sum 
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
    * 這個解法的時間複雜度為 $O(n^2)$，比使用HashMap的解法慢得多。當數組很大時，運行時間會非常長。因此，使用HashMap的解法是更好的選擇。

### 解答2 : 建立一個HashMap，先將值存進，在使用一個for迴圈達成
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>(); // 使用HashMap來儲存數字與其索引的對應關係
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i]; // 計算目標與當前數字的差值
            if (map.containsKey(complement)) { // 如果map中已經存在差值對應的索引，就返回結果
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i); // 將當前數字與其索引加入map (以nums中value作為key值)
        }
        throw new IllegalArgumentException("No two sum solution"); // 如果找不到符合條件的數字組合，就拋出異常
    }
}
```
    * 這邊因只使用一個for迴圈，其中利用差值所得到另一個數值，查詢HashMap內是否有存在，如果有的話則返回其索引值。此方法時間複雜度是O(n)
    
  
## 2.Best Time to Buy and Sell
### 問題
* 給定一個股票價格的數組 prices，prices[i] 表示第 i 天的股票價格。你想要通過一次買進和一次賣出交易來獲得最大利潤。如果不能獲得利潤，則返回 0。
### 範例:
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
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
    * 這個解法的時間複雜度為 $O(n^2)$，比使用HashMap的解法慢得多。當數組很大時，運行時間會非常長。因此，使用HashMap的解法是更好的選擇。

### 解答2 : 建立一個HashMap，先將值存進，在使用一個for迴圈達成
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>(); // 使用HashMap來儲存數字與其索引的對應關係
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i]; // 計算目標與當前數字的差值
            if (map.containsKey(complement)) { // 如果map中已經存在差值對應的索引，就返回結果
                return new int[] { map.get(complement), i };
            }
            map.put(nums[i], i); // 將當前數字與其索引加入map (以nums中value作為key值)
        }
        throw new IllegalArgumentException("No two sum solution"); // 如果找不到符合條件的數字組合，就拋出異常
    }
}
```
    * 這邊因只使用一個for迴圈，其中利用差值所得到另一個數值，查詢HashMap內是否有存在，如果有的話則返回其索引值。此方法時間複雜度是O(n)
