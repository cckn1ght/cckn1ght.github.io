---
layout: post
title:  "Bit Manipulation"
date:   2016-10-25 16:33:48 -0500
categories: Data Structure & Algorithms
---
### 1. Check if a given number is a power of 2
Brute force solution is to repeated divide N by 2 if N is even. Don't forget the special case, N = 0.

**Java Implementation:**

{% highlight java %}
boolean isPowerOfTwo(int num){
  if(num == 0) return false;
  else {
    while(num % 2 == 0) num /= 2;
    return num == 1;
  }
}
{% endhighlight %}

The time complexity of the brute force method is **O(logN)**.
Then here comes the magic of bit manipulation:
Think about x & (x-1). x & (x-1) will have all the bits equal to the x except for the rightmost 1 in x.

Let, x = 4 = (100)<sub>2</sub>

x - 1 = 3 = (011)<sub>2</sub>

x & (x-1) = 4 & 3 = (100)<sub>2</sub> & (011)<sub>2</sub> = (000)<sub>2</sub>

Let, x = 6 = (110)<sub>2</sub>

x - 1 = 5 = (101)<sub>2</sub>

x & (x-1) = 6 & 5 = (110)<sub>2</sub> & (101)<sub>2</sub> = (100)<sub>2</sub>

Properties for numbers which are powers of 2, is that they have one and only one bit set in their binary representation. If the number is neither zero nor a power of two, it will have 1 in more than one place. So if x is a power of 2 then x & (x-1) will be 0.

**Implementation:**
{% highlight java %}
boolean isPowerOfTwo(int num){
  return (num>0 && (num & (num - 1)) == 0);
}
{% endhighlight %}


### 2. Count the number of ones in the binary representation of the given number.

Since x & (x-1) flips the rightmost 1 into 0, we can take advantage of this operation to count 1s in a number:

{% highlight java %}
int countOne(int num){
  int count = 0;
  while(n>0) {
    n = n&(n-1);
    count++;
  }
  return count;
}
{% endhighlight %}


### 3. Check if the i<sup>th</sup> bit is set in the binary form of the given number.

To check if the i<sup>th</sup> bit is set or not (1 or 0). We can simply AND the number with 2<sup>i</sup>.
{% highlight java %}
boolean check(int num) {
  if ((num & (1 << i)) != 0) return true;
  return false;
}
{% endhighlight %}

### 4. How to generate all the possible subsets of a set ?
Because there are 2<sup>N</sup> possible subsets of any given set with N elements. We can represent each element in the suset with a bit in a binary number with length N. A bit can be either 1 or 0, thus we can use this to denote whether the corresponding element belongs to this given subset or not. So each bit pattern will represent a subset.

{% highlight java %}
void possibleSubsets(char[] A) {
  int n = A.length;
  // generate all possible binary numbers in the length of n
  for(int i = 0; i < (1 << n); ++i) {
    // check if the jth bit is set to 1.
    for(int j = 0; j < n; ++j) {
      if((i & (1 << j)) != 0) System.out.print(A[j]);
    }
    System.out.println("");
  }
}
{% endhighlight %}

### Tricks with Bits:

1) x ^ ( x & (x-1)) : Returns the rightmost 1 in binary representation of x.



2) x & (-x) : Returns the rightmost 1 in binary representation of x

(-x) is the two’s complement of x. (-x) will be equal to one’s complement of x plus 1.
Therefore (-x) will have all the bits flipped that are on the left of the rightmost 1 in x. So x & (-x) will return rightmost 1.


3) x \| (1 << n) : Returns the number x with the n<sup>th</sup> bit set.

(1 << n) will return a number with only n<sup>th</sup> bit set. So if we OR it with x it will set the n<sup>th</sup> bit of x.

<br/>

Special thanks to Prateek Garg's [original article](https://www.hackerearth.com/practice/notes/bit-manipulation/). This post is only my learning notes in bit manipulation.
