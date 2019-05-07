### Tricks

1. Represent a solution ChessBoard as an Integer[] with 8 elements (since there is a queen on each row)
1. Represent all solutions as ArrayList<Integer[]>.
1. We don't cache previous results since we are looking for ALL possible solutions

### Solution

```java
class EightQueens {
    static private final int GRID_SIZE = 8;

    public static ArrayList<Integer[]> placeQueens() {
        Integer[] board = new Integer[GRID_SIZE]; // Index is Queen's row. Value is Queen's column.
        ArrayList<Integer[]> solutions = new ArrayList<>();
        placeQueens(0, board, solutions);
        return solutions;
    }

    private void placeQueens(int row, Integer[] board, ArrayList<Integer[]> solutions) {
        if (row == GRID_SIZE) {
            /* Here, .clone() creates another Integer[] with its own deep copied Integers. If instead of Integer[] we had an array of objects,
            .clone() would still create another array of objects, but the objects would not be deep copied (they would be references to the
            original objects). This is because Integer, although an object, works differently than other objects that contain data.
            See my written lesson in "Lessons" package called ShallowDeep.java for more info */
            solutions.add((Integer[]) board.clone()); // no compiler warnings even if we omit typecast
        } else {
            for (int col = 0; col < GRID_SIZE; col++) {
                if (isValid(board, row, col)) {
                    board[row] = col;
                    placeQueens(row + 1, board, solutions);
                }
            }
        }
    }

    private static boolean isValid(Integer[] board, int rowNew, int colNew) {
        for (int rowOld = 0; rowOld < rowNew; rowOld++) {
            Integer colOld = board[rowOld];

            /* Check same column */
            if (colOld == colNew) {
                return false;
            }

            /* Check same diagonal */
            int rowDistance = rowNew - rowOld; // always positive
            int colDistance = Math.abs(colNew - colOld);
            if (colDistance == rowDistance) {
                return false;
            }
        }
        return true;
    }
}
```
