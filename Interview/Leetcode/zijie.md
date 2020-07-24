# simple

* (# 1)给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。

1. 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

```js
var twoSum = function(nums, target) {
    let result = []
    for(let i=0;i<nums.length;i++){
        let index = nums.indexOf(target-nums[i])
        if(index>-1 && index!=i){
            result.push(index,i)
            break
        }
    }
    return result
    //注意循环次数
}
```

* (#53) 给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。(贪心算法，每次都贪最大的)
```js
var  maxSubArray = function(nums) {
let max = ans = nums[0]
  for(let i = 1;i<nums.length;i++){
      if(ans<0){
          ans = nums[i]
      }else{
          ans = ans + nums[i]
      }
      max = Math.max(ans,max)
  }
  return max 
}
```

* (#121)给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。(贪心算法，每次都贪最大的)
1. 注意：你不能在买入股票前卖出股票。
```js
function maxProfit(prices) {
    let min = prices[0],max=0
    for(let i=1;i<prices.length;i++){
        let price = prices[i]
        if(min>price) min = price ;
        if(price-min>max) max = price-min;
    }
    return max
}
```

* (#20)给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。
```js
var isValid = function(s) {
    let arr = s.split("")
    let arr1 = []
    for(let v of s){
        if(v=="(" || v == "{" || v == "["){
            arr1.push(v)
        }else{
            if(arr1.length==0){
                return false
            }
            //将栈顶的左括号出栈
            const top = arr1.pop()
            if(top == "(" && v != ")"){
                return false 
            }
            if(top == "{" && v != "}"){
                return false
            }
            if(top == "[" && v != "]"){
                return false
            }
        }
    }
    return arr1.length ==0 
}
```

* (#7)给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

1. 输入: -123,输出: -321
2. 假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。
```js
var reverse = function(x) {
   if(x> (2**31)-1  || x< -(2**31)){
        return 0;
    }
    let absX = Math.abs(x)
    let strX = x+""
    let arr = strX.split("")
    arr.reverse()
    x = x<0?-parseInt(arr.join("")):parseInt(arr.join(""))
    return x
};
```
* (#206)反正一个单链表
1. 输入: 1->2->3->4->5->NULL   ，输出: 5->4->3->2->1->NULL

```js
var reverseList = function(head) {
    let [prev,curr] = [null,head]
    while(curr){
        let temp = curr.next
        curr.next = prev
        prev = curr
        curr = temp
    }
    return prev
    //注意返回的是prev（和head对应）
}
```

* （#70）假设你正在爬楼梯。需要 n 阶你才能到达楼顶。每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
1. 注意：给定 n 是一个正整数。
```js
var climbStairs = function(n) {
    const dp = []
    //设置dp[n]为上n级台阶有的方法数
    //则dp[n] = dp[n-1] + dp[n-2]
    dp[1] = 1
    dp[2] = 2
    for(let i=3;i<=n;i++){
        dp[i] = dp[i-1] + dp[i-2]
    }
    return dp[n]
}
```

* (#9)判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

```js
var isPalindrome = function(x) {
     if( x < 0 ) return false
    x = String(x)
    for(let i=0,len=x.length; i<len/2; i++){
        if( x[i] != x[len - i -1]) return false
    }
    return true
}
```

* (#88)给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。

1. 初始化 nums1 和 nums2 的元素数量分别为 m 和 n
2. 你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。

```js
function merge(arr1,arr2){
    let len1 = arr1.length - 1
    let len2 = arr2.length - 1
    let len = len1 + len2 + 1
    while(len2>=0){
        if(arr1[len1]>arr2[len2]){
            arr1[len] = arr1[len1]
            len1--
            len--
        }else{
            arr1[len] = arr2[len2]
            len2--
            len--
        }
    }
    return arr1
}
```

* (#14) 编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。

```js
var longestCommonPrefix = function(strs) { 
    let ans = strs[0]
    if(strs.length<=0 || ans.length<=0){
        return ""
    }
   for(let i = 0 ; i < ans.length;i++){
       for(let j = 0 ; j <strs.length;j++){
           if(ans[i]!=strs[j][i]){
                 ans =  ans.substring(0,i)
           }
       }
   }
   return ans
}
```

