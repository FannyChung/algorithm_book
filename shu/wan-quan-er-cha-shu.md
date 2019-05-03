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

改变状态的时机：有任意子为空

```java
if(l==null||r!=null) return false;
if(start&&(l!=null||r!=null)) return false;
if(l!=null) queue.add(l);
if(r!=null) queue.add(r);
else start=true;//右子为空
```



