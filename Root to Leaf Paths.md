## 01. Root to Leaf Paths

The problem can be found at the following link: [Question Link](https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1?page=1&category=Arrays,Strings,Matrix,Stack,Queue,Map,set,Pointers&company=Amazon,Microsoft,Google,Flipkart&difficulty=Basic,Easy,Medium&status=unsolved&sortBy=submissions)

### Problem Description

**Task:** Given a Binary Tree, you need to find all the possible paths from the root node to all the leaf nodes of the binary tree.

> **Note:** The paths should be returned such that paths from the left subtree of any node are listed first, followed by paths from the right subtree.

#### Examples

##### Example 1

- **Input:**
```text
root = [1, 2, 3, 4, 5, N, N]
```
- **Output:**
```text
[[1, 2, 4], [1, 2, 5], [1, 3]]
```
- **Explanation:** All the possible paths from root node to leaf nodes are: 1 - > 2 - > 4, 1 - > 2 - > 5 and 1 - > 3

##### Example 2

- **Input:**
```text
root = [1, 2, 3]Output: [[1, 2], [1, 3]]
```
- **Explanation:** All the possible paths from root node to leaf nodes are: 1 - > 2 and 1 - > 3

##### Example 3

- **Input:**
```text
root = [10, 20, 30, 40, 60, N, N]
```
- **Output:**
```text
[[10, 20, 40], [10, 20, 60], [10, 30]]Explanation: All the possible paths from root node to leaf nodes are: 10 - > 20 - > 40, 10 - > 20 - > 60 and 10 - > 30
```

#### Constraints

- **1.** `1 ≤ number of nodes ≤ 10⁴¹ ≤ node- > data ≤ 10⁴^`

### Time and Auxiliary Space Complexity

- **Expected Time Complexity:** O(n)
- **Expected Auxiliary Space Complexity:** O(h)

### Accepted Solutions (1)

#### Solution 1 (C++)

- **Submitted:** 2026-08-01 18:10:28
- **Status:** Correct
- **Marks:** 4

```cpp
/* Definition for Node
class Node {
  public:
    int data;
    Node* left;
    Node* right;
    Node(int val) {
        data = val;
        left = right = nullptr;
    }
}; */
class Solution {
private:
    void dfs(Node* node, vector<int>& current_path, vector<vector<int>>& ans) {
        if (!node) return;

        // Include the current node in the path
        current_path.push_back(node->data);

        // If it's a leaf node, add the path to our answer list
        if (!node->left && !node->right) {
            ans.push_back(current_path);
        } else {
            // Traverse left and right subtrees
            dfs(node->left, current_path, ans);
            dfs(node->right, current_path, ans);
        }

        // Backtrack to explore alternative branches
        current_path.pop_back();
    }

public:
    vector<vector<int>> paths(Node* root) {
        vector<vector<int>> ans;
        vector<int> current_path;
        dfs(root, current_path, ans);
        return ans;
    }
};
```

*Generated on: 8/1/2026, 6:10:51 PM*