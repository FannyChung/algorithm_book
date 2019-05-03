# 完全二叉树

完全二叉树是每一层都是满的，只有最后一层的最后几个节点是空的。

## 判断是否是完全二叉树

完全二叉树的特性是满二叉树去掉层次遍历的最后几个节点。所以如果层次遍历一旦出现空子，就开启了某种状态，要求后面的子全部都是空的。

```java
boolean start=false;
while(!queue.ieEmpty()){
    cur=queue.pop();
    if(!start){
        if(cur.left==null&&cur.right!=null) return false;
        if(cur.right==null||cur.left==null) start=true;
        //加入非空子
        if(cur.left!=null){
            queue.add(cur.left);
        }
        if(cur.right!=null) queue.add(cur.right)
    }else{//start
        if(cur.left!=null||cur.right!=null){
            return false;
        }
    }

}
return true;
```

更加简洁的写法：

返回false的情况：1. 有左子空而右子不空；2. start状态开启而有子不空

否则把子加入队列

改变状态的时机：有任意子为空（此时右子一定为空）

```java
if(l==null||r!=null) return false;
if(start&&(l!=null||r!=null)) return false;
if(l!=null) queue.add(l);
if(r!=null) queue.add(r);
else start=true;//右子为空
```

## 完全二叉树的节点数

用少于O\(N\)的方法。

因为满二叉树的高h和节点数N的关系是：$$N = 2^{h-1} -1$$。所以可以找到满二叉树子树，进行加和。

现在问题是如何分解为满二叉树，可以根据右子的最左路径的高度判断左子是否满，如果右子的最左路径到了最下面（当前节点的高度-1），则左子树一定是满的；否则，右子是一颗欠缺一层的满二叉树。

因此问题分解为：

1. 如果右子高度不欠缺，则当前子树的结点数为：$$2^{h-1}-1+1+recurse(cur.right)$$
2. 如果右子高度欠缺，则当前子树的节点数为：$$2^{h-2}-1+1+recurse(cur.left)$$

下面分析如何实现递归：需要收集的信息有：

右子高度：直接求

当前高度（总高度-递归的时候向上传下来的深度）

所以递归函数的参数为\(curNode,curDep,totalH\)；返回结果为当前子树的总结点数。



