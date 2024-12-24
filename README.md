# Prefix-Beauty-Sum-

In a digital world filled with binary strings, Aarav came across N unique strings, each adorned with a special beauty value. Fascinated by these strings, he decided to conduct some queries to explore their relationships.
For each query, Aarav would provide a binary string S, and his task was to discover the total beauty value of all strings that had S as a prefix. Given that the sum could grow quite large, he needed to present the results modulo 109 + 7. Can you help Aarav calculate the beauty value for each of his queries?

MOD = 1000000007

class TrieNode:
    def __init__(self):
        self.children = {}
        self.beauty_sum = 0

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, string, beauty):
        node = self.root
        for char in string:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
            node.beauty_sum = (node.beauty_sum + beauty) % MOD

    def query(self, string):
        node = self.root
        for char in string:
            if char not in node.children:
                return 0
            node = node.children[char]
        return node.beauty_sum

def prefix_beauty_sum(n, q, strings_with_beauty, queries):
    trie = Trie()
    
    # Build the Trie
    for string, beauty in strings_with_beauty:
        trie.insert(string, beauty)

    # Process Queries
    results = []
    for query in queries:
        results.append(trie.query(query))
    
    return results

# Input Reading
if __name__ == "__main__":
    n, q = map(int, input().split())
    strings_with_beauty = []
    for _ in range(n):
        A, p = input().split()
        strings_with_beauty.append((A, int(p)))
    queries = [input().strip() for _ in range(q)]
    
    # Solve the problem
    results = prefix_beauty_sum(n, q, strings_with_beauty, queries)
    print('\n'.join(map(str, results)))
