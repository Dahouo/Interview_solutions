### Solution

```java
ArrayList<String> generateParentheses(int count) {
    char[] str = new char[count * 2];
    ArrayList<String> solutions = new ArrayList<>();
    addParenthesis(0, count, count, str, solutions);
    return solutions;
}

private void addParenthesis(int index, int leftRem, int rightRem, char[] expression, ArrayList<String> solutions) {
    if (leftRem == 0 && rightRem == 0) {
        solutions.add(String.valueOf(expression)); // .valueOf converts char[] to String
        return;
    }
    if (leftRem > 0) {
        expression[index] = '(';
        addParenthesis(index + 1, leftRem - 1, rightRem, expression, solutions);
    }
    if (rightRem > 0 && rightRem > leftRem) {
        expression[index] = ')';
        addParenthesis(index + 1, leftRem, rightRem - 1, expression, solutions);
    }
}
```
