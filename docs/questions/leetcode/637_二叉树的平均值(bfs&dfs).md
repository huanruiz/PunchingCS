dfs bfs都可以, 主要注意数据类型的转换, 对于dfs来说要保证level一致. 对于bfs要根据queue的大小来判断下一层的node数量.
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        ArrayList<Integer> count = new ArrayList<>();
        ArrayList<Double> sum = new ArrayList<>();
        dfs(count, sum, root, 0);
        List<Double> res = new ArrayList<>();
        for (int i = 0; i < count.size(); i++)
        res.add(sum.get(i)/count.get(i));
        return res;
    }

    public void dfs(ArrayList<Integer> count, ArrayList<Double> sum, TreeNode root, int level) {
        if (root == null) {
            return;
        }

        if (level >= sum.size()) {
            count.add(1);
            sum.add(root.val * 1.0);
        } else {
            count.set(level, count.get(level)+1);
            sum.set(level, sum.get(level)+root.val);
        }
        dfs(count, sum, root.left, level + 1);
        dfs(count, sum, root.right, level + 1);
    }
}
```