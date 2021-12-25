---
template: BlogPost
path: /string-java-tle-burst-balloon
date: 2021-12-25T01:52:56.768Z
title: The "String+HashMap" in Java that led to TLE in Burst Balloons DP
---
Burst Balloons is a very famous Leetcode hard dynamic programming (DP) problem.

It's kind of tricky but once you have understood how the classical patterns of Matrix Chain Multiplication variant work, it won't be that hard as it looks like.

So, coming back to the whole point of this post. This post doesn't tell you how to solve or an intuition behind it. It is generally a slight variation in the memoized version of the DP that blew my mind.

<u>Basic Context</u>\
Memoization is a way to solve a DP problem by storing the previously solved subp-problems. If none of this makes sense, then maybe come back a bit later (maybe a little background knowledge on programming, dynamic programming and memoization would help a lot).

<u>Continue</u>\
If you already know about what I said in the previous paragraph, go on, it will be a delight to know about it(if you don't know it obviously)

<u>Earlier</u>\
I am kind of lazy to write, initialize variables, and all in the case of DP.\
So, I generally go with the recursive version and add a global HashMap<String, Integer> or HashMap<String, Type> depending on the requirements of the problem where I generally create a string by appending some special characters like comma(,) or dots(.) or star(*) or pound('#'), etc. (you got what I am saying, right?).

No?

Alright, see the below example

```java
HashMap<String, Integer> map;
int dpSolver(int nums[], int i, int j){
  if(i > j)
    return 0;
  
  //generating the key (to query the solution space to check if the required thing is already computed)
  String key = i + "," + j;
  //accessing the already computed values
  if(map.get(key) != null)
    return map.get(key);
  
  //logic to calculate
  
  map.put(key, computedValue);
  return computedValue;
}

public static void main(String[] args){
  map = new HashMap<>();
  //considered it initialized
  int nums[] = new int[10];
  return dpSolver(nums, 0, nums.length - 1);
}
```

The reason I had to use a comma or a special character is to separate two separate scenarios like the following.

If I haven't used comma in the above case, the following would be the scenario that is totally unexpected. Hence, I have to use a special delimeter.

```
Case 1:
i = 1, j = 12
String key = "112"

Case 2:
i = 11, j = 2
String key = "112"
```

Now you got the background.

So, in case of solving the burst balloons problem, I did use what I had been using since quite some time (my special map store).

Following is the full solution for the burst balloon question in [Leetcode](https://leetcode.com/problems/burst-balloons/).

```java
class Solution {
    
    Map<String, Integer> map;
    int maxCoinsUtil(int[] arr, int i, int j){
        if(i>j)
            return 0;
        
        String key = i +"," + j;
        if(map.get(key) != null)
            return map.get(key);
         
        int ans = Integer.MIN_VALUE;
        
        for(int k=i;k<=j;k++){
            int product = arr[k];
            if(i-1>=0)
                product *= arr[i-1];
            
            if(j+1 < arr.length)
                product *= arr[j+1];
            
            int tempAns = maxCoinsUtil(arr, i, k-1) + maxCoinsUtil(arr, k+1, j) + product;
            ans = Math.max(ans, tempAns);
        }
        
        map.put(key, ans);
        return ans;
    }
    
    public int maxCoins(int[] nums) {
        map = new HashMap<>();
        int n = nums.length;
        return maxCoinsUtil(nums, 0, n-1);
    }
}
```

<br>

Guess what?

Yes, you are correct, this solution gave me a TLE (Time Limit Exceeded).

<u>Solution</u>\
I just replace my map with a 2D array and things worked like a charm.

<br>

```
class Solution {
    
    
    int[][] dp;
    int maxCoinsUtil(int[] arr, int i, int j){
        if(i>j)
            return 0;
        
        if(dp[i][j] != -1)
            return dp[i][j];
        
        int ans = Integer.MIN_VALUE;
        
        for(int k=i;k<=j;k++){
            int product = arr[k];
            if(i-1>=0)
                product *= arr[i-1];
            
            if(j+1 < arr.length)
                product *= arr[j+1];
            
            int tempAns = maxCoinsUtil(arr, i, k-1) + maxCoinsUtil(arr, k+1, j) + product;
            ans = Math.max(ans, tempAns);
        }
        
        dp[i][j] = ans;
        return ans;
    }
    
    public int maxCoins(int[] nums) {
        int n = nums.length;
        dp = new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++)
                dp[i][j] = -1;
        }
        return maxCoinsUtil(nums, 0, n-1);
    }
}
```

<br>

See, no difference at all. But this passes the Leetcode's OJ.

```
HashMap+String Memoized -> ~2600 ms﻿
2D Array Memoized -> ~120 ms﻿
﻿
I even calculated the creation of String everytime and kept adding it, but it wasn't taking much time.﻿
All the string creation in the program were around -> ~20ms.
```

<br>
﻿What I feel is the combined time of Hashing, creating a corresponding String key as well as putting the value at the correct bucket (including handling collisions) amount to this time difference.

I am not sure of what is happening internally.
Though, I would be happy to get enlightened.
﻿
Thank you, that's it for today. Keep learning and Keep Coding.
Wish you a great Christmas Eve. May all of your dreams get fulfilled and you stay happy always.
