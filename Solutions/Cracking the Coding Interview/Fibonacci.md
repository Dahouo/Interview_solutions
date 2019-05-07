### List of Solutions

| # |      Solutions      | Runtime |   Space   |  Preference  |
|:-:|:-------------------:|:--------|----------:|:------------:|
| 1 | Recursive           |   O(n)  |   O(n)    |       -      |
| 2 | Iterative           |   O(n)  |   O(n)    |       -      |
| 3 | Iterative, no array |   O(n)  |   O(1)    |   Favorite   |

- Only downside to solution 3 is that results aren't cached, so each call to function takes O(n) time


### Solution 1

```java
public class Fibonacci {

    private final static int cacheSize = 100;
    public static int[] cache = new int[cacheSize];

    public static int fibRecursive(int n) {
        if (n < 0) {
            return -1;
        }
        cache[0] = 1; // We are defining 0th Fibonacci number as 1
        cache[1] = 1;
        return fibRecursiveHelper(n);
    }

    public static int fibRecursiveHelper(int n) {
        if (cache[n] > 0) {
            return cache[n];
        }
        cache[n] = fibRecursiveHelper(n - 1) + fibRecursiveHelper(n - 2);
        return cache[n];
    }
}
```

### Solution 2

- Solution omitted, but very similar to solution 3.


### Solution 3

```java
int fibIterative(int n) { // assumes 1st and 2nd Fibonacci numbers are defined as value 1.
    int prev = 0;
    int curr = 1;
    for (int i = 2; i <= n; i++) {
        int next = prev + curr;
        prev = curr;
        curr = next;
    }
    return curr;
}
```
