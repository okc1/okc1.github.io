---
layout: post
title: "[Google] Google API read4096 (read4K)"
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=14424684)

> Given API: int Read4096(char* buf); 

> It reads data from a file and records the position so that the next time when it is called it read the next 4k chars (or the rest of the file, whichever is smaller) from the file. The return is the number of chars read. 

> Use above API to Implement API "int Read(char* buf, int n)" which reads any number of chars from the file. 

### Solution

Since the nature of C++ and Java is different, I changed the api to: 

	GoogleApi.read4096(){}
	GoogleRead4096.read(int n){}

As [suggested](http://www.careercup.com/question?id=14424684), the solution is to keep __one local buffer__, and 1 pointer within the buffer. 

### Code

	String buffer = null;
	int p = 0;

	public String read(int n) {
		if (n < 0) {
			return null;
		} else if (n == 0) {
			return "";
		}
		StringBuilder sb = new StringBuilder();
		while (n > 0) {
			// there is (LENGTH - p) chars left in the local buffer
			if (buffer == null || p == buffer.length()) {
				// no char left in buffer, update buffer
				buffer = GoogleApi.read4096();
				p = 0;
				if (buffer.length() == 0) {
					// finish reading the file (no more input chars)
					break;
				}
			} else {
				int numChars = buffer.length() - p;
				if (numChars >= n) {
					sb.append(buffer.substring(p, p + n));
					p = p + n;
					n = 0;
				} else {
					sb.append(buffer.substring(p));
					p = buffer.length();
					n -= numChars;
				}
			}
		}
		return sb.toString();
	}
