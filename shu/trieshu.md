# 前缀树

前缀树也叫做trie树，是一种树形dp，用空间换时间。

适合场景：

* 在给定词典中，查找是否已指定字符串开头 的。

对前缀树进行加强，给节点增加一些属性，可以丰富其功能：

* 词典中是否包含字符串——增加bool代表`isEnd`
* 词典中包含多少个指定字符串——增加`endCnt`的整数
* 词典中包含多少个指定字符串开头的——增加 `pathCnt`整数

时间复杂度：  
建立树O\(totalLen），词典中所有字符串的长度加起来

查询O\(M\)，查询的字符串的长度。



空间也是O\(totalLen\)

