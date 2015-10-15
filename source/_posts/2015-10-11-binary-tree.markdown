---
layout: post
title: "the point of binary tree"
date: 2015-10-8 16:26:28 +0800
comments: true
categories: [binary tree]
---

二叉树三种遍历总是记不住，希望写一遍以后能够记下。。
<!--more-->
- 先序：父先
- 中序：父中
- 后序：父后

已知中序和后序或者中序和先序序列事都可以重构出该二叉树，这也是常见的编程实现题目。

以先序和中序为例构建二叉树的java实现：

定义二叉树：

``` java this is a java www.baidu.com link
//TreeNode.java
public class TreeNode {
		 int val;
	     TreeNode left;
	     TreeNode right;
	     TreeNode(int x) { val = x; }		
}
```
实现算法

``` 
//solution.java
public class solution {
	public static void main(String [] args){
		int pre[] ={1,2,4,7,3,5,6,8};
		int in[] = {4,7,2,1,5,3,8,6};
		TreeNode tree = reConstructBinaryTree(pre, in);
		postTraverse(tree);
}
		
	public static TreeNode reConstructBinaryTree(int[] pre, int[] in) {
		int lengthpre = pre.length;
		int lengthin = pre.length;
		if (lengthin != lengthpre)
			return null;
		TreeNode tree = new TreeNode(pre[0]);
		tree.left = null;
		tree.right = null;
		if (lengthin == 1)
			return tree;
		int i;
		for (i = 0; i < lengthin; i++) {
			if (tree.val == in[i])
				break;
		}
		if (i > 0) {
			int leftin[] = new int[i];
			int leftpre[] = new int[i];
			for (int j = 0; j < i; j++) {
				leftin[j] = in[j];
				leftpre[j] = pre[j + 1];
			}
			tree.left = reConstructBinaryTree(leftpre, leftin);
		}
		if (i < lengthin - 1) {
			int rightin[] = new int[lengthin - i - 1];
			int rightpre[] = new int[lengthin - i - 1];
			for (int j = 0; j < lengthin - i - 1; j++) {
				rightin[j] = in[j + i + 1];
				rightpre[j] = pre[j + 1 + i];
			}
			tree.right = reConstructBinaryTree(rightpre, rightin);
		}
		return tree;
	}

	public static void postTraverse(TreeNode tree) {
		if (tree.left != null)
			postTraverse(tree.left);
		if (tree.right != null)
			postTraverse(tree.right);
		System.out.print(tree.val+" ");
	}
}
```
