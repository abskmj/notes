---
title: "HackerRank Contest - Regular Expresso - Winning Tic Tac Toe"
date: 2017-11-19T20:31:51+05:30
tags: ["HackerRank","Solution","Regular Expression"]
---

# Solution

```java
/* Solution to HackerRank: Winning Tic Tac Toe
 * URL: https://www.hackerrank.com/contests/regular-expresso/challenges/winning-tic-tac-toe
 */

"(X|O)((...\\1){2}|..\\1..\\1|.\\1.\\1..$|\\1\\1(...)*$)"
```

### Case 1

```
(...\\1){2}) or (...\\1...\\1)

will take care of

X O -
O X O
- - X 
```

### Case 2 

```
(..\\1..\\1)

will take care of 

X - O
X O -
X - O

OR 

- X O
O X -
- X O

OR

- O X
O - X
- O X
```

### Case 3

```
(.\\1.\\1..$)

will take care of 

O - X
- X O
X O -

false positive if ..$ is not included

O X -
X O X
- O X
```

### Case 4

```
(\\1\\1(...)*$)

will take care of 

X X X
O - O
- - -

OR 

O - O
X X X
O - -

OR

O - -
O - X
X X X

false positive if (...)*$ is not included

O - X
X X -
- O O
```