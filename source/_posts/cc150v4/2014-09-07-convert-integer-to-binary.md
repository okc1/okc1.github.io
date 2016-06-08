---
layout: post
title: "[CC150v4] 5.2 Convert Integer to Binary Form "
comments: true
category: CC150v4

---

### Question

> Given a (decimal - e.g. 3.72) number that is passed in as a string, print the binary representation. 

> If the number can not be represented accurately in binary, print “ERROR” 

### Solution

Convert the integer part is easy. 

__The difficulty is how to convert a floating point (the decimal part) to binary form__. The idea suggested in the book is to keep x2, and subtract 1 when necessary. Eg. 

> 0.625 x 2 = 1.25, append 1
>
> 0.25 x 2 = 0.5, append 0
>
> 0.5 x 2 = 1, append 1
>
> the binary form of 0.625 would be 0.101.

We must declarify the max number of digits in the decimal part. In the book, __the answer assumes a maximum digits of 32 bits__ (i.e. when binary length grows more than 32 bits, return "Error"). 

### Code

__written by me__

	public static String printBinary(String n) {
		String[] num = n.split("\\.");
		int integer = Integer.parseInt(num[0]);
		double decimal = Double.parseDouble("0." + num[1]);

		// now convert decimal part, if can't convert, return ERROR
		StringBuilder sb = new StringBuilder();
		while (decimal != 0) {
			if (sb.length() > 32) {
				return "ERROR";
			}
			double newDoub = 2 * decimal;
			sb.append(newDoub >= 1 ? "1" : "0");
			decimal = newDoub % 1;
		}

		// now convert integer part
		String intStr = "";
		while (integer != 0) {
			intStr = ((integer & 1) == 1 ? "1" : "0") + intStr;
			integer = integer >> 1;
		}

		// return the 2 parts connected with a dot
		return intStr + "." + sb.toString();
	}
