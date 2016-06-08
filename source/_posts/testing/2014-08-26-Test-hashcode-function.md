---
layout: post
title: "[Testing] Test hashCode() function"
comments: true
category: Testing

---


### Question

> How to test hashCode() function? Example: 

	public int hashCode(){
		int result = 17 + hashDouble(re);
		result = 31 * result + hashDouble(im);
		return result;
	}

### Solution

We need to test that the hash function is [reflexive, symmetric, and transitive](http://stackoverflow.com/a/4449791). 

### Code

Not including 'not equal' test. 

	@Test
	public void testEquals_Symmetric() {
		Person x = new Person("Foo Bar");  // equals and hashCode check name field value
		Person y = new Person("Foo Bar");
		Assert.assertTrue(x.equals(y) && y.equals(x));
		Assert.assertTrue(x.hashCode() == y.hashCode());
	}
