
**Core Algorithm**
Time Complexity: O(V + E)
Space Complexity: O(V)
```python
def dfs(node):
	if node in visited:
		return
	
	visited[node] = True
	print("Processing the node")
	
	for neighbor in graph[node]:
		dfs(neighbor)
```

**Matrix**:
When to use: 
	- when given an n x m array n = row, m = col

```python
visited = set()
row, col = len(matrix), len(matrix[0])
def dfs_matrix(rowIdx, colIdx):
	# hit a wall/edge
	if rowIdx < 0 or rowIdx >= row or colIdx < 0 or colIdx >= col:
		return
	if (row, col) in visited:
		return
	visited.add((row, col))
	print("Processing the node")
	directions = [[0, 1], [0, -1], [1, 0], [-1, 0]]
	for dr, dc in directions:
		dfs(rowIdx + dr, colIdx + dc)
```

**Adjacency List**:
When to use:  
```python
# directed
def build_adj_list_directed(nodes_list):
	adjList = defaultdict(list)
	for key, val in nodes_list:
		adjList[key].append(val)
	return adjList

# undirected
def build_adj_list_undirected(nodes_list):
	adjList = defaultdict(list)
	for key, val in nodes_list:
		adjList[key].append(val)
		adjList[val].append(key)
	return adjList
```

**Connected Components**:
When to use:  
	- Counting Groups
	- Grouping Data
	- Reachibility
Key "trigger" phrase: 
	- "How many **distinct groups** are there"
	- Find the **number of islands**
	- Determine **if graph is fully connected**
	- Count the **number of provinces**
```python
def dfs(node):
	if node in visited:
		return
	visited.add(node)
	for neighbor in adjList[node]:
		dfs_adj_list(neighbor)

# global loop allows us to find new components that are disconnected
for node in range(num_of_nodes):
	if node not in visited: # tells us that we have reached a new node
		# do something - inc count, process something
		dfs(node)
```

**Cycle Detection**:
When to use:  
Key "trigger" phrase:
- if there's no possible path return none
- 
```python
# for directed graph
visited = set()
visiting = set()
def dfs(node):
	if node in visiting: # node we are currently visiting
		return True
	if node in visited: # node is not part of a cycle
		return False
	visiting.add(node)
	
	for neighbor in adjList[node]:
		if dfs(neighbor):
			return True
	# BACKTRACK
	visiting.remove(node)
	visited.add(node)
	# do something 
	return False
for i in range(n):
	if i not in visited:
		if dfs(i): return True
return False
```
```python
# for undirected graphs
def has_cycle_undirected(n, edges):
    adj = defaultdict(list)
    for u, v in edges:
        adj[u].append(v)
        adj[v].append(u)
        
    visited = set()

    def dfs(node, parent):
        visited.add(node)
        
        for neighbor in adj[node]:
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True
            # If neighbor is visited and NOT the node we just came from
            elif neighbor != parent:
                return True
        return False

    for i in range(n):
        if i not in visited:
            # Start DFS with parent as -1 or None
            if dfs(i, -1): return True
    return False
```
**Backtracking**:
When to use:  
Key "trigger" phrase:
```python

```

**Topological Sort**:
When to use:  
Key "trigger" phrase:
```python

```