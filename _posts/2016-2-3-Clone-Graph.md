---
layout: post
category: [algorithm]
title: Clone Graph
tagline: by Jian
tags: [Graph, DFS]
---

Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

How we serialize an undirected graph:

Nodes are labeled uniquely.

We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
As an example, consider the serialized graph {0,1,2#1,2#2,2}.

The graph has a total of three nodes, and therefore contains three parts as separated by #.

First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
Second node is labeled as 1. Connect node 1 to node 2.
Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.


return a deep copied graph.

<!--more-->

	class Solution {
public:
    UndirectedGraphNode *cloneGraph(UndirectedGraphNode *node) {
      if (node == NULL) return NULL;
      unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> map1;
      vector<UndirectedGraphNode*> queue;
      queue.push_back(node);
      UndirectedGraphNode *head = new UndirectedGraphNode(node->label);
      map1[node] = head;
      int curr = 0;
      while (curr < queue.size()) {
        UndirectedGraphNode * curr_node = queue[curr];
        int size = curr_node->neighbors.size();
        for (int i = 0; i < size; i++) {
          UndirectedGraphNode * curr_neigh = curr_node->neighbors[i];
          if (map1.find(curr_neigh) == map1.end()) {
            UndirectedGraphNode * curr_copy = new UndirectedGraphNode(curr_neigh->label);
            map1[curr_node]->neighbors.push_back(curr_copy);
            map1[curr_neigh] = curr_copy;
            queue.push_back(curr_neigh);
          } else {
            map1[curr_node]->neighbors.push_back(map1[curr_neigh]);
          }
        }
        curr++;
      }
      return head;
    }
	};


 Contribution

 [@jianw851](http://jianwang.info/)


---
