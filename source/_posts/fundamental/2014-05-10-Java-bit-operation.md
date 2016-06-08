---
layout: post
title: "[Fundamental] Java Bit Operation "
comments: true
category: Fundamental

---

### Bit operators

<table border="2">
  <tr>
    <th>operator</th>
    <th>what is means</th>
  </tr>
  <tr>
    <td>~</td>
    <td>invert every bit</td>
  </tr>
  <tr>
    <td>&lt;&lt;</td>
    <td>shift left (same as *2)</td>
  </tr>
  <tr>
    <td>&gt;&gt;</td>
    <td>signed shift right</td>
  </tr>
  <tr>
    <td>&gt;&gt;&gt;</td>
    <td>unsigned shift right</td>
  </tr>
  <tr>
    <td>^</td>
    <td>XOR</td>
  </tr>
  <tr>
    <td>|</td>
    <td>OR</td>
  </tr>
</table>
<br />

Note the unsigned right shift operator ">>>" shifts a __zero into the leftmost position__, while the leftmost position after ">>" __depends on sign extension__.
