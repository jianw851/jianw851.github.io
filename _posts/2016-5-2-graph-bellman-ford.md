---
layout: post
category: [algorithm]
title: Bellman-Ford algorithm
tagline: by Jian
tags: [Graph, Bellman-Ford]
---

This is a simple implementation of Bellman-Ford


<!--more-->

### Source Code (C++)

```cpp
#include<iostream>
#include<vector>
#include<queue>
#include <limits>
using namespace std;
class uwGraph {
public:
  int V;
  int E;
  bool useMatrix;
  vector<vector<double> > matrix;  // representation of matrix
  uwGraph() {  // O(1)
    V = 0;
    E = 0;
  }
  /******************************
  * create am empty graph with V vertices
  *******************************/
  uwGraph(int V1, int E1) {
      useMatrix = true;
      V = V1;
      E = E1;
      matrix = vector<vector<double> >(V, vector<double>(V, std::numeric_limits<double>::max())); //O(V^2)
      for (int i = 0; i < V1; i++) {
        matrix[i][i] = 0.0;
      }
  }
  /******************************
  * find all the adjacent value
  *******************************/
  vector<int> adjacent(int v) {
     vector<int> adjvector;
      // O(V)
       for (int i = 0; i < V; i++) {
         if (matrix[i][v] > 0) adjvector.push_back(i);
       }
     return adjvector;
  }

  /******************************
  * add edges to the graph
  *******************************/
  void addEdge(int v, int w, double weight) { // O(1)
      // here I use the whole matrix (not half)
      matrix[v][w] = weight;
      matrix[w][v] = weight;
  }

  /******************************
  * check if two vertices are adjacent
  *******************************/
  bool isAdjacent(int v, int w) {
    if (v == w) return true;
   // O(1)
      return matrix[v][w] != std::numeric_limits<double>::max();
  }

  void print() {
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
  }

  void bellmanford(vector<double> &D, vector<int> &P) { // O(V^3) omega(V^2)
    for (int i = 1; i < V; i++) {
      for (int u = 0; u < V; u++) {
        for (int v = 0; v < V; v++) {
          if (matrix[u][v] != std::numeric_limits<double>::max() &&
              D[u] != std::numeric_limits<double>::max() &&
              D[u] + matrix[u][v] < D[v]) {
                D[v] = D[u] + matrix[u][v];
                P[v] = u;
           }
      }
    }
  }
 }
};
int main() {
  int V, E, v, w;
  double weight;
  cin >> V >> E;
  uwGraph graphmatrix(V, E);
  for (int i = 0; i < E; i++) {
    cin >> v >> w >> weight;
    graphmatrix.addEdge(v, w, weight);
  }
  //cout << "**************** Matrix representation ***************** " << endl;
  //cout << "bellow is the representation of the graph:"<<endl;
  //graphmatrix.print();
  vector<double> D(V, std::numeric_limits<double>::max());
  D[0] = 0.0;
  vector<int> P(V, 0);
  graphmatrix.bellmanford(D, P);
  for (int i = 0; i < D.size(); i++) {
    cout << D[i] << "  ";
  }
  cout << endl;
  for (int i = 0; i < P.size(); i++) {
    cout << P[i] << "  ";
  }
  return 0;
}

```
Bellow is test data

```
6
8
0 1 2.5
0 3 0.5
1 4 1.2
1 2 0.5
2 3 1.5
2 4 1.0
4 5 1.4
3 5 4.4
```
### Contribution

 [@jianw851](http://jianwang.info/)


---
