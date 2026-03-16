Core Algorithm
```python
queue = deque([start_node])
visited = {start_node}
def bfs(node):
	while queue:
		top = queue.popleft()
		# process the top node
		for neighbor in graph[top]:
			if neighbor not in visited:
				visited.add(neighbor)
				queue.append(neighbor)
```

Matrix:
```python
from collections import deque

def matrix_bfs(grid):
    if not grid: return
    rows, cols = len(grid), len(grid[0])
    queue = deque([(0, 0)]) # (row, col)
    visited = set([(0, 0)])
    
    while queue:
        r, c = queue.popleft()
        
        # Define directions: Up, Down, Left, Right
        for dr, dc in [(1,0), (-1,0), (0,1), (0,-1)]:
            nr, nc = r + dr, c + dc
            
            if 0 <= nr < rows and 0 <= nc < cols and (nr, nc) not in visited:
                # Add logic for specific cell values (e.g., if grid[nr][nc] == 1)
                visited.add((nr, nc))
                queue.append((nr, nc))
```

Multi Source BFS
```python
queue = deque()
for r in range(rows):
    for c in range(cols):
        if grid[r][c] == "START":
            queue.append((r, c))
            visited.add((r, c))
# Now run standard BFS
```

Cycle Detection
```python
# undirected
def has_cycle(start_node, graph):
    queue = deque([(start_node, -1)]) # (current, parent)
    visited = {start_node}
    
    while queue:
        curr, parent = queue.popleft()
        for neighbor in graph[curr]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, curr))
            elif neighbor != parent:
                return True # Cycle detected
    return False
```
```python
# directed
from collections import deque

def has_cycle_directed(n, edges):
    # 1. Build adjacency list and calculate in-degrees
    adj = {i: [] for i in range(n)}
    in_degree = [0] * n
    for u, v in edges:
        adj[u].append(v)
        in_degree[v] += 1
    
    # 2. Add all nodes with 0 in-degree to the queue
    queue = deque([i for i in range(n) if in_degree[i] == 0])
    
    visited_count = 0
    
    while queue:
        curr = queue.popleft()
        visited_count += 1
        
        # 3. "Remove" curr and decrease in-degree of neighbors
        for neighbor in adj[curr]:
            in_degree[neighbor] -= 1
            # If in-degree becomes 0, it's ready to be processed
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
                
    # 4. If we didn't visit all nodes, there's a cycle
    return visited_count != n
```

Weighted BFS:
```python
import heapq

def dijkstra(start, graph):
    # distances[node] = shortest distance from start to node
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    
    # pq stores (distance, current_node)
    pq = [(0, start)]
    
    while pq:
        curr_dist, curr_node = heapq.heappop(pq)
        
        # If we found a longer path already, skip it
        if curr_dist > distances[curr_node]:
            continue
            
        for neighbor, weight in graph[curr_node].items():
            new_dist = curr_dist + weight
            
            # If this path is shorter, update and push to heap
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(pq, (new_dist, neighbor))
                
    return distances
```