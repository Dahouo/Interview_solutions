### Tips

- We can't simply multiply out n! and count number of 0s since n! may be too big to fit in an int/long.
- Trailing 0's are created by 2's and 5's. Since we will always have more 2's than 5's, the 5's will determine # of 0's.

### Solution 1

- Count # of factors of 5's in each term of the factorial (1...n) - Not coded since I like solution 2 better.

### Solution 2

- Count multiples of 5 (btwn 1 and n), then multiples of 25, then 125

```
Special numbers:
  5   = 5
  25  = 5 x 5           Our code will properly add 2 to count for this
  125 = 5 x 5 x 5       Our code will properly add 3 to count for this
  625 = 5 x 5 x 5 x 5   Our code will properly add 4 to count for this
```

```java
int numTrailingZeros(int n) {
    if (n < 1) {
        return 0;
    }
    int fives = 0;
    for (int i = 5; i <= n; i *= 5) { // i is 5, 25, 125, 625 ...
        fives += n/i; // to count how many multiples of "i" are in range 1...n, we just do n/i
    }
    return fives;
}
```
