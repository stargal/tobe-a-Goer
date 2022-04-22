---
title: "PopCountAlgorithm"
date: 2022-04-04T21:17:55+08:00
---

#  Population Count Algorithms

> **"Population count" means to <font color = "red">count the number of population bits in a 64-bit word.</font>**

#### Here are some algorithms to solve the problem

<!--more-->

- ##### Lookaside table

  > With the Go's `init` function to precompute eight lookaside table, representing the eight bytes of the 64-bit word.
  >
  > The `inint` function is always used to initialize more complex variable,like data table. 
  >
  > This kind of function may not be just one, the functions will automatically execute in the order in which they are declared

  <font color = "red">Be careful !: the init function can't be called or referenced</font>

  ```go
  package popcount
  
  //	p[i] is the population count of i.
  var p [256]byte
  
  func init() {
  	for i := range p {
  		p[i] = p[i/2] + byte(i&1)
  	}
  }
  
  //	PopCount returns the population count (number of set bits) of x.
  func PopCount(x uint64) int {
    var res int = 0
    for i := 0; i < 8; i++ {
  	res += int(p[byte(x)])
  	x >>= 8
    }
    return res
  }
  ```

- ##### use the quality: `x&(x-1)` statement can clear the  rightmost  bit of the 64-bit word

  ```c
  func PopCount(x uint64) int {
    var res int = 0
    for i := 0; i < 8; i++ {
  	res += int(p[byte(x)])
  	x >>= 8
    }
    return res
  }
  ```

  
