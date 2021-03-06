# 定位节点

## 找带parent指针的中序后继节点

分析：一颗二叉树的中序遍历是左中右，所以：

1. 对于有右子的节点，后继是右子的最左孙
2. 如果是没有右子的节点，则是向上找还没打印过的祖先，因为打印顺序是左中右，所以当向上路径的某个祖先的儿子是左节点时，这个祖先才会没有打印过。——所以我们向上找的目标是某个祖先节点p，p.parent.left=p，则p.parent 是目标节点的后继节点。

可以根据具体例子来分析：

![](/assets/import3.png)

遍历顺序为：4251637

具体举几个例子来分析：

1. 节点1有右子，它的后继为6，也就是右子的最左孙。
2. 节点5没有右子，它的后继为1，也就是担任左子的祖先2的父亲1；节点7没有右子，它的后继是null，因为没有担任左子的祖先
3. 节点4没有右子，但是它自己是左子，所以后继为自己的父亲2.



