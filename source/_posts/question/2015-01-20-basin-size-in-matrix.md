---
layout: post
title: "[Palantir] Largest basin size in matrix"
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=15380670)

A group of farmers has some elevation data, and we’re going to help them understand how rainfall flows over their farmland.

We’ll represent the land as a two-dimensional array of altitudes and use the following model, based on the idea that water flows downhill:

If a cell’s neighboring cells all have higher altitudes, we call this cell a sink; water collects in sinks. Two cells are neighbors if the rows and columns each differ by at most one. Hence an interior cell will have eight neighbors, a cell on the edge will have five neighbors, and a cell in a corner will have three neighbors.

Otherwise, water will flow to the neighboring cell with the lowest altitude. If a cell is not a sink, you may assume it has a unique lowest neighbor and that this neighbor will be lower than the cell.
Cells that drain into the same sink – directly or indirectly – are said to be part of the same basin.
 
Your challenge is to partition the map into basins. In particular, given a map of elevations, your code should partition the map into basins and output the sizes of the basins, in descending order.
 
Assume the elevation maps are square. Input will begin with a line with one integer, S, the height (and width) of the map. The next S lines will each contain a row of the map, each with S integers – the elevations of the S cells in the row.  Some farmers have small land plots such as the examples below, while some have larger plots.  However, in no case will the total size of the farmland exceed 1000x1000.
 
Note: The input uses unix line endings (\n). If you try to view the sample inputs on a windows machine with a program that does not convert line endings (like Notepad), you will see the input appear all on a single line.
 
Your code should output a space-separated list of the basin sizes, in descending order. (Trailing spaces are ignored.)
 
While correctness and performance are the most important parts of this problem, a human will be reading your solution, so please make an effort to submit clean, readable code. In particular, do not write code as if you were solving a problem for a competition.
 
A few examples are below.
 
Input:

           3
           1 5 2
           2 4 7
           3 6 9

Output:

                7 2
 
The basins, labeled with A’s and B’s, are:

           A A B
           A A B
           A A A

Input:

           1
           10

Output:

           1
 
There is only one basin in this case.

Input:

           5
           1 0 2 5 8
           2 3 4 7 9
           3 5 7 9 9
           1 2 5 5 3
           3 3 5 1 0

Output:

           10 8 7

The basins, labeled with A’s, B’s, and C’s, are:

           A A A A A
           A A A A A
           B B B C C
           B B C C C
           B B C C C

Input:

           4
           0 3 2 3
           3 2 1 4
           3 4 3 3
           5 5 2 0

Output:

           6 5 5

The basins, labeled with A’s, B’s, and C’s, are:

           A A B B
           A A B B
           A B C C
           A C C C

### Solution

I did not find a 'best' solution online, but there's a good enough explanation available [here](http://stackoverflow.com/questions/24336686/find-the-largest-basin-size-in-a-given-matrix): 

1. First store index according to their heights.

1. Then iterate from smallest height to largest height.

1. If current index is not visited, make it Basin surface (where water can collect), and make all higher neighbours as Non-Basin surface.

1. Repeat step 3 till all indexes are visited.

1. DFS find each basin

### Code

I post my solution written in 2013. 

    public class MeSolution2013 {

        public static void main(String args[]) {

            String inputFile;
            int testCaseNumber = 1;

            while (true) {
                inputFile = "input" + testCaseNumber + ".txt";
                BufferedReader in;
                try {
                    URI uri = MeSolution2013.class.getResource(inputFile).toURI();
                    in = new BufferedReader(new FileReader(new File(uri)));
                } catch (Exception e) {
                    // there is not more test cases
                    break;
                }

                Scanner sc = new Scanner(in);
                int length = sc.nextInt();
                int[][] elevation = new int[length][length];
                for (int i = 0; i < length; i++) {
                    for (int j = 0; j < length; j++) {
                        elevation[i][j] = sc.nextInt();
                    }
                }

                List<Pair> sinkList = new ArrayList<Pair>();

                // first find out all sink nodes
                for (int i = 0; i < length; i++) {
                    for (int j = 0; j < length; j++) {
                        if (elevation[i][j] < lowestNeighbor(i, j, elevation)) {
                            // (i,j) is a sink point
                            sinkList.add(new Pair(i, j));
                        }
                    }
                }

                // then for each sink node, return the count
                int[] basinSize = new int[sinkList.size()];
                for (int i = 0; i < sinkList.size(); i++) {
                    basinSize[i] = count(sinkList.get(i).X, sinkList.get(i).Y,
                            elevation);
                }
                Arrays.sort(basinSize);

                for (int i = sinkList.size() - 1; i >= 0; i--) {
                    System.out.print(basinSize[i]);
                    if (i != 0)
                        System.out.print(" ");
                }
                System.out.println();
                testCaseNumber++;
            }
        }

        static int count(int x, int y, int[][] ele) {

            int num = 1;

            // if the neighbour is higher than current, add count to current count
            // if all neighbours are lower than current, return 1

            // diagonal neighbors
            if (withinBound(x - 1, y, ele) && rainFlowFrom(x, y, x - 1, y, ele)) { // upper
                                                                                    // elment
                num += count(x - 1, y, ele);
            }
            if (withinBound(x + 1, y, ele) && rainFlowFrom(x, y, x + 1, y, ele)) { // lower
                                                                                    // element
                num += count(x + 1, y, ele);
            }
            if (withinBound(x, y - 1, ele) && rainFlowFrom(x, y, x, y - 1, ele)) { // left
                                                                                    // hand
                                                                                    // side
                num += count(x, y - 1, ele);
            }
            if (withinBound(x, y + 1, ele) && rainFlowFrom(x, y, x, y + 1, ele)) { // right
                                                                                    // hand
                                                                                    // side
                num += count(x, y + 1, ele);
            }

            // diagonal neighbors
            if (withinBound(x - 1, y - 1, ele)
                    && rainFlowFrom(x, y, x - 1, y - 1, ele)) { // upper elment
                num += count(x - 1, y - 1, ele);
            }
            if (withinBound(x + 1, y + 1, ele)
                    && rainFlowFrom(x, y, x + 1, y + 1, ele)) { // lower element
                num += count(x + 1, y + 1, ele);
            }
            if (withinBound(x + 1, y - 1, ele)
                    && rainFlowFrom(x, y, x + 1, y - 1, ele)) { // left hand side
                num += count(x + 1, y - 1, ele);
            }
            if (withinBound(x - 1, y + 1, ele)
                    && rainFlowFrom(x, y, x - 1, y + 1, ele)) { // right hand side
                num += count(x - 1, y + 1, ele);
            }

            return num;
        }

        static Boolean withinBound(int x, int y, int[][] ele) {
            int bound = ele.length;
            return (x >= 0 && x < bound && y >= 0 && y < bound);
        }

        static Boolean rainFlowFrom(int a, int b, int c, int d, int[][] ele) {
            // rain in (c,d) flows into (a,b).
            if (ele[a][b] >= ele[c][d])
                // if (a,b) is higher than (c,d), impossible to flow this way
                return false;

            int lowest = lowestNeighbor(c, d, ele);

            return (ele[a][b] == lowest);
            // the question states "you may assume it has a unique lowest neighbor"
            // so if flow to (a,b), then that is the unique lowest height.
        }

        static int lowestNeighbor(int a, int b, int[][] ele) {
            int height = 9999999;

            // adjacent neighbor
            if (withinBound(a - 1, b, ele) && ele[a - 1][b] < height) {
                height = ele[a - 1][b];
            }
            if (withinBound(a + 1, b, ele) && ele[a + 1][b] < height) {
                height = ele[a + 1][b];
            }
            if (withinBound(a, b - 1, ele) && ele[a][b - 1] < height) {
                height = ele[a][b - 1];
            }
            if (withinBound(a, b + 1, ele) && ele[a][b + 1] < height) {
                height = ele[a][b + 1];
            }

            // diagonal neighbor
            if (withinBound(a - 1, b - 1, ele) && ele[a - 1][b - 1] < height) {
                height = ele[a - 1][b - 1];
            }
            if (withinBound(a + 1, b - 1, ele) && ele[a + 1][b - 1] < height) {
                height = ele[a + 1][b - 1];
            }
            if (withinBound(a - 1, b + 1, ele) && ele[a - 1][b + 1] < height) {
                height = ele[a - 1][b + 1];
            }
            if (withinBound(a + 1, b + 1, ele) && ele[a + 1][b + 1] < height) {
                height = ele[a + 1][b + 1];
            }
            return height;
        }
    }

    class Pair {

        public int X;
        public int Y;

        public Pair(int _x, int _y) {
            X = _x;
            Y = _y;
        }
    }
