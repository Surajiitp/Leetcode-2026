# LeetCode 2144 - Minimum Cost of Buying Candies With Discount

## Problem Statement

A store offers a discount where for every three candies purchased, the cheapest candy among them is free.

Given an integer array `cost`, where `cost[i]` is the price of the ith candy, return the minimum cost needed to buy all the candies.

## Approach

### Greedy Strategy

To maximize the discount:

1. Sort the candies in descending order.
2. Process candies in groups of three.
3. Pay for the first two candies.
4. Get the third (cheapest in the group) for free.

This ensures that the free candy has the highest possible value.

## Algorithm

1. Sort the array in descending order.
2. Traverse the array.
3. Add the cost of the first two candies in every group of three.
4. Skip every third candy.

## C++ Solution

```cpp
class Solution {
public:
    int minimumCost(vector<int>& cost) {
        sort(cost.begin(), cost.end(), greater<int>());

        int ans = 0;

        for (int i = 0; i < cost.size(); i++) {
            if ((i + 1) % 3 != 0) {
                ans += cost[i];
            }
        }

        return ans;
    }
};
```

## Example

### Input

```text
cost = [6,5,7,9,2,2]
```

### Sorted Array

```text
[9,7,6,5,2,2]
```

### Calculation

```text
Pay: 9 + 7
Free: 6

Pay: 5 + 2
Free: 2
```

### Output

```text
23
```

## Complexity Analysis

* Time Complexity: O(n log n)
* Space Complexity: O(1)

## Topics

* Greedy
* Sorting
* Arrays

## LeetCode Link

https://leetcode.com/problems/minimum-cost-of-buying-candies-with-discount/
