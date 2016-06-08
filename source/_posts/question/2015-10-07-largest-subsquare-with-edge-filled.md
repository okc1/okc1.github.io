---
layout: post
title: "[Question] Largest Sub-square with Edges filled "
comments: true
category: Question
tags: [  ]
---

### Question

[link](www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/index.html)

> Given a matrix where every element is either ‘O’ or ‘X’, find the largest sub-square surrounded by ‘X’. (meaning that the 4 edges are filled with 'X')

> Example Input:

     {'X', 'O', 'X', 'X', 'X'},
     {'X', 'X', 'X', 'X', 'X'},
     {'X', 'X', 'O', 'X', 'O'},
     {'X', 'X', 'X', 'X', 'X'},
     {'X', 'X', 'X', 'O', 'O'},


> Output: 3. The square submatrix starting at (1, 1) is the largest sub-squre. 

> Example Input:

     {'X', 'O', 'X', 'X', 'X', 'X'},
     {'X', 'O', 'X', 'X', 'O', 'X'},
     {'X', 'X', 'X', 'O', 'O', 'X'},
     {'X', 'X', 'X', 'X', 'X', 'X'},
     {'X', 'X', 'X', 'O', 'X', 'O'},

> Output: 4. The square submatrix starting at (0, 2) is the largest

### Solution

Read a very similar question - __[Question] Maximum Square Sub-matrix With All 1s__

Typical DP question. Now the solution is to build 2 arrays to cache info. One horizontally and one, vertical. 

> create two auxiliary arrays hor[N][N] and ver[N][N]. 

> hor[i][j] is the number of horizontal continuous ‘X’ characters till mat[i][j] in mat[][]. 

> ver[i][j] is the number of vertical continuous ‘X’ characters till mat[i][j] in mat[][]. 

    mat[6][6] =  X  O  X  X  X  X
                 X  O  X  X  O  X
                 X  X  X  O  O  X
                 O  X  X  X  X  X
                 X  X  X  O  X  O
                 O  O  X  O  O  O

    hor[6][6] = 1  0  1  2  3  4
                1  0  1  2  0  1
                1  2  3  0  0  1
                0  1  2  3  4  5
                1  2  3  0  1  0
                0  0  1  0  0  0

    ver[6][6] = 1  0  1  1  1  1
                2  0  2  2  0  2
                3  1  3  0  0  3
                0  2  4  1  1  4
                1  3  5  0  2  0
                0  0  6  0  0  0

After we got these, start from the bottom-right corner row by row up... For every mat[i][j], we compare hor[i][j] with ver[i][j] and pick the smaller one. 

All we need to do next, is to check the other 2 edges. This solution is O(n^3).

### Code 

C++ code provided by [G4G](www.geeksforgeeks.org/given-matrix-o-x-find-largest-subsquare-surrounded-x/index.html):

    int findSubSquare(int mat[][N])
    {
        int max = 1; // Initialize result

        // Initialize the left-top value in hor[][] and ver[][]
        int hor[N][N], ver[N][N];
        hor[0][0] = ver[0][0] = (mat[0][0] == 'X');

        // Fill values in hor[][] and ver[][]
        for (int i=0; i<N; i++)
        {
            for (int j=0; j<N; j++)
            {
                if (mat[i][j] == 'O')
                    ver[i][j] = hor[i][j] = 0;
                else
                {
                    hor[i][j] = (j==0)? 1: hor[i][j-1] + 1;
                    ver[i][j] = (i==0)? 1: ver[i-1][j] + 1;
                }
            }
        }

        // Start from the rightmost-bottommost corner element and find
        // the largest ssubsquare with the help of hor[][] and ver[][]
        for (int i = N-1; i>=1; i--)
        {
            for (int j = N-1; j>=1; j--)
            {
                // Find smaller of values in hor[][] and ver[][]
                // A Square can only be made by taking smaller
                // value
                int small = getMin(hor[i][j], ver[i][j]);

                // At this point, we are sure that there is a right
                // vertical line and bottom horizontal line of length
                // at least 'small'.

                // We found a bigger square if following conditions
                // are met:
                // 1)If side of square is greater than max.
                // 2)There is a left vertical line of length >= 'small'
                // 3)There is a top horizontal line of length >= 'small'
                while (small > max)
                {
                    if (ver[i][j-small+1] >= small &&
                        hor[i-small+1][j] >= small)
                    {
                        max = small;
                    }
                    small--;
                }
            }
        }
        return max;
    }
