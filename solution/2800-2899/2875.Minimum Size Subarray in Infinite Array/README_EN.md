# [2875. Minimum Size Subarray in Infinite Array](https://leetcode.com/problems/minimum-size-subarray-in-infinite-array)

[中文文档](/solution/2800-2899/2875.Minimum%20Size%20Subarray%20in%20Infinite%20Array/README.md)

## Description

<p>You are given a <strong>0-indexed</strong> array <code>nums</code> and an integer <code>target</code>.</p>

<p>A <strong>0-indexed</strong> array <code>infinite_nums</code> is generated by infinitely appending the elements of <code>nums</code> to itself.</p>

<p>Return <em>the length of the <strong>shortest</strong> subarray of the array </em><code>infinite_nums</code><em> with a sum equal to </em><code>target</code><em>.</em> If there is no such subarray return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,2,3], target = 5
<strong>Output:</strong> 2
<strong>Explanation:</strong> In this example infinite_nums = [1,2,3,1,2,3,1,2,...].
The subarray in the range [1,2], has the sum equal to target = 5 and length = 2.
It can be proven that 2 is the shortest length of a subarray with sum equal to target = 5.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,1,1,2,3], target = 4
<strong>Output:</strong> 2
<strong>Explanation:</strong> In this example infinite_nums = [1,1,1,2,3,1,1,1,2,3,1,1,...].
The subarray in the range [4,5], has the sum equal to target = 4 and length = 2.
It can be proven that 2 is the shortest length of a subarray with sum equal to target = 4.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,4,6,8], target = 3
<strong>Output:</strong> -1
<strong>Explanation:</strong> In this example infinite_nums = [2,4,6,8,2,4,6,8,...].
It can be proven that there is no subarray with sum equal to target = 3.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>1 &lt;= target &lt;= 10<sup>9</sup></code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python

```

### **Java**

```java
class Solution {
    public int shortestSubarray(int[] nums, int k) {
        int n = nums.length;

        int minLength = n * 2 + 1;
        int l = 0;
        int sum = 0;

        for (int r = 0; r < n * 2; r++) {
            int start = l % n;
            int end = r % n;
            sum += nums[end];

            while (sum > k && l <= r) {
                start = l % n;
                sum -= nums[start];
                l++;
            }

            if (sum == k) {
                minLength = Math.min(minLength, r - l + 1);
                start = l % n;
                sum -= nums[start];
                l++;
            }
        }

        return minLength == n * 2 + 1 ? -1 : minLength;
    }
    public int minSizeSubarray(int[] nums, int target) {
        int n = nums.length;
        int sum = 0;

        for (int num : nums) {
            sum += num;
        }
        int k = target % sum;
        int ans = target / sum * n;
        if (k == 0) {
            return ans;
        }
        int res = shortestSubarray(nums, k);
        return res == -1 ? -1 : ans + res;
    }
}

```

### **C++**

```cpp

```

### **Go**

```go

```

### **...**

```

```

<!-- tabs:end -->