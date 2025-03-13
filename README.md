# Hashedin-by-deloitte
recruitment drive question asked in 2025



## Problems and Solutions

### 1. **Stock Distribution Problem**
**Problem Statement:**
In the town of Shopville, there are `N` specialty stores and `M` different types of products available for distribution. Each store can only stock one type of product, and we aim to distribute the stock so that no store is overwhelmed. The goal is to minimize the maximum number of products allocated to any store.

**Solution Approach:**
- We use **binary search** to find the maximum stock per store (`X`).
- The function `required_stores(limit)` calculates how many stores are needed if each store can hold at most `limit` items.
- We adjust `X` using binary search to find the smallest valid maximum stock allocation.

**Python Implementation:**
```python
def minMaxStockPerStore(N, quantities):
    left, right = 1, max(quantities)

    def required_stores(limit):
        return sum((q + limit - 1) // limit for q in quantities)

    while left < right:
        mid = (left + right) // 2
        if required_stores(mid) <= N:
            right = mid
        else:
            left = mid + 1

    return left

# Example usage
N = 7
quantities = [15, 10, 5]
print(minMaxStockPerStore(N, quantities))  # Output: 5
```

---

### 2. **Minimum Operations to Type a String**
**Problem Statement:**
Ashrae needs to type a string `s` but can reduce workload by:
1. Appending one character at a time.
2. Append the entire string formed so far (only once).
The goal is to find the minimum number of operations required to type `s`.

**Solution Approach:**
- Start with an empty string and append characters one by one.
- Check if doubling the current string (`concatenation`) can reduce the number of steps.
- Use an optimal strategy to minimize operations.

**Python Implementation:**
```python
def min_operations_to_type(s):
    n = len(s)
    typed = ""
    steps = 0
    
    for i in range(n):
        typed += s[i]  # Append one character
        steps += 1  
        
        if 2 * len(typed) <= n and s.startswith(typed * 2):
            typed *= 2  # Perform concatenation
            steps += 1  
    
    return steps

# Example usage
s = "abcabca"
print(min_operations_to_type(s))  # Output: 5
```

---

### 3. **Bread Loaves Grouping for Maximum Sum of Averages**
**Problem Statement:**
Oliver, a kind bread maker, was given a task by the village chief to prepare a certain number of bread loaves for a festival. He must divide these loaves into at most `K` groups, ensuring each group has at least one loaf. The goal is to maximize the sum of the average loaves per group.

**Solution Approach:**
- Use **dynamic programming** or **binary search with greedy approach** to optimize the division.
- Ensure each group contains at least one loaf.
- Find a partitioning strategy that maximizes the sum of averages.

**Python Implementation:**
```python
def maxSumOfAverages(nums, K):
    from itertools import accumulate
    
    n = len(nums)
    prefix_sum = [0] + list(accumulate(nums))
    dp = [[0] * (K + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        dp[i][1] = prefix_sum[i] / i
    
    for k in range(2, K + 1):
        for i in range(k, n + 1):
            for j in range(k - 1, i):
                dp[i][k] = max(dp[i][k], dp[j][k - 1] + (prefix_sum[i] - prefix_sum[j]) / (i - j))
    
    return dp[n][K]

# Example usage
nums = [9, 1, 2, 3, 9]
K = 3
print(maxSumOfAverages(nums, K))  # Output: 20
```


## Contributions
Feel free to open an issue or submit a pull request if you find a bug or an optimization.


