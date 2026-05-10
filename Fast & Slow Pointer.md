Use Cases: 
- Cycle Detection
-  Middle of Linkedlist
- lenght of a cycle 
- reorder or split linkedlist
- find duplicate number in array

**Cycle Detection**
```python
def isCycle(node):
	if not node:
		return False
	slow = node
	fast = node
	while fast is not None and fast.next is not None:
		slow = slow.next
		fast = fast.next.next
		if slow == fast:
			return True
	return False
```

**Middle of LinkedList**
```python
def find_middle(node):
	
```