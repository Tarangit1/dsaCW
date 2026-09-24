# 37. Sudoku Solver

```java
class Solution {
	public void solveSudoku(char[][] board) {
		boolean[][] rows = new boolean[9][10];
		boolean[][] cols = new boolean[9][10];
		boolean[][] boxes = new boolean[9][10];

		for (int row = 0; row < 9; row++) {
			for (int col = 0; col < 9; col++) {
				if (board[row][col] != '.') {
					int digit = board[row][col] - '0';
					rows[row][digit] = true;
					cols[col][digit] = true;
					boxes[getBoxIndex(row, col)][digit] = true;
				}
			}
		}

		solve(board, 0, 0, rows, cols, boxes);
	}

	private boolean solve(char[][] board, int row, int col,
						  boolean[][] rows, boolean[][] cols, boolean[][] boxes) {
		if (row == 9) {
			return true;
		}

		if (col == 9) {
			return solve(board, row + 1, 0, rows, cols, boxes);
		}

		if (board[row][col] != '.') {
			return solve(board, row, col + 1, rows, cols, boxes);
		}

		int boxIndex = getBoxIndex(row, col);
		for (int digit = 1; digit <= 9; digit++) {
			if (!rows[row][digit] && !cols[col][digit] && !boxes[boxIndex][digit]) {
				board[row][col] = (char) ('0' + digit);
				rows[row][digit] = true;
				cols[col][digit] = true;
				boxes[boxIndex][digit] = true;

				if (solve(board, row, col + 1, rows, cols, boxes)) {
					return true;
				}

				board[row][col] = '.';
				rows[row][digit] = false;
				cols[col][digit] = false;
				boxes[boxIndex][digit] = false;
			}
		}

		return false;
	}

	private int getBoxIndex(int row, int col) {
		return (row / 3) * 3 + (col / 3);
	}
}
```
