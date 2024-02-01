# 淺淺紀錄leetCode 75
## @ Two Sum 
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
----
## @ Maximum Subarray
### 問題
* 找出整數陣列中具有最大總和的子陣列，並返回該總和。
### 範例:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
```
* 需從 nums 中找出兩數相加等於 target 的兩數索引值，並回傳兩數索引值組成的容器
### 解答 : 使用Kadane's algorithm（卡登算法），通過遍歷陣列一次，在線性時間內找到最大子陣列和。該算法的基本思想是維護兩個變數：目前子陣列的總和和找到的最大總和。在遍歷過程中，將當前元素添加到目前總和中，並更新最大總和。如果目前總和變為負數，則將其重置為0，重新計算子陣列的總和。最終，最大總和即為所求
```java
class Solution {
    public int maxSubArray(int[] nums) {
    	//設定目前總和
    	int sum = 0;
    	//設定最大總和
    	int max = Integer.MIN_VALUE;
    	for(int i = 0; i < nums.length; i++) {
			sum += nums[i];
    		max = Math.max(sum, max);
    		//總和小於0時歸0
    		if(sum < 0) sum = 0;
    	}
    	return max;
    }
}
```
* 這邊因只使用一個for迴圈，該解答的時間複雜度為 O(n)、空間複雜度為 O(1)。
----
## @ Container With Most Water
### 問題
* 在一個非負整數的陣列中，找到兩個柱子組成的容器，使其能夠盛放最多的水。
### 範例:
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. 
In this case, the max area of water (blue section) the container can contain is 49.
```
* 回傳最大容積、需同時考慮X,Y軸。
### 解答 : 使用「雙指針法」來解決。初始化兩個指針，一個指向陣列的開始，另一個指向陣列的結尾。然後計算兩個指針所指的柱子所能容納的水量（取兩個指針指向的柱子中較小的高度乘上兩個指針之間的距離），並更新目前的最大水量。
```java
class Solution {
    public static int maxArea(int[] height) {
        //設定寬度
    	int width = 0;
        //設定左右指針位置
    	int left = 0, right = height.length - 1;
        //指針往右靠
    	while(left < right) {
            // 計算容器的寬度
            int width = right - left;
            // 計算容器的高度，選擇左右兩邊較矮的那一邊
            int containerHeight = Math.min(height[left], height[right]);
            // 計算容器的面積並更新最大面積
            int area = width * containerHeight;
            maxArea = Math.max(maxArea, area);
            // 移動指針，將高度較矮的一邊向內移動，以尋找可能的更大面積
    		if(height[left] < height[right]) {
    			left++;
    		}else {
    			right--;
    		}
    	}
    	return size;
    }
}
```
* 時間複雜度為O(n)，其中n為陣列的長度，因為只需遍歷一次陣列。
----
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
### 解答 : 使用for迴圈達成
```java
class Solution {
    public int maxProfit(int[] prices) {
        //最低購買金額
        int minPrice = Integer.MAX_VALUE;
        //最大盈利
        int maxProfit = 0;
        for (int i = 0; i < prices.length; i++) {
            //找出最低的購買金額
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            //如果今天的金額大於最低購買金額時則計算最大盈利
            } else if (prices[i] - minPrice > maxProfit) {
                maxProfit = prices[i] - minPrice;
            }
        }
        return maxProfit;
    }
}
```
* 使用一次for迴圈來解決此問題。遍歷整個數組，同時維護兩個變數：minPrice 和 maxProfit。
* 如果當前股票價格比 minPrice 小，則更新 minPrice 為當前股票價格。
* 否則，如果當前股票價格減去 minPrice 的值比 maxProfit 大，則更新 maxProfit 為該值。
* 這邊因只使用一個for迴圈，時間複雜度及空間複雜度皆是O(n)

----
## 3.Contains Duplicate
### 問題
* 找出數組中重複的值。
### 範例:
```
Input: nums = [1,2,3,1]
Output: true
```
* 有則返回TRUE，若沒有則返回FALSE
### 解答 : 使用HashSet搭配for迴圈
```java
class Solution {
    public static boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int i = 0; i < nums.length; i++){
            if(set.contains(nums[i])){
            	return true;
            }else {
            	set.add(nums[i]);
            }
        }
        return false;
    }
}
```
* 這邊因只使用一個for迴圈，時間複雜度及空間複雜度皆是O(n)
----
## 4.Number of 1 Bits
### 問題
* 寫一個函數，它接受一個無符號整數的二進制表示，並返回它包含的1位元的數量。
### 範例:
```
Input: n = 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.
```
* 計算出位元中含有1的數量
### 解答 : 定義一個計數器count，並使用while循環遍歷整個輸入的整數
```java
class Solution {
    public static int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count += n & 1;
            n >>>= 1;
        }
        return count;
    }
}
```
* 此方法時間複雜度為O(k)，其中k是n的二進制表示中1的個數、空間複雜度是O(1)。
----
## 5.Counting Bits
### 問題
* 給定一個整數n，返回一個長度為n+1的數組ans，ans[i]是i的二進制表示中1的個數。
### 範例:
```
Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
```
* 計算出整數二進制表示中1的數量，並放入array中
### 解答 : 使用for循環遍歷，並使用bitCount得出整數中1的數量
```java
class Solution {
    public int[] countBits(int n) {
        int[] arr = new int [n+1];
        for(int i = 0; i <= n; i++){
            arr[i] = Integer.bitCount(i);
        }
        return arr;
    }
}
```
* 此方法時間和空間複雜度都是O(n)
