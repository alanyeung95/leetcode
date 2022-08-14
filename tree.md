## binary-tree-maximum-path-sum
### my ans
```
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        left = [float("-inf"), float("-inf")]
        right = [float("-inf"), float("-inf")]
        
        if root.left:
            self.helper(root.left, left)
            
        if root.right:
            self.helper(root.right, right) 

        return max(root.val + max(0, left[0], right[0],  left[0] + right[0]), left[0], right[0], left[1], right[1])
    
    def helper(self, root: Optional[TreeNode], result):
        if not root:
            result = [0,0]

        left = [float("-inf"), float("-inf")]
        right = [float("-inf"), float("-inf")]
        
        if root.left:
            self.helper(root.left, left)
            
        if root.right:
            self.helper(root.right, right) 
        
        result[0] = root.val + max(0, left[0], right[0])
        result[1] = max(root.val + max(0, left[0] + right[0]), left[0], right[0], left[1], right[1])
```
### ans

```
# ref: https://leetcode.com/problems/binary-tree-maximum-path-sum/discuss/603423/Python-Recursion-stack-thinking-process-diagram
1. class Solution:
2.     def maxPathSum(self, root: TreeNode) -> int:
3. 		max_path = float("-inf") # placeholder to be updated
4. 		def get_max_gain(node):
5. 			nonlocal max_path # This tells that max_path is not a local variable
6. 			if node is None:
7. 				return 0
8. 				
9. 			gain_on_left = max(get_max_gain(node.left), 0) # Read the part important observations
10. 		gain_on_right = max(get_max_gain(node.right), 0)  # Read the part important observations
11. 			
12. 		current_max_path = node.val + gain_on_left + gain_on_right # Read first three images of going down the recursion stack
13. 		max_path = max(max_path, current_max_path) # Read first three images of going down the recursion stack
14. 			
15. 		return node.val + max(gain_on_left, gain_on_right) # Read the last image of going down the recursion stack
16. 			
17. 			
18. 	get_max_gain(root) # Starts the recursion chain
19. 	return max_path		
```

## construct-binary-tree-from-preorder-and-inorder-traversal
### ans
```
def buildTree(self, preorder, inorder):
    if inorder:
        ind = inorder.index(preorder.pop(0))
        root = TreeNode(inorder[ind])
        root.left = self.buildTree(preorder, inorder[0:ind])
        root.right = self.buildTree(preorder, inorder[ind+1:])
        return root
```

## deepest-leaves-sum

### ans
```
def deepestLeavesSum(self, root):
    q = [root]
    while q:
        pre, q = q, [child for p in q for child in [p.left, p.right] if child]
    return sum(node.val for node in pre)
```

## binary-tree-inorder-traversal
visit left node, then parent node, finally right node
### ans
```
# recursively
def inorderTraversal1(self, root):
    res = []
    self.helper(root, res)
    return res
    
def helper(self, root, res):
    if root:
        self.helper(root.left, res)
        res.append(root.val)
        self.helper(root.right, res)
 
# iteratively       
def inorderTraversal(self, root):
    res, stack = [], []
    while True:
        while root:
            stack.append(root)
            root = root.left
        if not stack:
            return res
        node = stack.pop()
        res.append(node.val)
        root = node.right
```

## invert-binary-tree
### iterative ans
```
def invertTree(self, root):
    stack = [root]
    while stack:
        node = stack.pop()
        if node:
            node.left, node.right = node.right, node.left
            stack += node.left, node.right
    return root
```

## maximum-depth-of-binary-tree

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

### iterative ans
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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int max = 1;
        
        Stack<TreeNode> nodes = new Stack<>();
        Stack<Integer> depths = new Stack<>();
        
        nodes.push(root);
        depths.push(1);
        
        while (!nodes.empty()) {
            TreeNode curr = nodes.pop();
            int depth = depths.pop();
            
            if (curr.left == null && curr.right == null) {
                max = Math.max(max, depth);
            } 
            
            if (curr.right != null) {
                nodes.push(curr.right);
                depths.push(depth + 1);
            } 
            if (curr.left != null) {
                nodes.push(curr.left);
                depths.push(depth + 1);
            }
        }
        
        return max;
        
    }
}
```

## symmetric-tree
```
Input: root = [1,2,2,3,4,4,3]
Output: true
```

```
Input: root = [1,2,2,null,3,null,3]
Output: false
```

### ans (iterative)
```
 class Solution2:
  def isSymmetric(self, root):
    if root is None:
      return True

    stack = [[root.left, root.right]]

    while len(stack) > 0:
      pair = stack.pop(0)
      left = pair[0]
      right = pair[1]

      if left is None and right is None:
        continue
      if left is None or right is None:
        return False
      if left.val == right.val:
        stack.insert(0, [left.left, right.right])

        stack.insert(0, [left.right, right.left])
      else:
        return False
    return True
```
