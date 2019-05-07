
## Solution 1

- Preorder Traversal
  - Book says if T1's preorder traversal is substring of T2's preorder traversal, and same is true for inorder traversals, then T2 is substring of T1
  - During implementation, we can insert dummy "0" for nulls. This is necessary to distinguish the 2 trees in book with duplicate values.

Not coded.

### Time/Space Complexity

- Let `t1` have `n` nodes and `t2` have m nodes
- Time Complexity: `O(n + m)` since `.isSubstring()` is linear time complexity
- Space Complexity: `O(n + m)` since we copy the trees


## Solution 2

- Recursive Search



```java
boolean containsTree(TreeNode t1, TreeNode t2) {
    if (t2 == null) { // the empty tree is always a subtree. We do this
                      // check here to avoid doing it every time in subTree.
        return true;
    }
    return subTree(t1, t2);
}

public static boolean subTree(TreeNode t1, TreeNode t2) {
    if (t1 == null) {
        return false;
    }

    if (matchTree(t1, t2)) {
        return true;
    }

    return subTree(t1.left, t2) || subTree(t1.right, t2);
}

public static boolean matchTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) {
        return true;
    } else if (p == null || q == null) {
        return false;
    }
    if (p.data != q.data) {
        return false;
    }
    return matchTree(p.left, q.left) && matchTree(p.right, q.right);
}
```

### Time/Space Complexity

- Let `t1` have `n` nodes and `t2` have m nodes
- Time Complexity
  - `O(nm)` worst case, but average case is much better since `matchTree()` usually returns false immediately, so it's `O(n + km)` where k is number of occurrences of `T2`'s root in `T1`
  - Also, even when we do call matchTree, it is likely to not match very soon in its search
- Space Complexity
  - `O(log(n) + log(m))`. Which is great.
