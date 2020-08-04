# Internship Notes

## Database Management Systems

### Topics to cover

      [1] ER Diagram
      [2] Conversion of ER into Relational Model
      [3] Basis of Relational Models and Functional Dependency
      [4] Idea about Keys/ Types
      [5] Normalization
      [6] Lossless decomposition and Dependency Preserving
      [7] Indexing and Physical Structure (B, B+ Trees)
      [8] SQL
      [9] Relational Algrbra and Relational Calculus
      [10] Transactions
      [11] Concurrency Control

#### 0. Basics

1. Data: Raw and isolated facts about an entitiy is called data.
2. Information: Processed, meaningfull and usable data
3. Database: Collection of similar/related data.
4. DBMS: Software used to create, manipulate and delete database.

What are the drawbacks of File System?

- Data Redundancy
- Data Inconsistency (Same data has multiple values)
- Difficult in accessing data
- Atomicity Problem (Either complete it or dont do at all)
- Data Isolation (data is separate from the language used in coding the software)
- Security Problem
- Concurrency Anomalies
- Integrity Problem

#### ER Diagram

- Entity: An entitiy is an object in the real world and that is distingushable from other objects based on the values of the attributes it possesses.

- Types of Entities

  - Tangible: Entities which physically exist in real world.
  - Intangible: Entitites which exist logically.

- Entitiy Set: Collectioin of same types of entities is called as an Entitiy Set.
  It is represented with a Rectangle.

#### Attributes

They are the units that describe the characteristics of entities.  
For each attribute, there is a set of permitted value, called domain.  
Attributes are represented by an Oval.

Types of Attributes:

1. Simple: Cannot be divided further.
2. Composite: Can be divided further (Name -> first name, last name)

3. Single Valued: Can only have 1 value per instance
4. Multi Valued: Can have multiple values. For these, separate table is made.

5. Stored: Whose value is stored in the DB.
6. Derived: Whose value isnt stored, but you can get it from some other stored attribute

#### Relationship

It is an association between two or more entities of same or different type.

- Individual relationship between entities is not represented in an ER Diagram.

**Relationship Type**: A set of similar types of relationship is represented in ER Diagram using a diamond.

    teacher --- <teaches> --- student

Every realtionship has 3 components:

- Cardinality
- Degree
- Name

**Degree of a Relationship**  
It means the number of entitiy sets which participate in the relationship set  
They can be Binary, Ternary, Quaternary etc.

Unary relationships are also possible, eg: Employee can have relation with other employees, like boss, manager etc.

There is no limit on the degree of a relationship, but higher degrees are not possible, most of them are binary only.

**Cardinality Ratio**  
Expresses the number of entities to which other entity can be related by a relationship.

These are the following types:

- One to One
- One to Many
- Many to One
- Many to Many

1.  One to One  
    When every entitiy on one side can relate to **at max** one entity on other side and vice versa.  
    eg: Aadhar Number and Citizen.  
    In ER, the edge either has 1 written on it, or it has arrow ->

2.  One to Many  
    Every entitiy on one side can relate to many entities on other side, but reverse can only have 1 entitiy.

        -> is 1 in ER and no arrow is Many

3.  Many to One  
    Same as previous one, just reversed.

4.  Many to Many  
    Every entitiy on one side can be related to many entities on the other side and vice versa. If there are no arrows on the ER Diagram, then it is many to many, or many can have a \* on it.

## Object Oriented Programming

**Object Oriented Programming** is a methodology to design a program using classes and objects. It simplifies development and maintence by providing some concepts, like:

- Object
- Class
- Inheritance
- Polymorphism
- Abstraction
- Encapsulation

#### Object

1. Objects have a state and behaviour
2. It is an instance of a class

## Data Structures and Algorithms

## Hashing

Hashing is an improvement over Direct Access Table. The idea is to use hash function that converts a given phone number or any other key to a smaller number and uses the small number as index in a table called hash table.

#### Hash Function

A function that converts a given, (for example) big phone number to a small practical integer value. The mapped integer value is used as an index in hash table. In simple terms, a hash function maps a big number or string to a small integer that can be used as index in hash table.

A good hash function should have following properties:

1. Efficiently Computable
2. Should Uniformly Distribute Keys

#### Direct Access Table

In this, the values to be stored are used as indices directly. This is not useful for very big numbers, because getting that many indices isnt possible.

### Hash Table

When Hash tables are used, a hashingfunction is generated to get the hash values for inputs. And those hashed values are used as indices in a hash table.

Since a hash function generates a small number for a very big number, there might be cases where two keys result in the same hashed value.

The situation where a new key maps to an already occupied slot in hash table is called Collision.

These collisions must be handled. These are the ways to handle collisions:

1. **Chaining**: The idea is to make each cell of the hash table to point at a linked list of record values which have the same hash value. This is simple but it requires extra memory.

2. **Open Adressing**: In open addressing, all the elements are stored in the hash table itself. Each cell contains either a record or NIL.
   When searching the element, we one by one go through the table slots, until desired element is found, or it is clear that the element does not exist.

## Graph Algorithms

**Common Graph Theory Problems**

1. Shortest Path Problem

   - BFS (for Unweighted Graph)
   - DJ's Shortest
   - Bellman-Ford
   - Floyd Warshall

2. Connectivity

   - Union Find
   - DFS/BFS

3. Negative Cycle

   - Bellman Ford
   - Floyd Warshall

4. Strongly Connected Components

   - Tarjan's
   - Kosaraju

5. Travelling Salesman Problem

   - Held-Karp
   - Branch and Bound

6. Bridges
7. Articulation Points
8. Minimum Spanning Tree

   - Primm's Algorithm
   - Krushkal's Algorithm

9. Max flow
   - Ford Fulkerson
   - Dinic

#### 1. BFS

Time Complexity: O(V+E)

```c++
  queue<int> q;
  int curr = 0;

  q.push(curr);
  vector<int> res;

  while(!q.empty()) {
    int n = q.front();
    res.push_back(n);
    q.pop();

    for(int neighbor : g[n]) {
      q.push(neighbor);
    }
  }

  return res;
```

BFS can be used to generate the shortest path from source to destination of an unweighted graph.
Here is the psuedocode for it.

```c++
//We will generate a parent array, and then reconstruct the path from s -> e using that parent array
int n; //This is the number of nodes present in the graph
vector<vector<int>> g; //This is the adjacency list representation of a graph

vector<int> parent(n, -1);
vector<bool> visited(n, false);
vector<int> res;

//This function will populate the parent array
void bfs(int s) {
  queue<int> q;
  q.push(s);

  while(!q.empty()) {
    int curr = q.front();
    q.pop();
    visited[curr] = true;
    for(int neighbour : g[curr]) {
      if(!visited[neighbour]) {
        q.push(neighbour);
        parent[neighbour] = curr;
      }
    }
  }
}

vector<int> reconstructPath(int source, int destination) {
  while(parent[destination] != -1) {
    res.push_back(destination);
    destination = parent[destination];
  }
  reverse(res.begin(), res.end());
  if(res[0] == source)
    return res;
  return {};
}
//Res now contains the shortest path from s to e
```

BFS Can also be applied on a matrix, see implementation a little bit, should be easy. Check if questions are there on leetcode.

BFS on a matrix can be done with having a queue for each dimension, as it is easier to work with. We can have parent matrix as before to trace down the shortest path that we have constructed.

#### 2. DFS

Time Complexity: O(V+E)

```c++
  stack<int> st;
  int curr = 0;

  st.push(curr);
  vector<int> res;
  while(!st.empty()) {
    int n = st.top();
    st.pop();

    for(int neighbour : g[i]) {
      st.push(neighbour);
    }
  }

  return res;
```

#### 3. Detect Cycle in a DAG

```c++
  unordered_set<int> white;
  unordered_set<int> gray;
  unordered_set<int> black;

  //Graph is represented as adjacent list
  vector<vector<int>> g;
  //Put All Nodes in white set first

  bool hasCycle (int curr) {
    //move the curr from white set to gray set
    white.erase(curr);
    gray.insert(curr);

    for(int neighbour: g[curr]) {
      if(gray.find(neighbour) != gray.end())
        return true;

      if(black.find(neighbour) != black.end())
        continue;

      if(white.find(neighbour) != white.end()) {
        if(hasCycle(neighbour))
          return true;
      }
    }

    gray.erase(curr);
    black.insert(curr);
    return false;
  }
```

#### 4. DJ's Shortest Path

Time Complexity: O(E log(E))

E = <sup>V</sup>C<sub>2</sub>, in worse case, which is V<sup>2</sup>  
Substituting it in the equation, we get:  
Time Complexity: O(2E log(V))

```c++
  int n; // -> Number of nodes in the graph
  vector<vector<int>> g; //Graph as a adjacency List
  vector<int> dis(n, INT_MAX); //Distance array, will contain the shortest distance from source
                               //to i th node at dis[i];
  priority_queue<pair<int, int> , vector<pair<int,int>>, greater<pair<int, int>>> pq;
  //This priority queue will contain a pair of: distance, node

  //This array can be used to build the shortest path
  vector<int> prev(n, -1);


  int source;
  dis[source] = 0;

  pq.push({0, source});

  while(!pq.empty()) {
    int u = pq.top().first;
    int w = pq.top().second;
    pq.pop();

    if(w > dis[u])
      continue;

    for(pair<int,int> neighbour: g[u]) {
      int v = neighbour.first;
      int c = neighbour.second;

      if(dis[v] > dis[u] + c) {
        dis[v] = dis[u] + c;
        prev[v] = u;
        pq.push({dis[v], v});
      }

    }
  }

  return dis;
```

#### 5. Bellman-Ford SSSP Algorithm

This is a much slower algorithm than DJ's shortest path, as this is a O(VE) complexity algorithm  
This is chosen when the graph contains negative cycle, because then DJ's doesnt work.

```c++
int v; //number of nodes
int e; //number of edges
int s; //starting node
vector<int> dist(v, INT_MAX);
dist[s] = 0;
//Input graph is converted to edge list:
// vector<vector<int>> edge; (src, des, weight)
vector<vector<int>> edges;

for(int i = 0; i < v-1; i++) {
  for(int j = 0; j < e; j++ ) {
    int src = edges[j][0];
    int des = edges[j][1];
    int w = edges[j][2];

    if(dist[src] != INT_MAX && dist[src] + w < dist[des]) {
      dist[des] = dist[src] + w;
    }
  }
}

//Run algorithm 2nd time to change all the negative cycle weights
for(int i = 0; i < V-1; i++) {
  for(int j = 0; j < e; j++) {
    int src = edges[j][0];
    int des = edges[j][1];
    int w = edges[j][2];

    if(dist[src] == INT_MIN || dist[src] + w < dist[des]) {
      dist[des] = INT_MIN;
    }
  }
}
```

#### 6. Floyd-Warshall Algorithm (All Pair Shortest Path)

This algorithm can find shortest path between all pairs of nodes. This algorithm runs in O(V<sup>3</sup>).

Here, we will use Adjacency Matrix representation of graph, which has g[i][j] as edge weight.
No edge should be represented with INT_MAX.

#### 7. Topological Sort

Time Complexity: O(V+E)  
The graph MUST be a DAG for a valid topo sort to exist. We will get size of topo sort output < n if it is not a DAG.

```c++
  //Graph is assumed to be taken as an adjacency list
  //populate the indeg array with the indegree of each node
  int n; //number of nodes in the graph
  vector<int> indeg(n); //populate this

  queue<int> q;
  for(int i = 0; i < indeg.size(); i++) {
    if(indeg[i] == 0)
      q.push(i);
  }

  vector<int> res;

  while(!q.empty()) {
    int curr = q.front();
    q.pop();

    res.push_back(curr);

    for(int neighbour: g[curr]) {
      indeg[neighbour]--;
      if(indeg[neighbour] == 0)
        q.push(neighbour);
    }
  }

  return res;
```

We can also use DFS to run topological sort. Before returning from the DFS function, we can push the current node in a stack. Then, we can empty this stack in a array, and that will be our Topo sorted output. This means, decreasing order of departure time (I think).

```c++
int n; //The number of nodes in the graph
vector<vector<int>> g; //The graph is assumed to be in adjacency list form
stack<int> st;
vector<bool> visited(n, false);

void topoHelper(int curr) {
  visited[curr] = true;

  for(int neighbour : g[curr]) {
    if(visited[neighbour]) {
      topoHelper(neighbour);
    }
  }
  st.push(curr);
}

vector<int> res;

while(!st.empty()) {
  res.push_back(st.top());
  st.pop();
}

//Res now contains the topological sorted graph.
```

#### 8. Single Source Shortest Path, for any DAG

We can calculate SSSP for a DAG, whether it contains negative edges or not using this method. We need to have a topological sorting, and then, we will go through the nodes 1 by 1 in order of their topology sort, and update the distance for minimum length of the path for each children.

This is O(V+E)

```c++
// Graph is adjacency list of pair<int,int>, first is destination of edge, and second is the edge weight.
vector<int> dagShortestPath(vector<vector<pair<int,int>>> &g, int start, int numNodes) {
  vector<int> topo;
  topologicalSort(g, topo);

  vector<int> dist(numNodes, INT_MAX);
  dist[start] = 0;

  for(int i = 0; i < numNodes; i++) {
    int nextNode = topo[i];

    if(dist[nextNode] != INT_MAX) {
      for(pair<int,int> neighbour : g[nextNode]) {
        int currDist = dist[nextNode] + neighbour.second;
        int v = neighbour.first;

        if(dist[v] > currDist)
          dist[v] = currDist;

      }
    }
  }

  return dist;
}
```

#### 9. Longest Path

This is NP-Hard for general graphs, but for DAGs, this can be done in O(V+E).

For DAG, we can multiply all Edge weights with -1 and then find the shortest path. Multiply this with -1 to get the longest path.

#### 10. Krushkal's Minimum Spanning Tree

This uses a greedy approach to create a minimum spanning tree.  
The Steps involved are as follows:

- Choose the minimum edge weight among all the edges that are present.
- If adding this edge creates a cycle, move on. Other wise add this edge.

To find whether a cycle is created or not, we can use union find to check it.
We can add edges between 2 trees, but we cannot add an edge within a tree it self.  
So, if we find an edge between 2 nodes who's parents are the same, it will result in a cycle.  
If we add an edge between 2 nodes who's parents are different, it will not create a cycle. We then have to merge these 2 trees into 1.

```c++
//Input graph is processed, to get an array of <edge weight, <src, dest>>
//This is sorted.
int nodes; //Number of nodes.
int edges; //Number of edges.

//We initialize the parent array with all i
vector<int> parent(nodes);
for(int i = 0; i < nodes; i++) {
  parent[i] = i;
}

int root (int n) {
  while(parent[n] != n) {
    n = parent[n];
  }
  return n;
}

void unionify(int a, int b) {
  int parentA = root(a);
  int parentB = root(b);

  parent[parenA] = parentB;
}

int krushkal(vector<pair<int, pair<int,int> > > &edge) {
  int x, y;
  long long int cost, minimumCost = 0;

  vector<pair<int, int> > addedEdges;
  //We need to run this for n-1 additions
  for(int i = 0; i < edge.size(); i++) {
    x = edge[i].second.first; //src
    y = edge[i].second.second; //dest

    cost = edgs[i].first;

    if(root(x) != root(y)) {
      minimumCost+=cost;
      addedEdges.push_back({x,y});
      unionify(x,y);
    }
  }
  return minimumCost;
}

```

#### 11. Articulation Points and Bridges

**Bridge**  
Any edge, which when removed, increases the number of connected components in the graph  
**Articulation Points**  
Any vertex, which when removed, increases the number of connected components in the graph

## Concurrency

#### Race Condition

At least 2 processes working on a shared piece of data, and eventual output is dependant on the order in which these process are run.
This will lead to data inconsistency, which we cannot afford to have.

This is the problem that we have to solve.

This problem happened because these processes were working on shared data.
If we restricted this access, ie, if we didnt let 2 processes work on same data at the same time then this problem will be solved.

##### Critical Section Problem

If you have 2 processes, p1 and p2, and both these processes have critical sections, cs1 and cs2 (critial section: Part of code which accesses the shared data).
Now problem reduces to: Making these critical sections work sequentially

We can have a flag. As long as flag is 1, that means someone else is using the Critical section, once it's 0, only then it can be used

```c++
1. while(flag == 0) {
2.    flag = 1;
3.    cs;
4.    flag = 0;
5. }
```

If we can have a condition that while loop check and flag = 1 can only either both be executed, or none of them be executed.

ie, make line 1 and 2 Atomic. If a set of instructions are atomic, you cannot divide them further. So, either all of them will execute or none of them will execute.

##### Who can make this atomic? Which entitity is responsible to make this atomic?

Our Program cannot make this atomic, as it is running on the system.
The Entitiy which runs it can make it atomic. The Entitiy which schedules these processes can do this. This entity is OS.

We are reliant on the OS to ensure that line 1 and 2 are atomic.

This is known as a **Mutex Lock**. Program can communicate to OS about what it wants to be atomic, OS then makes it atomic.

**Mutex Lock** is known as Mutual Exclusion Law

We are testing a variable, and then setting the value of it. This is known as testing and setting.

What facility do we want from the OS?
If a program calls a function "Lock", the OS should check for the shared variable, and block if the shared variable is being used, if not, set it, and come out.

As soon as one entity is done using the shared variable, the OS will unblock the shared variable and hence next/other process can use it.

The Code for it will look something like this:

```
LOCK(); Line 1 and 2 are executed by one process.
CS
UNLOCK();
```

If one process locks, then another process wont be able to use it. It will be stuck in that lock and then it will keep trying till lock gets free. OS will make sure atomicity is there.

#### How will Lock be implemented?

Do we want the process to loop or sleep?
We would prefer for it to sleep, because if it is looping, it is waiting CPU Time.

If it is looping, then it is known as Busy Waiting.

_Parallelism vs Concurrency, Check the diference._

#### Condition Variables
