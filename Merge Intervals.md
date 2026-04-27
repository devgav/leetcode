**Core Algorithm**
```python
def mergeIntervals(intervals):
	intervals.sort(key = lambda k : k.start)
	ret = [intervals[0]]
	for current in intervals[1:]:
		prev = ret[-1]
		if prev.end >= current.start:
			prev.end = max(prev.end, current.end)
		else:
			ret.append(current)
	return ret
			
```

**Insert Interval**
```python
def insert(intervals, newInterval):
    result = []
    i = 0
    n = len(intervals)
    
    new_start, new_end = newInterval
    
    # 1. Add all intervals that come strictly before the new interval
    while i < n and intervals[i][1] < new_start:
        result.append(intervals[i])
        i += 1
    
    # 2. Merge all overlapping intervals into one big "newInterval"
    while i < n and intervals[i][0] <= new_end:
        # The new start is the minimum of the two; the new end is the maximum
        new_start = min(new_start, intervals[i][0])
        new_end = max(new_end, intervals[i][1])
        i += 1
    
    # Add the final merged version of the new interval
    result.append([new_start, new_end])
    
    # 3. Add all remaining intervals that come after
    while i < n:
        result.append(intervals[i])
        i += 1
        
    return result
```