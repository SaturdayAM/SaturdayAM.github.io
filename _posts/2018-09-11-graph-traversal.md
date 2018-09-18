---
layout: post
title:  "Graph Traversal"
categories: jekyll update
---


## Graph Traversal ##
As our last blog post introduced some basic information on graphs,
we now look at show graphs are traversed and the runtime of 
searching for elements.

Graph searching tends to fall into two methods, **depth-first search**
and **breadth-first search**. Their names more or less tell you
how they are implemented.

In **depth-first search**, the algorithm begins with some arbitrary node,
a, and then iterate through each of its branches completely before going 
to another branch.For a neighbor, b, of a, we go through all of b's neighbors 
before going back "up" a level to a and searching its a's neighbors. This is
a preferred method if we wish to visit every node in the graph. 

{% highlight javascript %}
  function DFS(node){
    if(node == null) return; //base case
    visit(node); 
    node.visited = true; //Keep track of visited nodes 
                         //to avoid infinite loops

    //Search through the full depth of each branch
    //from the selected node
    for(let i = 0; i < node.adjacent.length; i++){
      let temp = node.adjacent[i];
      if(!temp.visited){
        DFS(temp);
      }
    }
  }
{% endhighlight %}


In **breadth-first search**, we start with some arbitrary node,
and explore each of that node's neighbors before traversing 
the neighbor's children. Breadth-first search is implemented
using a queue, and is preferred for finding the shortest
path between two nodes. 

{% highlight javascript %}
  function BFS(node){ //Iterative approach, can be any node
    let queue = []; //Queue used to keep track of visited nodes
    node.visited = true;
    queue.push(node); 

    while(queue.length > 0){ 
      let temp = queue.shift(); //temp is the front of queue
      visit(temp);
      for(let i = 0; i < temp.adjacent.length; i++){ //iterate through all neighbors of
                                                     //the first element on queue
        let neighbor = temp.adjacent[i];
        if(!neighbor.visited){
          neighbor.visited = true;
          queue.push(neighbor); //add neighbors to queue to iteratively          
        }
      }
    }
  }
{% endhighlight %}


The time complexity of both **breadth-first search** and **depth-first search**
will be O(V+E), where V is the number of vertices (nodes) and E is the number of 
edges. This, however, will actually depend on the method used to implement the graph.
For an adjacency matrix, since every vertix V's relationship to every other vertex is stored,
it is O(V^2). For an adjacency list, which represents each vertex and its existing edges,
it remains O(V+E). Going deeper into this idea of O(V+E), we can see that either V or E
will dominate the runtime depending on the nature of the graph.

If a graph has many edges but very few vertices, it will become dominated by the value of E
and can be considered O(E). For isnstance, consider a maximally connexted graph of
100 vertices and 4950 edges (v*(v-1)/2). In this case, the value of E dominates the runtime.
Vice versa, if a graph is sparsley connected, the value of V can dominate the runtime. 
