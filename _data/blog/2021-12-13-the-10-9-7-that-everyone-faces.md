---
template: BlogPost
path: /module-10-9-7
date: 2021-12-13T03:07:52.028Z
title: The 10^9 + 7 that everyone faces.
---
MOD: 10^9 + 7 (let's say we call this MOD here)
﻿
Context:
﻿
Those who have done some competitive coding challenges or Leetcode or Hackerrank problems, you might have come across this special number to be used before returning your final answer.\
More specifically, the result in most of the cases go beyond the allowable ranges for a datatype and it overflows and introduces lot of bugs in the code.
﻿
You can get the required answer by taking a modulo of your result by MOD.
﻿
**Let's take an example of Java**
﻿
```
public int multiplier(int a, int b) {
  int c = a * b;
  return c;
}
```
﻿
In this case, we have a simple multiplier which multiplies two int numbers and returns a **int.**
﻿
If we put a = 40001, b = 40001, then both of them are well within the range of int **(-2147483648 to 2147483647**.)
﻿
But as soon as we multiply, c overflows and gets a negative number.
﻿
So, will the modulo help in this case ? Let's try it out.
﻿
```
public int multiplier(int a, int b) {
  int c = (a % MOD * b % MOD );
  return c % MOD;
}
```
﻿
Did you see what I did. 
﻿
Yes you are correct, I took the modulo with the individual number and then I took with the result.
﻿
**Problems ?**
﻿
When we multiplied both the numbers, c has already overflown and the above code basically takes a modulo on the -ve number which we never wanted.
﻿
**Solution ?** 
﻿
```
public int multiplier(int a, int b) {
  long c = a * b;
  long res = c % MOD;
  return (int) res;
}
```
﻿
This will help you solve the problem.
﻿
Thanks for reading, I hope you don't spend entire 2 hours not knowing WTH my solution is not working.
﻿
Happy Coding !
