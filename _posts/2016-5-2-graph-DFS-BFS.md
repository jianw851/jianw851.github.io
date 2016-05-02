---
layout: post
category: [algorithm]
title: Graph Representation
tagline: by Jian
tags: [Graph, DFS, BFS]
---

This is a simple implementation of Undirected Graph


<!--more-->

### Source Code (C++)

```cpp

#include<iostream>
#include<vector>
#include<queue>
using namespace std;
class undirectedGraph {
public:
  class edge {
  public:
    //int vertex;  //in case the vetices are huge and not contiguous
    vector<int> list;
    edge () {}
  };
  int V;
  int E;
  bool useMatrix;
  vector<edge> adjlist;  // representation of adjacent list
  vector<vector<int> > matrix;  // representation of matrix
  undirectedGraph() {  // O(1)
    V = 0;
    E = 0;
  }
  /******************************
  * create am empty graph with V vertices
  *******************************/
  undirectedGraph(int V1, int E1, bool flag) {
    if (flag) {
      useMatrix = true;
      V = V1;
      E = E1;
      matrix = vector<vector<int> >(V, vector<int>(V,0)); //O(V^2)
    } else {
      useMatrix = false;
      V = V1;
      E = E1;
      adjlist = vector<edge>(V); //initial O(V)
    }
  }
  int numberOfV() { // O(1)
    return V;
  }
  int numberOfE() { // O(1)
    return E;
  }
  /******************************
  * find all the adjacent value
  *******************************/
  vector<int> adjacent(int v) {
     vector<int> adjvector;
     if (useMatrix) { // O(V)
       for (int i = 0; i < V; i++) {
         if (matrix[i][v] > 0) adjvector.push_back(i);
       }
     } else {  // O(V) omega(1)
       for (int i = 0; i < adjlist[v].list.size(); i++) {
          adjvector.push_back(adjlist[v].list[i]);
       }
     }
     return adjvector;
  }
  /******************************
  * find the number of vetices
  * adjacent to vertex v
  *******************************/
  int degree(int v) {  // matrix: O(V) adjacent list: O(V) omega(1)
    int degree = 0;
    for (int w : adjacent(v)) degree++;
    return degree;
  }
  /******************************
  * add edges to the graph
  *******************************/
  void addEdge(int v, int w) { // O(1)
    if (useMatrix) {
      // here I use the whole matrix (not half)
      matrix[v][w] = 1;
      matrix[w][v] = 1;
    } else {
      adjlist[v].list.push_back(w);
      adjlist[w].list.push_back(v);
    }
  }
  /******************************
  * count the number of Cycles
  * matrix: O(V^3) adjacent list: O(V^3) omega(V^2)
  *******************************/
  int numberOfCycles() {
    int count = 0;
    for (int v = 0; v < V; v++) {
      for (int w = 0; w < adjacent(v).size(); w++) {
        if (v == w) count++;
      }
    }
    return count / 2; // this is only for undirected graph. For directed graph, no need divide by 2;
  }
  /******************************
  * check if two vertices are adjacent
  *******************************/
  bool isAdjacent(int v, int w) {
    if (v == w) return true;
    if (useMatrix) {  // O(1)
      return matrix[v][w] == 1;
    } else { // O(V) omega(1)
      for (int i = 0; i < adjlist[v].list.size(); i++) {
         if (adjlist[v].list[i] == w)
           return true;
      }
      return false;
    }
  }
  /******************************
  * DFS all the vertices
  * O(V^2) omega(V) limited to edges
  *******************************/
  void DFS(vector<bool> &visited, int v) {
    visited[v] = true;
    for (int i : adjacent(v)) {
      if (!visited[i])
        DFS(visited, i);
      }
  }
  /******************************
  * BFS all the vertices
  * O(V^2) omega(V) limited to edges too
  *******************************/
  void BFS(vector<bool> &visited) {
    queue<int> queue1;
    queue1.push(0);
    while (!queue1.empty()) {
      int v = queue1.front();
      visited[v] = true;
      for (int i : adjacent(v)) {
       if (!visited[i])
         queue1.push(i);
      }
      queue1.pop();
    }
  }
  /******************************
  * count the number of Cycles
  * matrix: O(V^3) adjacent list: O(V^3) omega(V^2)
  *******************************/
  bool isConnected() {
    vector<bool> visited(V, false);
    DFS(visited, 0);
    visited = vector<bool>(V, false);
    BFS(visited);
    for (int i = 0; i < visited.size(); i++) {
      if (!visited[i]) return false;
    }
    return true;
  }
  void print() {
    if (useMatrix) {
      cout << "title ";
      for  (int i = 0; i < V; i++) {
        cout << i << " ";
      }
      cout << endl;
     for (int i = 0; i < V; i++) {
      for (int j = 0; j <= V; j++) {
        if (j == 0)
          cout << i << "     ";
        else
          cout << matrix[i][j-1] << " ";
      }
      cout << endl;
    }
   } else {
     for (int i = 0; i < V; i++) {
       for (int j = 0; j <= adjlist[i].list.size(); j++) {
         if (j == 0)
           cout << "vertex #" << i <<": ";
         else
           cout << adjlist[i].list[j-1] << " ";
       }
       cout << endl;
     }
   }
  }
};
int main() {
  int V, E;
  int v, w; // two adjacent vertices
  cin >> V;
  cin >> E;
  undirectedGraph graphmatrix(V, E, true);
  undirectedGraph graphadjlist(V, E, false);
  for (int i = 0; i < E; i++) {
    cin >> v;
    cin >> w;
    graphmatrix.addEdge(v, w);
    graphadjlist.addEdge(v, w);
  }
  cout << "**************** Matrix representation ***************** " << endl;
  cout << "the number of vertices is: " << graphmatrix.numberOfV() << endl;
  cout << "the number of edges is: " << graphmatrix.numberOfE() << endl;
  cout << "the degree of v = 1 is: " << graphmatrix.degree(1) << endl;
  cout << "the number of cycles is: " << graphmatrix.numberOfCycles() << endl;
  cout << "bellow is the representation of the graph:"<<endl;
  graphmatrix.print();
  cout << "Is connected? " << graphmatrix.isConnected() << endl;
  cout << "*************** adj-list representation **************** " << endl;
  cout << "the number of vertices is: " << graphadjlist.numberOfV() << endl;
  cout << "the number of edges is: " << graphadjlist.numberOfE() << endl;
  cout << "the degree of v = 1 is: " << graphadjlist.degree(1) << endl;
  cout << "the number of cycles is: " << graphadjlist.numberOfCycles() << endl;
  cout << "bellow is the representation of the graph:"<<endl;
  graphadjlist.print();
  cout << "Is connected? " << graphadjlist.isConnected() << endl;
  return 0;
}



```
Bellow is test data

```
7
8
0 1
0 2
0 6
0 5
3 5
3 4
4 5
4 6
```
### Contribution

 [@jianw851](http://jianwang.info/)


---
