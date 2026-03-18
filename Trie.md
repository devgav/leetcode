Core Algorithm
```python
class TrieNode:
	def __init__(self):
		self.children = [null] * 26
		self.end_of_word = False # this can change

class Trie:
	def __init__(self):
		self.root = TrieNode()
		
	def insert(self, word):
		node = self.root
		for c in word:
			idx = ord(c) - ord('a')
			if node.children[idx] is None:
				node.children[idx] = new TrieNode()
			node = node.children[idx] # move to the next node
			
		node.end_of_word = True
						
	
	def search(self, word):
		node = self.root
		for c in word:
			idx = ord(c) - ord('a')
			if node:
				node = node.children[idx]
			if not node:
				return False
		return True
```

Top K / Autocomplete / Suggestions
```python
class TrieNode:
	def __init__(self):
		self.children = [null] * 26
		self.end_of_word = False
		self.suggestions = []
		
class Trie:
	def __init__(self):
		self.root = TrieNode()
		
	def insert(self, word):
		node = self.root
		for c in word:
			idx = ord(c) - ord('a')
			if node.children[idx] is None:
				node.children[idx] = new TrieNode()
			# KEY VARIATION
			if len(node.suggestions) < 3:
				node.suggestions.append(word)
				
			node = node.children[idx] # move to the next node
			
		node.end_of_word = True
		
	def search(self, word):
		node = self.root
		result = []
		for c in word:
			idx = ord(c) - ord('a')
			if node:
				node = node.children[idx]				
				result.append(node.suggestions)
			else:
				result.append([])
		return result	
```

Counting Trie (frequency)
```python
class TrieNode:
	def __init__(self):
		self.children = [null] * 26
		self.end_of_word = False
		self.prefix_count = 0
		
class Trie:
	def __init__(self):
		self.root = TrieNode()
	
	def insert(self, word):
		node = self.root
		for c in word:
			idx = ord(c) - ord('a')
			if node.children[idx] is None:
				node.children[idx] = new TrieNode()
			node = node.children[idx]
			# KEY VARIATION
			node.prefix_count += 1
		node.end_of_word = True
```

WildCard Search
```python
class WildcardTrie:
    def __init__(self):
        self.children = {}
        self.is_end = False

    def insert(self, word):
        node = self
        for char in word:
            if char not in node.children:
                node.children[char] = WildcardTrie()
            node = node.children[char]
        node.is_end = True

    def search(self, word):
        node = self
        for i, char in enumerate(word):
            if char == '.': # Variation: Check all children recursively
                for child in node.children.values():
                    if child.search(word[i+1:]):
                        return True
                return False
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
```