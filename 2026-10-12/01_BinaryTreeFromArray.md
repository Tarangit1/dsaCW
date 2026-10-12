```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}

class BinaryTreeFromArray {
    public static TreeNode buildTree(int[] arr) {
        if (arr == null || arr.length == 0) return null;

        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode root = new TreeNode(arr[0]);
        queue.offer(root);
        int index = 1;

        while (!queue.isEmpty() && index < arr.length) {
            TreeNode curr = queue.poll();

            if (index < arr.length) {
                curr.left = new TreeNode(arr[index++]);
                queue.offer(curr.left);
            }
            if (index < arr.length) {
                curr.right = new TreeNode(arr[index++]);
                queue.offer(curr.right);
            }
        }

        return root;
    }
}
```