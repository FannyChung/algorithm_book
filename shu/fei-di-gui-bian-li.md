# 非递归遍历

递归遍历的方法比较简单，就不详细说明了。从根向下递归时，会访问每个节点三次：第一次是刚来到这个节点，第二次是访问完左子树后回到该节点，第三次是访问完右子树后回到该节点。这三次访问分别对应前序、中序、后序遍历。

## 前序遍历

（中左右）用栈来记录，先把当前节点打印，再把**右子、左子**压入栈。

## 中序遍历

（左中右）想象成树由左侧路径组成。

用栈记录节点，用于递归中的第二次访问。

```java
cur=head;
stack.push(cur);
while(cur.left!=null||!stack.isEmpty()){
    if(cur.left!=null){
        stack.push(cur);
        cur=cur.left;
    }else{
        cur=stack.pop();    
        print(cur);
        //并且往右走
        cur=cur.right;
    }
}
```

## 后序遍历

（左右中）先用【前序遍历+入栈左右子逆序】的方法得到（中右左）的序列，然后再逆序。用到两个栈。

```java
cur=head;
stack.push(cur);
while(!stack.isEmpty()){
    cur=stack.pop();
    stack2.push(cur);
    if(cur.left!=null){
        stack.push(cur.left);
    }
    if(cur.right!=null){
        stack.push(cur.right);
    }
}
while(!stack2.isEmpty()){
    print(stack2.pop());
}
```



