# Construct Binary Tree from Descriptions

## Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
To construct a binary tree from the given descriptions, the key insight is to use a dictionary to keep track of all nodes and their relationships. By processing the descriptions, we can build the tree step-by-step, ensuring each node is correctly placed as a left or right child. To identify the root, we can leverage a set to track all child nodes. The root will be the node that is not present in this set.

## Approach
<!-- Describe your approach to solving the problem. -->
1. **Dictionary for Nodes:** Create a dictionary to store nodes by their values.
2. **Set for Children:** Create a set to keep track of all child nodes.
3. **Processing Descriptions:** Iterate through each description to:
   - Add nodes to the dictionary if they are not already present.
   - Set the left or right child pointers based on the `isLeft` value.
   - Add the child node to the set of children.
4. **Identify Root:** Determine the root node by finding a node that is not a child of any other node (i.e., not present in the children set).
5. **Return Root:** Return the root node, which represents the constructed binary tree.

## Complexity
- **Time complexity:**  
  The time complexity is $$O(n)$$, where $$n$$ is the number of descriptions. This is because we process each description once and perform constant-time operations (dictionary and set operations) for each one.

- **Space complexity:**  
  The space complexity is $$O(n)$$ because we store all nodes in the dictionary and all child nodes in the set. In the worst case, we may store up to 2n nodes and n child references.



# Code
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public TreeNode CreateBinaryTree(int[][] descriptions) {
          Dictionary<int, TreeNode> nodes = new Dictionary<int, TreeNode>();
        HashSet<int> children = new HashSet<int>();
        
        foreach (var desc in descriptions) {
            int parentVal = desc[0];
            int childVal = desc[1];
            bool isLeft = desc[2] == 1;
            
            if (!nodes.ContainsKey(parentVal)) {
                nodes[parentVal] = new TreeNode(parentVal);
            }
            if (!nodes.ContainsKey(childVal)) {
                nodes[childVal] = new TreeNode(childVal);
            }
            
            if (isLeft) {
                nodes[parentVal].left = nodes[childVal];
            } else {
                nodes[parentVal].right = nodes[childVal];
            }
            
            children.Add(childVal);
        }
        
        TreeNode root = null;
        foreach (var node in nodes.Values) {
            if (!children.Contains(node.val)) {
                root = node;
                break;
            }
        }
        
        return root;
    }
}
```
