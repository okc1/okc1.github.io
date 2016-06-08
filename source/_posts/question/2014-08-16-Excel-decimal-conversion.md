---
layout: post
title: "[ItInt5] Excel Decimal Conversion "
comments: true
category: Question
tags: [ ItInt5 ]
---

### Question 

[link](http://www.itint5.com/oj/#23)

> Excel中的行列数用A~Z 26个字母表示，A, B, C, D, …, Z, AA, AB, …, AZ, BA, BB, … 分别表示10进制数1, 2, 3, 4, …, 26, 27, 28, …, 52, 53, 54…。

> 请实现2个函数decToExcel和excelToDec，将10进制数转换为Excel数，以及将Excel数转换为10进制数。

### Solution

Note the indexing starts from 1, not from 0. This caused some trouble for me. 

### Code

__written by me__

    public String decToExcel(int decNum) {
        decNum--;
        int digits = 1;
        int exponen = 26;
        while (decNum >= exponen) {
            decNum -= exponen;
            exponen *= 26;
            digits++;
        }
        // now we know the total number of digits
        int num = decNum;
        int total = exponen / 26;
        String ans = "";
        for (int i = 0; i < digits; i++) {
            ans += (char) (num / total + 'A');
            num %= total;
            total /= 26;
        }
        return ans;
    }
    
    public int excelToDec(String excelNum) {
        int digits = excelNum.length();
        int total = 1;
        int sum = 1;
        for (int i = 1; i < digits; i++) {
            total *= 26;
            sum += total;
        }
        for (int i = 0; i < digits; i++) {
            sum += (excelNum.charAt(i) - 'A') * total;
            total /= 26;
        }
        return sum;
    }

__updated code__: we can actually do it recursively. The code is much more concise. 

    //将十进制数转换为excel数
	public String decToExcel(int decNum) {
		if (decNum == 0) {
			return "";
		}
		decNum--;
		char last = (char) ('A' + decNum % 26);
		return decToExcel(decNum / 26) + last;
	}
    
    //将excel数转换为十进制数
	public int excelToDec(String excelNum) {
		if (excelNum.equals("")) {
			return 0;
		}
		int len = excelNum.length();
		int last = 1 + excelNum.charAt(len - 1) - 'A';
		return excelToDec(excelNum.substring(0, len - 1)) * 26 + last;
	}
