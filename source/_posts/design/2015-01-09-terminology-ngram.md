---
layout: post
title: "[Design] Terminology: n-gram "
comments: true
category: Design

---

### n-gram

In the fields of computational linguistics and probability, an __[n-gram](http://en.wikipedia.org/wiki/N-gram)__ is a contiguous sequence of n items from a given sequence of text or speech. 

The items can be phonemes, syllables, letters, words or base pairs according to the application. The n-grams typically are collected from a text or speech corpus.

#### Example

<table border="1" width="100%" id="table5" cellpadding="3" style="border-collapse: collapse" bordercolor="#89B0D8" cellspacing="0">
				<tbody><tr>
					<td bgcolor="#D9ECFF">
					<p align="center">frequency</p></td>
					<td bgcolor="#D9ECFF">
					<p align="center">word1</p></td>
					<td bgcolor="#D9ECFF">
					<p align="center">word2</p></td>
					<td bgcolor="#D9ECFF">
					<p align="center">word3</p></td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">1419</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">the</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">same</p>
					</td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">461</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">more</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">likely</p>
					</td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">432</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">better</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">than</p>
					</td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">266</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">more</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">difficult</p>
					</td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">235</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">of</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">the</p>
					</td>
				</tr>
				<tr>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">226</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">much</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">more</p>
					</td>
					<td bgcolor="#F5F9FC">
					<p style="line-height: 150%; margin-top:0; margin-bottom:0" align="center">than</p>
					</td>
				</tr>
</tbody></table>

#### Downloadable n-grams sets for English

1. __[Google n-grams](https://catalog.ldc.upenn.edu/LDC2006T13)__, based on the web as of 2006. 
1. __[COCA n-grams](http://www.ngrams.info/intro.asp)__, based on Corpus of Contemporary American English [COCA]. 450 million words from 1990 to 2012. 

With n-grams data (2, 3, 4, 5-word sequences, with their frequency), we can carry out powerful queries offline. 
