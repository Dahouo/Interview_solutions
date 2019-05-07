### Solution 1

Linear Search

```java
Integer shortest(String[] words, String word1, String word2) {
    if (words == null || word1 == null || word2 == null) {
        return null;
    }
    int min = Integer.MAX_VALUE;
    int lastPosWord1 = -1;
    int lastPosWord2 = -1;

    for (int i = 0; i < words.length; i++) {
        if (words[i].equals(word1)) {
            lastPosWord1 = i;
        } else if (words[i].equals(word2)) {
            lastPosWord2 = i;
        }

        if (lastPosWord1 != -1 && lastPosWord2 != -1) {
            int currDistance = Math.abs(lastPosWord1 - lastPosWord2);
            min = Math.min(min, currDistance);
        }
    }
    return min;
}
```

### Solution 2

Preprocess with HashMap

1. Preprocess into `HashMap<String, ArrayList<Integer>>`, where the `ArrayList` is all the positions the word shows up in.
1. Merge 2 sorted `ArrayList`s together (using algo from mergeSort) and "flag" which list each entry is from (using `Pair` class).
1. Use Solution 1's method to then find minimum distance on our preprocessed data.

```java
public class WordDistance {

    private static HashMap<String, ArrayList<Integer>> map = new HashMap<>();

    public static void preProcess(String[] words) {
        for (int i = 0; i < words.length; i++) {
            String currWord = words[i];
            if (!map.containsKey(currWord)) {
                map.put(currWord, new ArrayList<Integer>());
            }
            ArrayList<Integer> positions = map.get(currWord);
            positions.add(i);
        }
    }

    public static Integer shortest2(String word1, String word2) {
        return findDistance(map.get(word1), map.get(word2));
    }

    /* Merges lists, then uses same algo from Solution 1 to find minimum distance */
    private static Integer findDistance(ArrayList<Integer> listA, ArrayList<Integer> listB) {
        if (listA == null || listB == null || listA.size() == 0 || listB.size() == 0) {
            return null;
        }

        ArrayList<Pair> merged = merge(listA, listB);

        int min = Integer.MAX_VALUE;
        int lastPosWord1 = -1;
        int lastPosWord2 = -1;

        for (int i = 0; i < merged.size(); i++) {
            Pair pair = merged.get(i);
            if (pair.fromListA) {
                lastPosWord1 = pair.num;
            } else {
                lastPosWord2 = pair.num;
            }

            if (lastPosWord1 != -1 && lastPosWord2 != -1) {
                int currDistance = Math.abs(lastPosWord1 - lastPosWord2);
                min = Math.min(min, currDistance);
            }
        }
        return min;
    }

    private static ArrayList<Pair> merge(ArrayList<Integer> listA, ArrayList<Integer> listB) {
        if (listA == null || listB == null || listA.size() == 0 || listB.size() == 0) {
            return null; // function assumes both lists are non-empty (to make error-checking easier to write)
        }

        ArrayList<Pair> merged = new ArrayList<>();
        int aIndex = 0;
        int bIndex = 0;
        int aValue;
        int bValue;
        while (aIndex < listA.size() && bIndex < listB.size()) {
            aValue = listA.get(aIndex);
            bValue = listB.get(bIndex);
            if (aValue < bValue) {
                merged.add(new Pair(aValue, true));
                aIndex++;
            } else {
                merged.add(new Pair(bValue, false));
                bIndex++;
            }
        }

        /* Only one of these will execute */

        while (aIndex < listA.size()) {
            aValue = listA.get(aIndex);
            merged.add(new Pair(aValue, true));
            aIndex++;
        }

        while (bIndex < listB.size()) {
            bValue = listB.get(bIndex);
            merged.add(new Pair(bValue, false));
            bIndex++;
        }
        return merged;
    }
  }
```
