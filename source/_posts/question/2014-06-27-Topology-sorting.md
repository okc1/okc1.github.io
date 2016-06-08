---
layout: post
title: "[Question] Topology Sort "
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://en.wikipedia.org/wiki/Topological_sorting)

> Topological ordering of a directed graph is a linear ordering of its vertices such that __for every directed edge uv from vertex u to vertex v, u comes before v in the ordering__. 

> A topological ordering is possible if and only if the graph has no directed cycles, that is, if it is a __directed acyclic graph (DAG)__. 

### Analysis

Canonical application of toposort is to schedule tasks with dependency (project management etc.) It's also used for computing formulas, logic synthesis, order of compilation ('make' command) and data serialization. 

{% img middle /assets/images/topology_sort_example.png %}

### Solution

The usual algorithms have __linear run-time__, i.e. O(V + E). 

> First step is to find a list of "start nodes" which have no incoming edges. Then insert them into a set S and delete it. At least one such node must exist in an __directed acyclic graph__. From a university [lecture](https://courses.cs.washington.edu/courses/cse326/03wi/lectures/RaoLect20.pdf). 

From Wiki: 

    L ← Empty list that will contain the sorted elements
    S ← Set of all nodes with no incoming edges
    while S is non-empty do
        remove a node n from S
        add n to tail of L
        for each node m with an edge e from n to m do
            remove edge e from the graph
            if m has no other incoming edges then
                insert m into S
    if graph has edges then
        return error (graph has at least one cycle)
    else 
        return L (a topologically sorted order)

If the graph is a DAG, __a solution will be contained in the list L__ (the solution is not necessarily unique). Otherwise, the graph must have at least one cycle and therefore __a topological sorting is impossible__.

### Code

The solution comes from [here](http://codereview.stackexchange.com/questions/44689/topological-sort-in-java). 

{% img middle /assets/images/topology_sort.png 250 250 %}

    public class Graph {
        private int vertices;
        private Set<Node> nodes = new HashSet<Node>();

        public Graph(int vertices) {
            this.vertices = vertices;
        }

        public void addVertex(Node node) {
            this.nodes.add(node);
        }

        public Set<Node> topologicalSort() {
            Queue<Node> q = new LinkedList<Node>();
            Set<Node> topoSort = new LinkedHashSet<Node>();
            int vertexProcessesCtr = 0;
            for (Node m : this.nodes) {
                vertexProcessesCtr = addToQueue(m, topoSort, vertexProcessesCtr, q);
            }
            while (!q.isEmpty()) {
                Node m = q.poll();
                for (Node child : m.getAdjacenctNode()) {
                    int indeq = child.getInDegree() - 1;
                    child.setInDegree(indeq);
                    vertexProcessesCtr = addToQueue(child, topoSort,
                            vertexProcessesCtr, q);
                }
            }
            if (vertexProcessesCtr > this.vertices) {
                System.out.println();
            }
            return topoSort;
        }

        private int addToQueue(Node node, Set<Node> topoSort, int vertexProcess,
                Queue<Node> q) {
            if (node.getInDegree() == 0) {
                q.add(node);
                topoSort.add(node);
                return vertexProcess + 1;
            }
            return vertexProcess;
        }

        public static void main(String[] args) {
            Graph g = new Graph(8);

            Node TEN = new Node("10");
            Node ELEVEN = new Node("11");
            Node TWO = new Node("2");
            Node THREE = new Node("3");
            Node FIVE = new Node("5");
            Node SEVEN = new Node("7");
            Node EIGHT = new Node("8");
            Node NINE = new Node("9");

            SEVEN.AdjacenctNode.add(ELEVEN);
            ELEVEN.inDegree++;
            SEVEN.AdjacenctNode.add(EIGHT);
            EIGHT.inDegree++;
            FIVE.AdjacenctNode.add(ELEVEN);
            ELEVEN.inDegree++;
            THREE.AdjacenctNode.add(EIGHT);
            EIGHT.inDegree++;
            THREE.AdjacenctNode.add(TEN);
            TEN.inDegree++;
            ELEVEN.AdjacenctNode.add(TEN);
            TEN.inDegree++;
            ELEVEN.AdjacenctNode.add(TWO);
            TWO.inDegree++;
            ELEVEN.AdjacenctNode.add(NINE);
            NINE.inDegree++;
            EIGHT.AdjacenctNode.add(NINE);
            NINE.inDegree++;

            g.nodes.add(TWO);
            g.nodes.add(THREE);
            g.nodes.add(FIVE);
            g.nodes.add(SEVEN);
            g.nodes.add(EIGHT);
            g.nodes.add(NINE);

            System.out.println("Now calling the topologial sorts");
            Set<Node> result = g.topologicalSort();
            for (Node node : result) {
                System.out.println(node.data + " ");
            }
        }
    }

    class Node {
        public String data;
        public int dist;
        public int inDegree;
        LinkedList<Node> AdjacenctNode = new LinkedList<Node>();

        public void addAdjNode(final Node Child) {
            AdjacenctNode.add(Child);
            Child.inDegree++;
        }

        public Node(String data) {
            super();
            this.data = data;
        }

        public int getInDegree() {
            return inDegree;
        }

        public void setInDegree(int inDegree) {
            this.inDegree = inDegree;
        }

        public LinkedList<Node> getAdjacenctNode() {
            return AdjacenctNode;
        }
    }
