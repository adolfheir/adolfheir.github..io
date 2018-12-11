---
title: 数据结构-树
date: 2018-12-11 15:48:11
tags: [tree,数据结构]
categories: algorithm
---

树的结点包含一个数据和多个指向子树的分支 结点拥有的子树的数量为结点的度，度为0的结点是叶结点，度不为0的结点为分支结点，树的度定义为树的所有结点中度的最大值。。。
 
<!-- more -->
## 普通树

### 树的概念

#### 树的度

树的结点包含一个数据和多个指向子树的分支 结点拥有的子树的数量为结点的度，度为0的结点是叶结点，度不为0的结点为分支结点，树的度定义为树的所有结点中度的最大值。

#### 树的前驱和后继

结点的直接后继称为结点的孩子，结点称为孩子的双亲。 结点的孩子的孩子称为结点的孙子，结点称为子孙的祖先。 同一个双亲的孩子之间互称兄弟。

#### 树中结点的层次

树中根结点为第1层，根结点的孩子为第2层，依次类推。 树中结点的最大层次称为树的深度或高度

#### 树的有序性

如果树中结点的各子树从左向右是有序的，子树间不能互换位置，则称该树为有序树，否则为无序树。 

#### 森林

森林是由n棵互不相交的树组成的集合。 三棵树组成的森林如下： 

### 树的遍历

树的遍历分为递归和非递归广度优先   非递归深度优先

```javascript
// dfs 递归
let arr =[]
function deepTraversal(tree){
    if(tree != null){
        arr.push(tree);
        let child = tree.children;
        for (let i = 0; i < child.length; i++) {
            deepTraversal(child[i])        
        }
    }
}
deepTraversal(tree)
console.log(arr)
// dfs 非递归
let arr = []; 
function deepTraversal(tree) {  
    if (tree != null) {  
        let stack = [];  
        stack.push(tree);  
        while (stack.length != 0) {
            let item = stack.pop();  
            arr.push(item);  
            let children = item.children;  
            for (let i = children.length - 1; i >= 0; i--)  
                stack.push(children[i]);  
        }  
    }    
}  
deepTraversal(tree)
console.log(arr)
// bfs 非递归
let arr = []; 
function wideTraversal(tree) {  
    if (tree != null) {  
        let queue = [];  
        queue.unshift(tree);  
        while (queue.length != 0) {  
            let item = queue.shift();  
            arr.push(item);  
            let children = item.children;  
            for (let i = 0; i < children.length; i++)  
                queue.push(children[i]);  
        }  
    }  
} 
wideTraversal(tree)
```

