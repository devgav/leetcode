```python 
class UnionFind:
	def __init__(self, size):
		self.size = size
		self.parent = list(range(size))
		self.rank = [0] * size
	def find(self, x):
		if x != self.parent[x]:
			self.parent[x] = self.find(self.parent[x])
		return self.parent[x]
		
	def union(self, x, y):
		root_x = self.find(x)
		root_y = self.find(y)
		
		if root_x == root_y:
			return False
		
		# link x and y the smaller one is linked to the larger ranked value
		if self.rank[root_x] < self.rank[root_y]:
			self.parent[root_x] = root_y
		elif self.rank[root_x] > self.rank[root_y]:
			self.parent[root_y] = root_x
		else:
			self.parent[root_y] = root_x
			self.rank[root_x] += 1
		return True
			
```