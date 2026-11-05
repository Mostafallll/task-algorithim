import time
import random
import sys
from collections import deque
import matplotlib.pyplot as plt

sys.setrecursionlimit(2000000)

class Graph:
    def __init__(self):
        self.adj = {}

    def add_vertex(self, u):
        if u not in self.adj:
            self.adj[u] = []

    def add_edge(self, u, v, directed=False):
        self.add_vertex(u)
        self.add_vertex(v)
        self.adj[u].append(v)
        if not directed:
            self.adj[v].append(u)

    def bfs(self, start):
        if start not in self.adj:
            return []
        visited = set([start])
        queue = deque([start])
        order = []
        while queue:
            node = queue.popleft()
            order.append(node)
            for neighbor in self.adj[node]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
        return order

    def dfs_iterative(self, start):
        if start not in self.adj:
            return []
        visited = set()
        stack = [start]
        order = []
        while stack:
            node = stack.pop()
            if node not in visited:
                visited.add(node)
                order.append(node)
                for neighbor in reversed(self.adj[node]):
                    if neighbor not in visited:
                        stack.append(neighbor)
        return order

    def dfs_recursive(self, start):
        if start not in self.adj:
            return []
        visited = set()
        order = []
        def _dfs(node):
            visited.add(node)
            order.append(node)
            for neighbor in self.adj[node]:
                if neighbor not in visited:
                    _dfs(neighbor)
        _dfs(start)
        return order


def run_tests():
    print("=" * 50)
    print("TEST CASES")
    print("=" * 50)

    g_empty = Graph()
    print("1. Empty Graph:")
    print("   BFS:", g_empty.bfs(1))
    print("   DFS Iterative:", g_empty.dfs_iterative(1))
    print("   DFS Recursive:", g_empty.dfs_recursive(1))

    g_single = Graph()
    g_single.add_vertex(1)
    print("
2. Single Vertex:")
    print("   BFS:", g_single.bfs(1))
    print("   DFS Iterative:", g_single.dfs_iterative(1))
    print("   DFS Recursive:", g_single.dfs_recursive(1))

    g_disc = Graph()
    g_disc.add_edge(1, 2)
    g_disc.add_edge(3, 4)
    print("
3. Disconnected Graph (start at 1):")
    print("   BFS:", g_disc.bfs(1))
    print("   DFS Iterative:", g_disc.dfs_iterative(1))
    print("   DFS Recursive:", g_disc.dfs_recursive(1))

    g_cycle = Graph()
    g_cycle.add_edge(1, 2)
    g_cycle.add_edge(2, 3)
    g_cycle.add_edge(3, 1)
    print("
4. Cycle Graph:")
    print("   BFS:", g_cycle.bfs(1))
    print("   DFS Iterative:", g_cycle.dfs_iterative(1))
    print("   DFS Recursive:", g_cycle.dfs_recursive(1))

    g_tree = Graph()
    g_tree.add_edge(1, 2)
    g_tree.add_edge(1, 3)
    g_tree.add_edge(2, 4)
    g_tree.add_edge(2, 5)
    print("
5. Tree Graph:")
    print("   BFS:", g_tree.bfs(1))
    print("   DFS Iterative:", g_tree.dfs_iterative(1))
    print("   DFS Recursive:", g_tree.dfs_recursive(1))


def measure_performance():
    v_sizes = [1000, 5000, 10000, 20000, 40000]
    ve_vals = []
    bfs_times = []
    dfs_iter_times = []
    dfs_rec_times = []

    for v in v_sizes:
        e = v * 3
        g = Graph()
        for i in range(v):
            g.add_vertex(i)
        for _ in range(e):
            u = random.randint(0, v - 1)
            w = random.randint(0, v - 1)
            g.add_edge(u, w)

        ve_vals.append(v + e)

        t0 = time.time()
        g.bfs(0)
        bfs_times.append(time.time() - t0)

        t0 = time.time()
        g.dfs_iterative(0)
        dfs_iter_times.append(time.time() - t0)

        t0 = time.time()
        g.dfs_recursive(0)
        dfs_rec_times.append(time.time() - t0)

    plt.figure(figsize=(10, 5))
    plt.plot(ve_vals, bfs_times, marker='o', label='BFS')
    plt.plot(ve_vals, dfs_iter_times, marker='s', label='DFS Iterative')
    plt.plot(ve_vals, dfs_rec_times, marker='^', label='DFS Recursive')
    plt.title('Graph Traversal Performance O(V + E)')
    plt.xlabel('V + E')
    plt.ylabel('Time (seconds)')
    plt.grid(True)
    plt.legend()
    plt.savefig('graph_benchmark.png')
    print("
Benchmark saved as graph_benchmark.png")


def solve_maze(grid, start, end):
    rows, cols = len(grid), len(grid[0])
    queue = deque([start])
    visited = {start: None}

    while queue:
        curr = queue.popleft()
        if curr == end:
            break
        r, c = curr
        for dr, dc in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 0:
                nxt = (nr, nc)
                if nxt not in visited:
                    visited[nxt] = curr
                    queue.append(nxt)

    if end not in visited:
        return None

    path = []
    curr = end
    while curr is not None:
        path.append(curr)
        curr = visited[curr]
        
    return path[::-1]


def run_mini_project():
    print("
" + "=" * 50)
    print("MINI PROJECT: MAZE SOLVER")
    print("=" * 50)
    maze = [
        [0, 1, 0, 0, 0],
        [0, 1, 0, 1, 0],
        [0, 0, 0, 1, 0],
        [1, 1, 0, 0, 0],
        [0, 0, 0, 1, 0]
    ]
    start = (0, 0)
    end = (4, 4)
    path = solve_maze(maze, start, end)
    print("Maze Layout (0 = open, 1 = wall):")
    for r in maze:
        print(" ", r)
    print(f"
Start: {start}, End: {end}")
    print("Shortest Path:", path)


if __name__ == "__main__":
    run_tests()
    measure_performance()
    run_mini_project()
