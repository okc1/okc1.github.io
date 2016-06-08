---
layout: post
title: "[Fundamental] Recap on Java HashMap "
comments: true
category: Fundamental

---

#### The HashMap

<blockquote cite="http://www.sparknotes.com/cs/searching/hashtables/section1.html">
<div>
<a href="http://www.sparknotes.com/cs/searching/hashtables/section1.html">link</a>
</div>
<p>
A hash table is made up of two parts: an array (the actual table where the data to be searched is stored) and a mapping function, known as a hash function. 
</p>
<p>
The hash function is a mapping from the input space to the integer space that defines the indices of the array. In other words, the hash function provides a way for assigning numbers to the input data such that the data can then be stored at the array index corresponding to the assigned number.
</p>
</blockquote>

For example, if I want to store <"Durant">, I pass "Durant" into the hash function, and get (let's say) number 3. So in the Hash Table, it will store table(3 -> "Durant"). 

In this way, the __searching of HashMap can almost achieve  O(1) time in best case__ (like array access). 

However,

<blockquote cite="http://stackoverflow.com/a/9214421">
<div>
<a href="http://stackoverflow.com/a/9214421">link</a>
</div>
<p>
For average case, It really is (as the wikipedia page says) O(1+n/k) where K is the hash table size. If K is large enough, then the result is effectively O(1). But suppose K is 10 and N is 100. In that case each bucket will have on average 10 entries, so the search time is definitely not O(1); it is a linear search through up to 10 entries.
</p>
</blockquote>

In practise, we will just assume search in HashMap always O(1). 

Below is a great conclusion.

<blockquote cite="http://stackoverflow.com/a/9214594">
<div>
<a href="http://stackoverflow.com/a/9214594">link</a>
</div>
<p><a href="http://en.wikipedia.org/wiki/Hash_table">Hash tables</a> are <code>O(1)</code> <strong>average and <a href="http://en.wikipedia.org/wiki/Amortized_analysis">amortized</a></strong> case complexity, however is suffers from <code>O(n)</code> <strong>worst case</strong> time complexity. [And I think this is where your confusion is]</p>

<p>Hash tables suffer from <code>O(n)</code> worst time complexity due to two reasons:</p>

<ol>
<li>If too many elements were hashed into the same key: looking inside this key may take <code>O(n)</code> time.</li>
<li>Once a hash table has passed its <a href="http://en.wikipedia.org/wiki/Load_balancing_%28computing%29">load balance</a> - it has to rehash [create a new bigger table, and re-insert each element to the table]. </li>
</ol>

<p>However, it is said to be <code>O(1)</code> average and amortized case because:</p>

<ol>
<li>It is very rare that many items will be hashed to the same key [if you chose a good hash function and you don't have too big load balance.</li>
<li>The rehash operation, which is <code>O(n)</code>, can at most happen after <code>n/2</code> ops, which are all assumed <code>O(1)</code>: Thus when you sum the average time per op, you get : <code>(n*O(1) + O(n)) / n) = O(1)</code></li>
</ol>
</blockquote>