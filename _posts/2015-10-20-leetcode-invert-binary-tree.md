---
layout:     post
title:      LeetCode - Invert Binary Tree
date:       2015-10-20 23:27:02
summary:    Invert a binary tree.
categories: leetcode
---


### Invert a binary tree. [Link](https://leetcode.com/problems/invert-binary-tree/)

~~~
     4
   /   \
  2     7
 / \   / \
1   3 6   9
~~~

to

~~~
     4
   /   \
  7     2
 / \   / \
9   6 3   1
~~~


## Recursive Solution

~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        
        if (null == root) {
            return root;
        }
        
        // switch the current left and right
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        
        // if the current left and right are not leaves
        // recursively switch each of them
        if (null != root.left) {
            root.left = invertTree(root.left);
        }
        
        if (null != root.right) {
            root.right = invertTree(root.right);
        }
        
        return root;
        
    }
}
~~~


## Non-recursive Solution


~~~ java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        
        if (null == root) {
            return root;
        }
        
        LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        
        while(queue.size() > 0) {
            
            // switch the current node's left and right
            TreeNode node = queue.poll();
            TreeNode tmp = node.left;
            node.left = node.right;
            node.right = tmp;
            
            // put the current node's non-empty left and right 
            // into the queue and let them wait to be switched
            if (null != node.right) {
                queue.add(node.right);
            } 
            
            if (null != node.left) {
                queue.add(node.left);
            }
        }
        
        return root;
    }
}
~~~
