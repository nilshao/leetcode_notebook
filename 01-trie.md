# 前缀树

## 介绍

N叉树的一种特殊形式，通常用于存储字符串，每一个节点用于存储一个字符串（的前缀），子节点代表的字符串是由节点本身的 原始字符串 ，以及 通往该子节点路径上所有的字符 组成的。根节点为空。

![trie001](https://github.com/nilshao/leetcode_notebook/blob/master/pics/01-trie/trie001.png)

前缀树的一个重要的特性是，节点所有的后代都与该节点相关的字符串有着共同的前缀。这就是 前缀树 名称的由来。

用途：自动补全，拼写检查等等。我们将在后面的章节中介绍实际应用场景。

## 表示

### 方法一：数组

如果我们只存储含有字母 a 到 z 的字符串，我们可以在每个节点中声明一个大小为 26 的数组来存储其子节点。对于特定字符 c ，我们可以使用 c - 'a' 作为索引来查找数组中相应的子节点。

```C++

// change this value to adapt to different cases
#define N 26

struct TrieNode {
    TrieNode* children[N];
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: (root->children)[c - 'a']
 */

```

### 方法二：map

第二种方法是使用 Hashmap 来存储子节点。可以在每个节点中声明一个 Hashmap 。Hashmap 的键是字符，值是相对应的子节点。

```C++
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    
    // you might need some extra values according to different cases
};

/** Usage:
 *  Initialization: TrieNode root = new TrieNode();
 *  Return a specific child node with char c: (root->children)[c]
 */

```
通过相应的字符来访问特定的子节点 更为容易 。但它可能比使用数组 稍慢一些 。但是，由于我们只存储我们需要的子节点，因此 节省了空间 。这个方法也更加 灵活 ，因为我们不受到固定长度和固定范围的限制。

### 补充

我们已经提到过如何表示前缀树中的子节点。除此之外，我们也需要用到一些其他的值。

例如，我们知道，前缀树的每个节点表示一个字符串，但并不是所有由前缀树表示的字符串都是有意义的。如果我们只想在前缀树中存储单词，那么我们可能需要在每个节点中声明一个布尔值（Boolean）作为标志，来表明该节点所表示的字符串是否为一个单词。


