# Minimum Spanning Tree

## Minimum Spanning Tree (MST)

A **spanning tree** is defined as a tree-like subgraph of a connected, undirected graph that includes all the vertices of the graph. Or, to say in Layman’s words, it is a subset of the edges of the graph that forms a tree (**acyclic**) where every node of the graph is a part of the tree.

The minimum spanning tree has all the properties of a spanning tree, with an added constraint of having the minimum possible weights among all possible spanning trees. Like a spanning tree, there can also be many possible MSTs for a graph.

![Minimum Spanning Tree (MST)](https://media.geeksforgeeks.org/wp-content/uploads/20200316173940/Untitled-Diagram66-3.jpg)

> Above texts are taken from [Geek for geeks](https://www.geeksforgeeks.org/what-is-minimum-spanning-tree-mst/)

Now, let's dive deeper with two different algorithms for getting your MST 🙃.

## Kruskals

### Disjoint Set

Before kruskals let's consider disjoint sets. More information is available here,

{% embed url="https://www.geeksforgeeks.org/introduction-to-disjoint-set-data-structure-or-union-find-algorithm/" %}
Disjoint sets
{% endembed %}

Here, we are separating each set from other by setting a root for a certain part.

```cpp
#include <bits/stdc++.h>
using namespace std;

int parent[INT_MAX];

void makeSet(int n) {
  for (int i = 0; i <= n; i++)
    parent[i] = i;
}

int find(int n) {
  if (parent[n] == n) return n;
  int result = find(parent[n]);
  parent[n] = result;
  return result;
}

void unite(int i, int j) {
  parent[find(i)] = find(j);
}

int main() {
  makeSet(1e6);
  unite(1024, 2048);
  unite(2048, 4096);
  cout << find(1024) << endl;
  cout << find(2048) << endl;
  cout << find(4096) << endl;
  return 0;
}
```

### Actual kruskal

If you have the disjoint, you can sort your data and use the set to do the MST!

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<pair<int, pair<int, int>>> edges;
int parent[INT_MAX];

void makeSet(int n) {
  for (int i = 0; i <= n; i++)
    parent[i] = i;
}

int find(int n) {
  if (parent[n] == n) return n;
  int result = find(parent[n]);
  parent[n] = result;
  return result;
}

void unite(int i, int j) {
  parent[find(i)] = find(j);
}

void addEdges(int i, int j, int k) {
  edges.push_back({k, {i, j}});
}

void kruskal() {
  sort(edges.begin(), edges.end());
  int weight = 0;
  for (auto it: edges) {
    int i = it.second.first;
    int j = it.second.second;
    int k = it.first;
    if (find(i) != find(j)) {
      unite(i, j);
      cout << i << " " << j << " " << k << endl;
      weight += k;
    }
  }
  cout << "Weight: " << weight << endl;
}

int main() {
  makeSet(1e6);
  
  addEdges(0, 1, 10);
  addEdges(1, 3, 15);
  addEdges(2, 3, 4);
  addEdges(2, 0, 6);
  addEdges(0, 3, 5);
  kruskal();

  return 0;
}
```
