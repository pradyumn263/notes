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

#### 1. ER Diagram

- Entity: An entitiy is an object in the real world and that is distingushable from other objects based on the values of the attributes it possesses.

- Types of Entities

  - Tangible: Entities which physically exist in real world.
  - Intangible: Entitites which exist logically.

- Entitiy Set: Collectioin of same types of entities is called as an Entitiy Set.

## Object Oriented Programming

**Object Oriented Programming** is a methodology to design a program using classes and objects. It simplifies development and maintence by providing some concepts, like:

- Object
- Class
- Inheritance
- Polymorphism
- Abstraction
- Encapsulation

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

#### 1. BFS

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

#### 2. DFS

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

```c++
  int n; // -> Number of nodes in the graph
  vector<vector<int>> g; //Graph as a adjacency List
  vector<int> dis(n, INT_MAX); //Distance array, will contain the shortest distance from source
                               //to i th node at dis[i];
  priority_queue<pair<int, int> , vector<pair<int,int>>, greater<pair<int, int>>> pq;
  //This priority queue will contain a pair of: distance, node

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
        pq.push({dis[v], v});
      }

    }
  }

  return dis;
```

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
