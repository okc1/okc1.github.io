---
layout: post
title: "[UVa] Wooden Sticks "
comments: true
category: Question

---

### Question 

[link](https://icpcarchive.ecs.baylor.edu/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=323)

<body>There is a pile of <i>n </i>wooden sticks. The length and weight of
each stick are known in advance. The sticks are
to be processed by a woodworking machine in one by one fashion. It
needs some time, called setup time, for
the machine to prepare processing a stick. The setup times are
associated with cleaning operations and
changing tools and shapes in the machine. The setup times of the
woodworking machine are given as follows:
<ul>
<li>The setup time for the first wooden
stick is 1 minute.</li>
<li>
Right after processing a stick of length <i>l </i>and weight <i>w
</i>, the machine will need no setup time for a stick
of length <i>l</i>' and weight <i>w</i>' if <i>l </i>&lt;=<i>l</i>'
and <i>w </i>&lt;=<i>w</i>' . </li>
</ul>
Otherwise, it will need 1 minute for setup.<br>
You are to find the minimum setup time to process a given pile of <i>n
</i>wooden sticks. For example, if you have
five sticks whose pairs of length and weight are (4,9), (5,2), (2,1), (3,5),
and (1,4) then the minimum setup
time should be 2 minutes since there is a sequence of pairs (1,4),
(3,5), (4,9), (2,1), (5,2).
<h2><font size="4" color="#ff0000"><a name="SECTION0001001000000000000000">Input</a> <br>
</font></h2>
The input consists of <i>T</i> test cases. The number of test cases (<i>T</i>) is given in the first line of the input file. Each
test case consists of two lines: The first line has an integer <i>n</i>,
1&lt;=<i>n&lt;=</i>5000, that represents the number of
wooden sticks in the test case, and the second line contains 2<i>n </i>positive
integers <i>l<sub>1</sub></i>, <i>w<sub>1</sub></i>, <i>l<sub>2</sub></i>,
<i>w<sub>2</sub></i>, ..., <i>l<sub>n</sub></i>, <i>w<sub>n</sub></i>,
each of magnitude at most 10000, where <i>l<sub>i</sub> </i>and <i>w<sub>i</sub>
</i>are the length and weight of the <i>i </i>th wooden stick,
respectively. The 2<i>n </i>integers are delimited by one or
more spaces.

<h2><font size="4" color="#ff0000"><a name="SECTION0001002000000000000000">Output</a>&nbsp;</font>
</h2>
The output should contain the minimum setup time in minutes, one per
line.
<h2><font size="4" color="#ff0000"><a name="SECTION0001003000000000000000">Sample Input</a> <br>
</font></h2>

<pre>3
5
4 9 5 2 2 1 3 5 1 4
3
2 2 1 1 2 2
3
1 3 2 2 3 1
</pre>

<h2><font size="4" color="#ff0000"><a name="SECTION000
1004000000000000000">Sample Output</a>&nbsp;</font>
</h2>

<pre>2
1
3
</pre>

</body>

### Analysis

This question is a little similar to [[CC150v5] 9.10 Stack Up the Boxes]({% post_url /cc150v5/2014-09-17-stack-up-boxes %}), yet different. 

### Solution

Solution quoted from [脚本百事通](http://www.csdn123.com/html/blogs/20130823/58042.htm): 

>按长度从小到大排序, 若长度相同, 则按重量从小到大排序(先按重量再按长度也行)

>然后, 我们针对当前木棍, 与剩下的木棍比较, 满足 w1 <= w2 && l1 <= l2 的, 就更新一下当前棍, 并标记~

>当所有木棍都被编组后 输出到底设置了几次~

[ref1](http://www.android100.org/html/201502/03/109926.html), [ref2](http://blog.csdn.net/keshuai19940722/article/details/10735689)

### Code

The following Java code is written by me

    public int count(Pair[] points) {
        Arrays.sort(points, new PointComparator());
        // now the array is sorted with Point.x
        int total = 0;
        int p = 0;
        int len = points.length;

        while (p < len) {
            // find the next non-null point
            while (p < len && points[p] == null) {
                p++;
            }
            if (p == len) {
                break;
            }
            // use points[p] as the first elements in the queue
            Pair temp = copy(points[p]);
            points[p] = null;
            total++;

            // then mark all elements that follow points[p]
            for (int k = p + 1; k < len; k++) {
                if (points[k] == null || points[k].y < temp.y) {
                    continue;
                }
                temp = copy(points[k]);
                points[k] = null;
            }
            p++;
        }
        return total;
    }

    Pair copy(Pair p) {
        Pair newP = new Pair(p.x, p.y);
        return newP;
    }

    class PointComparator implements Comparator<Pair> {

        @Override
        public int compare(Pair p1, Pair p2) {
            return p1.x - p2.x;
        }
    }
