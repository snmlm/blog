---
title: leetcode 二叉树
date: 2023/06/27
tags: 
    - leetcode
---

# 二叉树
## 二叉树遍历

- 前序遍历：先访问根节点，再前序遍历左子树，再前序遍历有子树
- 中序遍历：先中序遍历左子树，在访问根节点，再中序遍历右子树
- 后序遍历：先后序遍历右子树，再访问根节点，再后续遍历左子树

### 二叉树结构定义
```java
public class TreeNode {
    int val;
    TreeNode left;
	TreeNode right;
	TreeNode() {}
	TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
		this.val = val;
		this.left = left;
		this.right = right;
	}
}
```

### 前序递归
```java
public void preorderTraversal(TreeNode root, List<Integer> valList){
    if(root == null){
        return;
    }
    valList.add(root.val);
    preorderTraversal(root.left);
    preorderTraversal(root.right);
}
```

### 前序非递归
```java
public void preorderTraversal(TreeNode root, List<Integer> valList){
    if(root == null){
        return;
    }
    LinkedList<TreeNode> stack = new LinkedList<TreeNode>();
    while(!stack.isEmpty() || root!=null) {
        // 一直往左下遍历
        while(root!=null) {
            stack.push(root);
            valList.add(root.val);
            root = root.left;
        }
        // 无左子树的时候，去判断右子树
        root = stack.pop();
        root = root.right;
    }
}
```

### 中序递归
```java
public void inorderTraversal(TreeNode root, List<Integer> valList){
    if(root == null){
        return;
    }
    inorderTraversal(root.left);
    valList.add(root.val);
    inorderTraversal(root.right);
}
```

### 中序非递归
```java
public void inorderTraversal(TreeNode root, List<Integer> valList){
	if(root == null){
		return;
    }
    LinkedList<TreeNode> stack = new LinkedList<TreeNode>();
    while(!stack.isEmpty() || root!=null) {
        // 一直往左下遍历
        while(root != null) {
            stack.push(root);
            root = root.left;
        }
        // 无左子树的时候，去判断右子树
        root = stack.pop();
        valList.add(root.val);
        root = root.right;
    }
}
```

###  后序递归
```java
public void postorderTraversal(TreeNode root, List<Integer> valList){
    if(root == null){
        return;
    }
    postorderTraversal(root.right);
    valList.add(root.val);
    postorderTraversal(root.left);
}
```

###  后序递归
```java
public void inorderTraversal(TreeNode root, List<Integer> valList){
	if(root == null){
		return;
    }
    LinkedList<TreeNode> stack = new LinkedList<TreeNode>();
    while(!stack.isEmpty() || root!=null) {
        // 一直往右下遍历
        while(root != null) {
            stack.push(root);
            root = root.right;
        }
        // 无右子树的时候，去判断左子树
        root = stack.pop();
        valList.add(root.val);
        root = root.left;
    }
}
```

### DFS 深度搜索-从上到下
```java
public List<Integer> preorderTraversal(TreeNode root){
	List<Integer> valList = new ArrayList<>();
	dfs(root,valList);
	return valList;
}

public void dfs(TreeNode root, List<Integer> valList){
    if(root == null){
        return;
    }
    valList.add(root.val);
    dfs(root.left);
    dfs(root.right);
}
```

### DFS 深度搜索-从下向上（分治法）
```java
public List<Integer> preorderTraversal(TreeNode root){
	return divideAndConquer(root);
}

public List<Integer> divideAndConquer(TreeNode root){
	List<Integer> valList = new ArrayList<>();
	if(root == null){
		return valList;
	}
	valList.add(root.val);
	valList.addAll(divideAndConquer(root.left));
	valList.addAll(divideAndConquer(root.right));
	return valList;
}
```

> DFS 深度搜索（从上到下） 和分治法区别：前者一般将最终结果通过指针参数传入，后者一般递归返回结果最后合并

### BFS层次遍历
```java
public List<Integer> bfs(TreeNode root){
	List<Integer> valList = new ArrayList<>();
	if(root == null){
		return valList;
	}
    LinkedList<TreeNode> queue = new LinkedList<TreeNode>();
    queue.add(root);
    while (!queue.isEmpty()) {
    	//将队列的头部的元素拿出来
        TreeNode tree = queue.remove();
        if(tree != null){
        	if (tree.left != null){
        		queue.add(tree.left);
        	}
        	if (tree.right != null){
        		queue.add(tree.right);
        	}
        	list.add(tree.val);
        }
    }
    return valList;
} 
```

## 分治法应用
先分别处理局部，再合并结果

适用场景
- 快速排序
- 归并排序
- 二叉树相关问题

### 分治法模板
```java
public List<Integer> traversal(TreeNode root){
	List<Integer> valList = new ArrayList<>();
	// 递归返回条件
	if(root == null){
		return valList;
	}
	// 分段处理
	// 合并结果
	valList.add(root.val);
	valList.addAll(traversal(root.left));
	valList.addAll(traversal(root.right));
	return valList;
}
```
### 归并排序
```java
public int[] sort(int[] nums) {
        return mergeSort(nums);
    }

    public int[] mergeSort(int[] nums) {
        if (nums.length <= 1) {
            return nums;
        }
        // 分治法：二分法
        int mid = nums.length / 2;
        int[] left = new int[mid];
        int[] right = new int[nums.length - mid];
        for (int i = 0; i < nums.length; i++) {
            if (i < mid) {
                left[i] = nums[i];
            } else {
                right[i - mid] = nums[i];
            }
        }
        return merge(mergeSort(left), mergeSort(right));
    }

    public int[] merge(int[] left, int[] right) {
        int leftIndex = 0;
        int rightIndex = 0;
        int[] result = new int[left.length + right.length];
        for (int i = 0; i < result.length; i++) {
            if (leftIndex == left.length && rightIndex < right.length) {
            	// 右分支还有剩余
                result[i] = right[rightIndex];
                rightIndex++;
            } else if (leftIndex < left.length && rightIndex == right.length) {
            	// 左分支有剩余
                result[i] = left[leftIndex];
                leftIndex++;
            } else {
            	// 正常处理
                if (left[leftIndex] < right[rightIndex]) {
                    result[i] = left[leftIndex];
                    leftIndex++;
                } else {
                    result[i] = right[rightIndex];
                    rightIndex++;
                }
            }
        }
        return result;
    }
```
### 快速排序
```java
public int[] sort(int[] nums) {
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }

    public void quickSort(int[] nums, int start, int end) {
        if (start < end) {
            int mid = partition(nums, start, end);
            quickSort(nums, 0, mid - 1);
            quickSort(nums, mid + 1, end);
        }
    }

    public int partition(int[] nums, int start, int end) {
        int temp = nums[end];
        for (int i = start; i < end; i++) {
            if (nums[i] < temp) {
                swap(nums, start, i);
                start++;
            }
        }
        swap(nums, start, end);
        return start;
    }

    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
```

## 题目
{% post_link algorithm/leetcode/leetcode_104 %}</br>
{% post_link algorithm/leetcode/leetcode_110 %}</br>