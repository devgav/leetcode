```python
def reverse_linkedlist(node):
	prev, curr, next = None, node, None
	while node:
		next = curr.next
		curr.next = prev 
		prev = curr
		curr = next
	return prev
```