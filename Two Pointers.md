hint at when to use: 
- when you need to find a  set of elements (pair, triplet, or subarray) that fulfill a certain constraint

**Core Algorithm**
```python
def two_pointers(arr):
	arr.sort() # sort if not already sorted
	left = 0
	right = len(arr) - 1
	while left < right:
		left_val = arr[left]
		right_val = arr[right]
		if compare_left_right: # some condition is met
			# update pters
	return #answer
```

**Shrinking Window**
```python
def two_pointers(arr):
	arr.sort()
	left = 0
	right = len(arr) - 1
	while left < right:
		left_val = arr[left]
		right_val = arr[right]
		while compare_left_right: # some condition is met
			# perform some action
			left += 1
	return #answer
```