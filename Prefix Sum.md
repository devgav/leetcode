**Core template**
```python
# 1d template
def prefix_sum(nums):
	n = len(nums)
	prefixSums = [0] * (n + 1)
	for i in range(n):
		prefixSums[i + 1] = prefixSums[i] + nums[i]

# query in range [L, R] (inclusive)
sum = prefixSums[R + 1] - prefixSums[L]
```

**Matrix:**
```python
# 2d template
def prefix_sum(matrix):
	row, col = len(matrix), len(matrix[0])
	# add padding so we don't have to check out of bounds
	prefixSum = [[0] * (col + 1) for _ in range(row + 1)]
	for r in range(row):
		for c in range(col):
			prefixSum[r + 1][c + 1] = (
				matrix[r][c] + # current number in matrix
				prefixSum[r][c + 1] + # everything above rectable has been summed
				prefixSum[r + 1][c] - # everything summed to the left
				prefixSum[r][c] # the "above" and "left" added top-left corner so substract it out
			)
	
# query in range (r1, c1) to (r2, c2)
sum = (prefixSum[r2 + 1][c2 + 1] - # 1. Total sum from (0,0) to the bottom-right of target
		prefixSum[r1][c2 + 1] - # 2. Subtract the entire "top" block above the target
		prefixSum[r2 + 1][c1] + # 3. Subtract the entire "left" block to the left of the target
		prefixSum[r1][c1]) # 4. Add back the top-left corner (it was subtracted twice in steps 2 & 3)
```

**Difference Array**
```python
def apply_range_updates(nums, updates):
    n = len(nums)
    # 1. Create a difference array
    # We use n + 1 to handle updates that reach the very last index
    diff = [0] * (n + 1)
    
    # 2. Record updates in O(1) each
    # Update format: [start_idx, end_idx, value_to_add]
    for left, right, val in updates:
        diff[left] += val
        if right + 1 < n:
            diff[right + 1] -= val
            
    # 3. Convert difference array back to actual values using Prefix Sum
    current_running_sum = 0
    for i in range(n):
        current_running_sum += diff[i]
        nums[i] += current_running_sum
        
    return nums
```

**HashMap:**
```python
def subarray_sum(nums, k):
    count = 0
    curr_sum = 0
    prefix_map = {0: 1} # {sum: frequency}
    
    for num in nums:
        curr_sum += num
        if curr_sum - k in prefix_map: # Is there a prefix we can remove to leave exactly k?
            count += prefix_map[curr_sum - k]
        prefix_map[curr_sum] = prefix_map.get(curr_sum, 0) + 1
    return count
```