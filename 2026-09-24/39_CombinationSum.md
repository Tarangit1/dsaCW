# 39. Combination Sum

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        backtrack(candidates, target, 0, new ArrayList<>(), ans);
        return ans;
    }

    private void backtrack(int[] candidates, int remaining, int start, List<Integer> curr, List<List<Integer>> ans) {
        if (remaining == 0) {
            ans.add(new ArrayList<>(curr));
            return;
        }
        if (remaining < 0) {
            return;
        }

        for (int i = start; i < candidates.length; i++) {
            curr.add(candidates[i]);
            backtrack(candidates, remaining - candidates[i], i, curr, ans);
            curr.remove(curr.size() - 1);
        }
    }
}
```
