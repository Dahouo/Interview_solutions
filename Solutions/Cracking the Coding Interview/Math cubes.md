### Solution

```java
void printPairs() {
    /* Put Pairs in HashMap */
    HashMap<Integer, ArrayList<Pair>> map = new HashMap<>();
    for (int i = 0; i < 100; i++) {
        for (int j = 0; j < 100; j++) {
            int result = i*i*i + j*j*j;
            map.putIfAbsent(result, new ArrayList<Pair>());
            ArrayList<Pair> list = map.get(result);
            list.add(new Pair(i, j));
        }
    }

    /* Print pairs of Pairs */
    for (Integer num : map.keySet()) {
        ArrayList<Pair> pairs = map.get(num);
        for (int i = 0; i < pairs.size(); i++) {
            for (int j = 0; j < pairs.size(); j++) {
                Pair pair1 = pairs.get(i);
                Pair pair2 = pairs.get(j);
                System.out.println(pair1 + " " + pair2);
            }
        }
    }
}
```
