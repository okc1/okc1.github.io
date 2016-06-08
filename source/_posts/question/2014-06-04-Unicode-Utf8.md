---
layout: post
title: "[Question] ASCII, Utf-8, Utf-16 and Unicode"
comments: true
category: Question

---


## First Word

__ASCII, UTF-? are encoding schemes. Unicode is character set__. 

Or in other words, UTF-8 is an encoding used to translate binary data into numbers. Unicode is a character set used to translate numbers into characters.

## ASCII 

__[ASCII](http://en.wikipedia.org/wiki/ASCII)__ is a character-encoding scheme based on the English alphabet. It encodes 128 characters into 7-bit integers.

ASCII was the most commonly used character encoding on the World Wide Web until December 2007, when it was surpassed by UTF-8, which includes ASCII as a subset. 

## UTF-8

UCS Transformation Format—8-bit

__[UTF-8](http://en.wikipedia.org/wiki/Utf_8)__ is a variable-width encoding that can represent every character in the Unicode character set. It uses 1 byte for ASCII characters, and up to 4 bytes for others.

__UTF-8 is the dominant character encoding for the World Wide Web__, accounting for more than half of all Web pages. 

Utf-8 is good because:

1. backward compatibility with ASCII 

2. avoid the complications of endianness and byte order marks in UTF-16 and UTF-32

UTF-8 has become the dominant character encoding for the World Wide Web, accounting for more than half of all Web pages

## UTF-16 and UTF-32

__UTF-16 is used for text in the OS API in Microsoft Windows 2000/XP/2003/Vista/7/8/CE__. The word "Unicode" means something else according to [this person](http://stackoverflow.com/a/3951826):

> Windows uses UTF-16LE encoding internally as the memory storage format for Unicode strings, it considers this to be the natural encoding of Unicode text. In the Windows world, there are ANSI strings and there are Unicode strings (stored internally as UTF-16LE).

> This was all devised in the early days of Unicode, before UTF-8 was invented. This is why Windows's support for UTF-8 is all-round poor. 

#### UTF-8: "size optimize": 

Best suited for Latin character based data (or ASCII), it takes only 1 byte. 

#### UTF-16: "balance" 

It takes minimum 2 bytes per character which is enough for existing set of the mainstream languages with having fixed size on it to ease character handling, but size is still variable and can grow up to 4 bytes per character. 

#### UTF-32: "performance"

Allows using of simple algorithms as result of fixed size characters (4 bytes) but with memory disadvantage

## Unicode 

[Unicode](http://en.wikipedia.org/wiki/Unicode) is a computing industry standard for the consistent encoding. It expresses most of world's writing systems with more than 110,000 characters covering 100 scripts and symbols. 

Unicode can be implemented by Utf-8, Utf-16 and now-obsolete Ucs-2. When unicode is encoded with UTF-8, its code value is same as ASCII. 

## Table of the scheme

<table class="wikitable">
<tbody><tr>
<th class="bg-color bg-img font-color">Bits of<br>
code point</th>
<th class="bg-color bg-img font-color">First<br>
code point</th>
<th class="bg-color bg-img font-color">Last<br>
code point</th>
<th class="bg-color bg-img font-color">Bytes in<br>
sequence</th>
<th class="bg-color bg-img font-color">Byte 1</th>
<th class="bg-color bg-img font-color">Byte 2</th>
<th class="bg-color bg-img font-color">Byte 3</th>
<th class="bg-color bg-img font-color">Byte 4</th>
<th class="bg-color bg-img font-color">Byte 5</th>
<th class="bg-color bg-img font-color">Byte 6</th>
</tr>
<tr>
<th class="bg-color bg-img font-color">&nbsp;&nbsp;7</th>
<td class="bg-color bg-img font-color">U+0000</td>
<td class="bg-color bg-img font-color">U+007F</td>
<td style="text-align: center;" class="bg-color bg-img font-color">1</td>
<td class="bg-color bg-img font-color"><code>0xxxxxxx</code></td>
</tr>
<tr>
<th class="bg-color bg-img font-color">11</th>
<td class="bg-color bg-img font-color">U+0080</td>
<td class="bg-color bg-img font-color">U+07FF</td>
<td style="text-align: center;" class="bg-color bg-img font-color">2</td>
<td class="bg-color bg-img font-color"><code>110xxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
</tr>
<tr class="bg-color bg-img font-color">
<th class="bg-color bg-img font-color">16</th>
<td class="bg-color bg-img font-color">U+0800</td>
<td class="bg-color bg-img font-color">U+FFFF</td>
<td style="text-align: center;" class="bg-color bg-img font-color">3</td>
<td class="bg-color bg-img font-color"><code class="bg-color bg-img font-color">1110xxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
</tr>
<tr>
<th class="bg-color bg-img font-color">21</th>
<td class="bg-color bg-img font-color">U+10000</td>
<td class="bg-color bg-img font-color">U+1FFFFF</td>
<td style="text-align: center;" class="bg-color bg-img font-color">4</td>
<td class="bg-color bg-img font-color"><code>11110xxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
</tr>
<tr>
<th class="bg-color bg-img font-color">26</th>
<td class="bg-color bg-img font-color">U+200000</td>
<td class="bg-color bg-img font-color">U+3FFFFFF</td>
<td style="text-align: center;" class="bg-color bg-img font-color">5</td>
<td class="bg-color bg-img font-color"><code>111110xx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
</tr>
<tr>
<th class="bg-color bg-img font-color">31</th>
<td class="bg-color bg-img font-color">U+4000000</td>
<td class="bg-color bg-img font-color">U+7FFFFFFF</td>
<td style="text-align: center;" class="bg-color bg-img font-color">6</td>
<td class="bg-color bg-img font-color"><code>1111110x</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
<td class="bg-color bg-img font-color"><code>10xxxxxx</code></td>
</tr>
</tbody></table>

## Example

Translate '€' into binary Utf-8. 

1. The Unicode code point for "€" is U+20AC.

2. According to the scheme table above, this will take 3 bytes (16 bits).

3. Convert hexadecimal 20AC into a 16-bit binary 0010000010101100.

4. Fill in the 16 bits into: 1110xxxx	10xxxxxx	10xxxxxx, we got 11100010 10000010 10101100 

5. Almost done. The result can be concisely written in hexadecimal, as E2 82 AC.

Note that the last byte of any encoding starts with '0', in this way computer can easily identify the encoding length of every character. Also __note that ASCII code is natively supported by Utf-8__. 