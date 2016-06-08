---
layout: post
title: "[Testing] Test Number Divisibility"
comments: true
category: Testing

---

### Question 

[link](http://www.mathsisfun.com/divisibility-rules.html)

> Pay attention on Number 3, 7, 9 and 11. 

### The Divisibility Rules

<table border="0" align="center" style='border:1px solid black'>
							    <tbody><tr align="center">
								    <th width="100" class="bg-color bg-img font-color">Divisible by:</th>
									<th width="300" class="bg-color bg-img font-color">If:</th>
									<th width="300" class="bg-color bg-img font-color">Examples:</th>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">2</td>
									<td class="bg-color bg-img font-color">The last digit is even (0,2,4,6,8)</td>
									<td class="bg-color bg-img font-color">12<b>8</b> is<br>
									12<b>9</b> is not								</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">3</td>
									<td class="bg-color bg-img font-color">The sum of the digits is divisible by 3</td>
									<td class="bg-color bg-img font-color">
									    <p class="font-color">381 (3+8+1=12, and 12÷3 = 4) <b>Yes</b><br>
									</p>
										<p class="font-color">217 (2+1+7=10, and 10÷3 = 3&nbsp;<span class="frac font-color"><sup>1</sup>/<sub>3</sub></span>) <b>No</b></p>									</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">4</td>
									<td class="bg-color bg-img font-color">The last 2 digits are divisible by 4</td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">13<b>12</b> is<b></b> (12÷4=3)<br>
									70<b>19</b> is not </p>								  </td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">5</td>
									<td class="bg-color bg-img font-color">The last digit is 0 or 5</td>
									<td class="bg-color bg-img font-color">17<b>5</b> is<br>
									80<b>9</b> is not								</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">6</td>
									<td class="bg-color bg-img font-color">The number is divisible by both 2 <i>and</i> 3</td>
									<td class="bg-color bg-img font-color">
										114 (it is even, and 1+1+4=6 and 6÷3 = 2) <b>Yes</b><br>
										<br>
										308 (it is even, but 3+0+8=11 and 11÷3 = 3&nbsp;<span class="frac font-color"><sup>2</sup>/<sub>3</sub></span>) <b>No</b>									</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">7</td>
									<td class="bg-color bg-img font-color">If you double the last digit and subtract it from the rest of the number and 
									  the answer  is:
									  <ul class="bg-color bg-img font-color">
                                        <li><b>0</b>, or </li>
									    <li><b>divisible by 7</b></li>
							      </ul>
									  (Note: you can apply this rule to that answer again if you want)</td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">672 (Double 2 is 4, 67-4=63, and 63÷7=9) <b>Yes</b></p>
										<p class="font-color">905 (Double 5 is 10, 90-10=80, and 80÷7=11&nbsp;<span class="frac font-color"><sup>3</sup>/<sub>7</sub></span>) <b>No<br>
									  </b></p>									</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">8</td>
									<td class="bg-color bg-img font-color">The last three digits are divisible by 8</td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">109<b>816</b> (816÷8=102) <b>Yes</b></p>
										<p class="font-color">216<b>302</b> (302÷8=37&nbsp;<span class="frac font-color"><sup>3</sup>/<sub>4</sub></span>) <b>No</b></p>									</td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">9</td>
									<td class="bg-color bg-img font-color">The sum of the digits is divisible by 9<br>
									  <br>
								  (Note: you can apply this rule to that answer again if you want)</td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">1629 (1+6+2+9=18, and again, 1+8=9) <b>Yes</b></p>
										<p class="font-color">2013 (2+0+1+3=6) <b>No</b></p>								  </td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">10</td>
									<td class="bg-color bg-img font-color">The number ends in 0</td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">22<b>0</b> is<br>
											22<b>1</b> is not									  </p>								  </td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center">11</td>
									<td class="bg-color bg-img font-color"><p class="font-color">If you sum every second digit and then subtract all other digits and the answer  is:</p>
								      <ul class="bg-color bg-img font-color">
								        <li><b>0</b>, or </li>
								        <li><b>divisible by 11</b></li>
	                  </ul>							        </td>
									<td class="bg-color bg-img font-color">
										<p class="font-color">1<b>3</b>6<b>4</b> ((3+4) - (1+6) = <b>0</b>) <b>Yes</b></p>
										<p class="font-color">3<b>7</b>2<b>9</b> ((7+9) - (3+2) = <b>11</b>) <b>Yes</b></p>
									  <p class="font-color">2<b>5</b>1<b>7</b>6 ((5+7) - (2+1+6) = <b>3</b>) <b>No</b></p>								  </td>
								</tr>
							    <tr>
								    <td class="large bg-color bg-img font-color" align="center" height="16">12</td>
									<td height="16" class="bg-color bg-img font-color">The number is divisible by both 3 <i><b>and</b></i> 4</td>
									<td height="16" class="bg-color bg-img font-color">
										<p class="font-color">648 <br>
										(<i>By 3?</i> 6+4+8=18 and 18÷3=6 Yes. <br>
										<i>By 4?</i> 48÷4=12 Yes) <b>Yes</b></p>
										<p class="font-color">524 <br>
										(<i>By 3?</i> 5+2+4=11, 11÷3= 3&nbsp;<span class="frac font-color"><sup>2</sup>/<sub>3</sub></span> No. <br>
										Don't need to check by 4.) <b>No</b></p>
</td>
</tr>
</tbody>
</table>
