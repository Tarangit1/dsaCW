# 51. N-Queens

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
	public List<List<String>> solveNQueens(int n) {
		List<List<String>> result = new ArrayList<>();
		char[][] board = new char[n][n];

		for (int row = 0; row < n; row++) {
			for (int col = 0; col < n; col++) {
				board[row][col] = '.';
			}
		}

		boolean[] columns = new boolean[n];
		boolean[] diagonalLeft = new boolean[2 * n - 1];
		boolean[] diagonalRight = new boolean[2 * n - 1];

		backtrack(0, n, board, columns, diagonalLeft, diagonalRight, result);
		return result;
	}

	private void backtrack(int row, int n, char[][] board,
						   boolean[] columns, boolean[] diagonalLeft,
						   boolean[] diagonalRight, List<List<String>> result) {
		if (row == n) {
			result.add(buildBoard(board));
			return;
		}

		for (int col = 0; col < n; col++) {
			int leftIndex = row - col + n - 1;
			int rightIndex = row + col;

			if (columns[col] || diagonalLeft[leftIndex] || diagonalRight[rightIndex]) {
				continue;
			}

			board[row][col] = 'Q';
			columns[col] = true;
			diagonalLeft[leftIndex] = true;
			diagonalRight[rightIndex] = true;

			backtrack(row + 1, n, board, columns, diagonalLeft, diagonalRight, result);

			board[row][col] = '.';
			columns[col] = false;
			diagonalLeft[leftIndex] = false;
			diagonalRight[rightIndex] = false;
		}
	}

	private List<String> buildBoard(char[][] board) {
		List<String> configuration = new ArrayList<>();
		for (char[] row : board) {
			configuration.add(new String(row));
		}
		return configuration;
	}
}
```
