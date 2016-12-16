# LeetCode-Record
LeetCode笔记

## <a name="Catalogue"/>目录
* Easy
 * [292.Nim Game](#292.Nim Game)
 * [258.Add Digits](#258.Add Digits)
 * [104.Maximum Depth of Binary Tree](#104.Maximum Depth of Binary Tree)
 * [226. Invert Binary Tree](#226. Invert Binary Tree)
 * [283. Move Zeroes](#283. Move Zeroes)
 * [237. Delete Node in a Linked List](#237. Delete Node in a Linked List)
 * [100. Same Tree](#100. Same Tree)
 * [242. Valid Anagram](#242. Valid Anagram)
 * [171. Excel Sheet Column Number](#171. Excel Sheet Column Number)
 * [217. Contains Duplicate](#217. Contains Duplicate)
 * [169. Majority Element](#169. Majority Element)
 * [206. Reverse Linked List](#206. Reverse Linked List)
 * [326. Power of Three](#326. Power of Three)
 * [231. Power of Two](#231. Power of Two)
 * [202. Happy Number](#202. Happy Number)
 * [83. Remove Duplicates from Sorted List](#83. Remove Duplicates from Sorted List)
 * [191. Number of 1 Bits](#191. Number of 1 Bits)
 * [263. Ugly Number](#263. Ugly Number)
 * [70. Climbing Stairs](#70. Climbing Stairs)
 * [404. Sum of Left Leaves](#404. Sum of Left Leaves)
 * [121. Best Time to Buy and Sell Stock](#121. Best Time to Buy and Sell Stock)
 * [235. Lowest Common Ancestor of a Binary Search Tree](#235. Lowest Common Ancestor of a Binary Search Tree)
 * [21. Merge Two Sorted Lists](#21. Merge Two Sorted Lists)
 * [345. Reverse Vowels of a String](#345. Reverse Vowels of a String)
 * [342. Power of Four](#342. Power of Four)
 * [24. Swap Nodes in Pairs](#24. Swap Nodes in Pairs)
 * [198. House Robber](#198. House Robber)
 * [409. Longest Palindrome](#409. Longest Palindrome)
 * [415. Add Strings](#415. Add Strings)
 * [107. Binary Tree Level Order Traversal II](#107. Binary Tree Level Order Traversal II)
 * [141. Linked List Cycle](#141. Linked List Cycle)
 * [66. Plus One](#66. Plus One)
 * [27. Remove Element](#27. Remove Element)
 * [101. Symmetric Tree](#101. Symmetric Tree)
 * [118. Pascal's Triangle](#118. Pascal's Triangle)
 * [102. Binary Tree Level Order Traversal](#102. Binary Tree Level Order Traversal)
 * [110. Balanced Binary Tree](#110. Balanced Binary Tree)
 * [26. Remove Duplicates from Sorted Array](#26. Remove Duplicates from Sorted Array)


## <a name="292.Nim Game"/>292.Nim Game
###问题：

> You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

>Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

>For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

###大意：

> 你和你的一个朋友玩一个游戏：在一个桌子上有一堆石头，每个人每次可以从中拿1个或2个或3个石头，你和你朋友两个人轮流拿，谁拿走的桌上最后一波石头，谁就赢了。你先拿。
> 假设你和你的朋友都会采取最佳策略。写一个函数来判断对于给出的一个数量的石头，你会不会赢。
> 比如说，如果桌上有4个石头，那么你肯定输，无论你先拿1个还是2个还是3个，最后一波石头总是被你朋友拿走的。

###思路：
乍一看好像不递归不可能判断出来，但其实演算一下，发现是有规律可行的。

1. 首先当石头数量是3个以下时，你肯定会赢。
2. 当石头数量为4个时，你肯定输。
3. 当石头数量为5、6、7个时，你总是可以拿到桌上只剩4个，那对于你朋友来说，他面对4个石头，上面说了，一定会输，所以你一定会赢。
4. 当石头数量是8个时，你不管怎么拿，最终桌上只会剩下5、6、7三种情况，那么此时你朋友面对的就是情况3，他就一定赢，而你一定输。
5. 当石头数量是9、10、11时，你总是可以把石头拿到只剩8个，那么此时你朋友面对的就是情况4，那他就一定输，而你一定赢。
……

这样分析一下，规律就出来了，只要你面对的石头数量是4的倍数，那你就一定会输，此外，你全都可以赢，赢面还是很大啊哈哈。代码也呼之欲出了。

###代码（C++）：

```C++
class Solution {
public:
    bool canWinNim(int n) {
        return n % 4 == 0 ? false : true;
    }
};
```

示例工程：[https://github.com/Cloudox/NimGame](https://github.com/Cloudox/NimGame)

[回到目录](#Catalogue)

-------------------------

## <a name="258.Add Digits"/>258.Add Digits
###问题：

> Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

>For example:

>Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

>Follow up:
>Could you do it without any loop/recursion in O(1) runtime?

###大意：
>给一个非负数，重复地加其中的数字知道最后只有一个数字。
>比如说：
>给出数字38，过程类似于：3+8=11,1+1=2.直到2只有一个数字了，就返回它。
>继续：
>你能不能不用任何循环、递归来在O(1)的时间复杂度中完成它？

###思路一：
首先想到的就是循环，对于一个数字，循环将其除以10的余数加起来，直到其是个位数。加完一次后判断是不是只有一个数字，也就是是不是小于10，如果还大于，说明还有多个数字，那就再进行同样的操作。这个方法我自己测试倒是对的，不过leetcode总是说我超时，而且是在11这个数时就超时。。

###代码一（c++）：

```c++
class Solution {
public:
    int addDigits(int num) {
        int tempResult = num;
		while (tempResult > 10) {
		    int tempNum = tempResult;
		    tempResult = 0;
       
	        for (; tempNum / 10 >= 1;) {
			    tempResult += tempNum % 10;
			    tempNum = tempNum / 10;
		    }
		    tempResult += tempNum;
	    }
		return tempResult;
    }
};
```

###思路二：
既然题目里也鼓励我们继续思考不用循环的方式，那就一定是有规律可循。我们可以简单地列一下：

数字 | 结果
----|------
0 | 0
1 | 1
2 | 2
3 | 3
4 | 4
5 | 5
6 | 6
7 | 7
8 | 8
9 | 9
10 | 1
11 | 2
12 | 3
13 | 4
14 | 5
15 | 6
16 | 7
17 | 8
18 | 9
19 | 1
20 | 2
21 | 3

就列这么多了，我们可以发现，结果除了第一个0以外，都在1~9之间循环。而且可以发现，其除以9的余数，为0时，对应的结果是9，而不为0时，余数等于对应的结果，那么代码就呼之欲出啦~

###代码二（c++）：

```c++
class Solution {
public:
    int addDigits(int num) {
        return num % 9 == 0 ? (num == 0 ? 0 : 9) : num % 9;
    }
};
```

示例工程：[https://github.com/Cloudox/AddDigits](https://github.com/Cloudox/AddDigits)

[回到目录](#Catalogue)

-------------------------

## <a name="104.Maximum Depth of Binary Tree"/>104.Maximum Depth of Binary Tree
###问题：
>Given a binary tree, find its maximum depth.

>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

###大意：
>给出一个二叉树，找到其最大的深度。
>最大深度是指从根节点到最远的叶子节点的最长距离的节点数。

###思路：
要探索二叉树的深度，用递归比较方便。我们题目要求的函数返回根节点的深度，那么就做到对二叉树上每个节点调用此函数都返回其作为根节点看待时的深度。比如，所有叶子节点的深度都是1，再往上就是2、3...一直到root根节点的返回值就是最大的深度。
对于每个节点，我们先判断其本身是否是节点，如果是一个空二叉树，那么就应该返回0。
然后，我们定义两个变量，一个左节点深度，一个右节点深度。我们分别判断其有无左节点和右节点，两种节点中的做法都是一样的，假设没有左节点，那么就左节点深度变量就是1，有左节点的话，左节点深度变量就是对左节点调用此函数返回的结果加1；对右节点也做同样的操作。
最后比较左节点深度和右节点深度，判断谁比较大，就返回哪个变量。这样就能一层一层地递归获取最大深度了。

###代码（Java）：

```java
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
    public int maxDepth(TreeNode root) {
        if (root != null) {// 有此节点
	        int rightResult;
	        int leftResult;
	        if (root.left != null) {// 有左节点
				leftResult = maxDepth(root.left) + 1;
			} else {// 无左节点
				leftResult = 1;
			}
			if (root.right != null) {// 有右节点
				rightResult = maxDepth(root.right) + 1;
			} else {// 无右节点
				rightResult = 1;
			}
			// 判断哪边更深，返回更深的深度
            return leftResult > rightResult ? leftResult : rightResult;
        } else {// 无此节点，返回0
            return 0;
        }
    }
}
```

不过我们稍加思考一下，就可以进一步简略一下代码。因为我们代码里对于root为null的情况下返回的是0，那其实没有左节点时，对齐使用函数返回的也会是0，加1的话就是我们需要的1了，所以其实不用判断有无左节点，右节点也是一样。所以可以简化如下：

```java
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
    public int maxDepth(TreeNode root) {
        if (root != null) {
	        int rightResult = maxDepth(root.left) + 1;
	        int leftResult = maxDepth(root.right) + 1;
            return leftResult > rightResult ? leftResult : rightResult;
        } else {
            return 0;
        }
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="226. Invert Binary Tree"/>226. Invert Binary Tree
###问题：

> Invert a binary tree.
>![](http://img.blog.csdn.net/20160326150503290)
>to
>![](http://img.blog.csdn.net/20160326150528760)
>
>Trivia:
>Google: 90% of our engineers use the software you wrote (Homebrew), >but you can’t invert a binary tree on a whiteboard so fuck off.

###大意：

> 反转一个二叉树。
> 从
> ![](http://img.blog.csdn.net/20160326150503290)
> 到
> ![](http://img.blog.csdn.net/20160326150528760)
> 
> 琐事：
> Google表示如果你连反转二叉树都做不到就滚吧。

###思路：
对于二叉树的每个子节点的左右节点都要反转，我们还是用递归，对每个节点都调用函数，这样就都可以反转了。就同置换变量的数字一样，我们可以创建两个新的节点对象，然后分别等同于其左右子节点，然后将其左节点变成其右节点的新对象，将其右节点变成其左节点的新对象，就可以了。同时我们对每个子节点都要进行同样的操作。还有一点很重要不要忘记了，我们一开始要先判断此节点是否为null，不为null才进行操作。

###代码（Java）：

```java
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
        if (root == null) {// 节点为空，不处理
            return null;
        } else {// 节点不为空
            TreeNode leftNode;// 左节点新对象
            TreeNode rightNode;// 右节点新对象
            if (root.left != null) {
                leftNode = invertTree(root.left);//对其子节点进行同样的操作，并赋给新对象
            } else {
                leftNode = null;
            }
            if (root.right != null) {
                rightNode = invertTree(root.right);//对其子节点进行同样的操作，并赋给新对象
            } else {
                rightNode = null;
            }
            // 反转左右子节点
            root.left = rightNode;
            root.right = leftNode;
            return root;
        }
    }
}
```

###精简代码（Java）：
我们在处理其子节点时，也判断了是否是null的情况，但其实我们函数中对本节点就会进行一次判断，也就是说如果子节点为null，那么函数本身就会返回null，用不着特意处理了。所以可以精简一下：

```java
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
        if (root == null) {
            return null;
        } else {
            TreeNode leftNode = invertTree(root.left);
            TreeNode rightNode = invertTree(root.right);
            root.left = rightNode;
            root.right = leftNode;
            return root;
        }
    }
}
```
[回到目录](#Catalogue)

-------------------------

## <a name="283. Move Zeroes"/>283. Move Zeroes
###题目：

> Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

>For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

>Note:
>You must do this in-place without making a copy of the array.
>Minimize the total number of operations.

###大意：
>给出一个数字数组，写一个函数来移动其中的所有“0”到末尾，并保持其他非零元素的相对顺序不变。
>比如说，给出数组 nums = [0, 1, 0, 3, 12]，调用你的函数之后，nums应该变成[1, 3, 12, 0, 0]。
>注意：
>你必须在不复制数组的情况下做。
>使操作数尽可能地少。

###思路1：
首先想到了一个比较笨的方法，就是循环从头开始遍历数组中的每个数，遇到“0”，就将后面的所有数的位置往前移动一个，然后把最后一个数置为“0”，当进行完这样一次操作后，还要检测一下移动到前面来的下一位数是不是为“0”，如果是的话就再来一次同样的操作，否则就往下走。但是这样会遇到一个问题，那就是如果我后面的数都是“0”了，那我就会永远停留在某个位置循环，因为我移来移去当前位置的数都是“0”，所以在每次移动完后，就要检测一下后面的数是不是都是“0”了，只有当后面的数不都为“0”时，我才继续进行这种大挪移操作。

###代码（Java）：

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int count = nums.length;
        for (int i = 0; i < count;) {
            if (nums[i] == 0) {// 当前数为0，进行大挪移
                for (int j = i; j < count - 1; j++) {
                    nums[j] = nums[j+1];
                }
                nums[count-1] = 0;
            }
            // 检测后面的数是不是都为0
            int is = 1;
            for (int j = i; j < count; j++) {
                if (nums[j] != 0) {
                    is = 0;
                    break;
                }
            }
            // 当前数不为0，或者后面都是0时，i++
            if (nums[i] != 0 || is == 1) i++;
        }
    }
}
```

这个代码的运行时间为25ms，明显有可以精简的地方，那就是当检测到后面的数字都是“0”时，就已经没必要再循环下去了，此时的数组已经符合要求了，直接结束就好，所以可以立马做出精简：

###精简代码1（Java）：

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int count = nums.length;
        for (int i = 0; i < count;) {// 当前数是1，放到最后去，后面的数往前移
            if (nums[i] == 0) {
                for (int j = i; j < count - 1; j++) {
                    nums[j] = nums[j+1];
                }
                nums[count-1] = 0;
            } else {// 不是1
                i++;
            }
            // 检查后面的数是否都是0
            int is = 1;
            for (int j = i; j < count; j++) {
                if (nums[j] != 0) {
                    is = 0;
                    break;
                }
            }
            if (is == 1) return;// 后面都是0
        }
    }
}
```

这个代码的运行时间为23ms，减少了2ms，有一点效果，再观察一下，其实后面那个检查后面的数是否都为0的操作，明明可以放在那个移动数字的循环中去做，在移动数字时，同样也要对后面的所有数字进行操作，所以可以在同一个循环中进行，没必要循环两次，应该可以进一步缩减时间了，所以继续精简如下：

###精简代码2（Java）：

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int count = nums.length;
        for (int i = 0; i < count;) {// 当前数是1，放到最后去，后面的数往前移
            if (nums[i] == 0) {
                int is = 1;// 标记是否后面的数都为0
                for (int j = i; j < count - 1; j++) {
                    nums[j] = nums[j+1];// 后面的数往前移
                    if (nums[j] != 0) is = 0;// 标记是有不为0的数
                }
                nums[count-1] = 0;
                if (is == 1) return;// 后面都是0，直接退出
            } else {// 不是1
                i++;
            }
        }
    }
}
```

*这样一精简，运行时间反而变成了45ms，运行了几次基本都稳定在这个附近，这就无法理解了，明明应该缩减了一半的工作量，但时间反而加倍了，实在是无法想明白，请教一下大家这是为什么呢？？？*

###思路2：
之前那条路已经走不到了一个奇怪的境况中，而且感觉这种一下子移动一堆数字也不是个好办法，那么就思考另一种方法。我们可以只移动一个啊。还是从数组的第一个数开始循环，当发现“0”以后，立马在它后面找到第一个不为“0”的数字，然后交换这两个数字的位置，其余的数字都不用动，这样应该简单一些。同时，我们还是要在每次都检测后面的数字是否都为“0”，如果都为“0”了，那也没必要继续往下走了，可以直接结束。

###代码2（Java）：

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        int count = nums.length;
        for (int i = 0; i < count;) {// 当前数是1，放到最后去，后面的数往前移
            if (nums[i] == 0) {
                int is = 1;// 标记是否后面的数都为0
                for (int j = i; j < count; j++) {
                    if (nums[j] != 0) {// 找到后面第一个不为0的数
                        int value = nums[i];
                        nums[i] = nums[j];// 替换到前面来
                        nums[j] = value;
                        is = 0;// 标记后面有不为0的数
                        break;// 停止此次循环
                    }
                }
                if (is == 1) return;// 后面都是0，直接退出
            } else {// 不是1
                i++;
            }
        }
    }
}
```

这个代码的运行时间为18ms，就少了挺多了。

###他山之石：
在Disguss中看到排名第一的答案，其代码如下：

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) return;        

        int insertPos = 0;
        for (int num: nums) {
            if (num != 0) nums[insertPos++] = num;
        }        

        while (insertPos < nums.length) {
            nums[insertPos++] = 0;
        }
    }
}
```

这个代码就比较恐怖了，运行时间为0ms...完败啊。他的思路是：设置一个从0开始的标记，然后遍历每个数字，当数字不为“0”时，将nums数组的序号为标记的位置的数改成这个数，然后把标记加一，注意它的“++”是后置的，只有当检测到不为0的数字时，才会增加标记值，所以标记值永远小于等于我当前遍历到的数字的位置，就不会对其产生影响。当遍历完一次后，对标记值后面的位置的数，都置为0，这样就结束了。时间复杂度为O（n）。

[回到目录](#Catalogue)

-------------------------

## <a name="237. Delete Node in a Linked List"/>237. Delete Node in a Linked List
###题目：

> Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

>Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

###大意：

> 写一个函数来删除一个简单链表中的一个节点（除了尾节点），只给出这个节点。
> 假设有一个链表 1->2->3->4，并给你第三个值为3的节点，在调用你的函数之后这个链表应该变成1->2->4。

###思路：
一般我们删除一个链表节点，直接将其上一个节点的next指向其下一个节点就可以了，但是这里只给出了该节点本身，也就是说你只能获取到该节点本身以及其下一个节点。那么就只能将该节点直接变成下一个节点了，将其值设为下一个节点的值，将其next指向下一个节点的next，就可以了。

###代码（Java）：

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

###代码（C++）：

```c++
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void deleteNode(ListNode node) {
        *node = *node->next;
    }
}
```

###疑问：
用Java像C++那样，直接将 node = node.next 将不能ac，必须对其val和next分别设置，这是为什么呢？希望高手帮忙解答一下~

[回到目录](#Catalogue)

-------------------------

## <a name="100. Same Tree"/>100. Same Tree
###题目：
>Given two binary trees, write a function to check if they are equal or not.

>Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

###大意：
>给出两个二叉树，写一个函数来检查两者是否相等。
>所谓相等，是指他们结构相同且节点有同样的值。

###思路：
这个思路还比较直接，考虑全面一点就好了。首先考虑节点为空的情况，如果两个都为空，那么直接相等；如果一个为空一个不为空，那么不相等；如果两个都不为空，那么继续进行深层次的判断。
首先看两个节点的值是否相等，不相等则二叉树不等，然后判断其子节点，这时候使用递归就可以了，对两个节点的左节点和右节点分别调用这个函数，只有都返回相等时，才表示两个节点完全相同，由于递归，其子节点也就一层层地判断下去了，整个二叉树就会遍历完成。

###代码（Java）：

```java
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        } else if (p != null && q != null) {
            if (p.val != q.val) return false;
        
            if (isSameTree(p.left, q.left) && isSameTree(p.right, q.right)) return true;
            else return false;
        } else {
            return false;
        }
    }
}
```

其实还可以进一步精简代码，可以看下Discuss最火的代码，思路是一致的，只是精简到了极致，确实很赞：

###精简代码（Java）：
```java
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
	    if(p == null && q == null) return true;
	    if(p == null || q == null) return false;
	    if(p.val == q.val)
	        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
	    return false;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="242. Valid Anagram"/>242. Valid Anagram
###题目：

> Given two strings s and t, write a function to determine if t is an anagram of s.

>For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

>Note:
You may assume the string contains only lowercase alphabets.

>Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

###大意：

> 给出两个字符串s和t，写一个函数来判断t是否是s的易位构词。
> 比如说：
> s = "anagram", t = "nagaram", 返回true。
> s = "rat", t = "car", 返回false。
> 注意：
> 你可以假设字符串只有小写字母组成。
> 进一步：
> 如果输入包含unicode字符呢？你如何调整你的代码来适应这种情况？

###思路：
一开始，想了一个现在看来很笨的办法，这道题无非就是要检查两个字符串中的字母是否全部一致，我就遍历其中一个字符串，在每一个字符中，从另一个字符串找到第一个相同的字符，然后删掉字符串中的这个字符，继续遍历，直到有一个字符在另一个字符串中找不到了，说明没有这个字符或者数量少一些，就返回false，如果全部遍历完了都找得到，且另一个字符串也被删完了，那就返回true。这个办法我提交之后，很悲剧的超时了。。。想想也是，时间复杂度是n的平方了，还是很大的。
后来想到了另一个方法，我弄两个int数组，初始各自包含26个"0"，用来记录两个字符串中各个字母出现的次数，然后分别遍历两个数组，记录其各个字母出现的次数，最后比较两个int数组是否完全一致就可以了，一遍ac，耗时5ms，打败了85%的提交者，哈哈哈。

###代码（Java）：

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        // 用于存放两个字符串中字符出现次数的标记
        int[] sArray = new int[26];
        int[] tArray = new int[26];
        for (int i = 0; i < 26; i++) {
            sArray[i] = 0;
            tArray[i] = 0;
        }
        // 遍历两个字符串，记录字符出现次数
        char[] sCharArr = s.toCharArray();
        for (int i = 0; i < sCharArr.length; i++) {
            int index = sCharArr[i] - 97;
            sArray[index] += 1;
        }
        char[] tCharArr = t.toCharArray();
        for (int i = 0; i < tCharArr.length; i++) {
            int index = tCharArr[i] - 97;
            tArray[index] += 1;
        }
        // 比对两个记录字符出现次数的数组是否相等
        for (int i = 0; i < 26; i++) {
            if (sArray[i] != tArray[i]) return false;
        }
        return true;
    }
}
```

代码还是有点长，理所当然应该是可以精简的，然后我去看了看Discuss中最hot的答案，发现思路跟我是一样的，不过处理起来真的机智的不行：

###精简代码（Java）：

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] alphabet = new int[26];
        for (int i = 0; i < s.length(); i++) alphabet[s.charAt(i) - 'a']++;
        for (int i = 0; i < t.length(); i++) alphabet[t.charAt(i) - 'a']--;
        for (int i : alphabet) if (i != 0) return false;
        return true;
    }
}
```

其思路就是只有一个int数组，先遍历一个字符串，记录各个字母出现的次数，然后遍历另一个字符串，出现某个字母就将其对应的int数组中的值减一，最后判断int数组是否都是0，如果是，说明加减均衡，两个字符串一致，果然机智！

[回到目录](#Catalogue)

-------------------------

## <a name="171. Excel Sheet Column Number"/>171. Excel Sheet Column Number
###题目：

> Related to question Excel Sheet Column Title

>Given a column title as appear in an Excel sheet, return its corresponding column number.

>For example:

>	A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 

###大意：

> 与题目Excel Sheet Column Title相关
> 给一个像Excel中显示的列标题，返回其对应的列数。
> 比如说：
> A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 

###思路：
首先最简单的，A~Z分别是1~26。然后AA到AZ是27~(26+26)。AAA到AAZ是26*26+1 ~ 26*26 + 26。
N位字母，前面位数的字母对应的数量总和为26^(n-1)，可以总结出一个公式来。加上我们当前计算一个n位字母的列数，其前面位数的字母数量总和为26^(n-1)，设其为startCount，从当前位数的字母开始计算，计算方法为：
```
startCount + ('A' - 65)*26^(n-1) + ('A' - 65)*26^(n-2) + ... + ('A' - 65) + 1
```
这样就可以总结为代码，分两步计算，第一步计算前面位数的字母数量总和，第二部计算当前位数的数量：

###代码（Java）：
```java
public class Solution {
    public int titleToNumber(String s) {
        int count = 0;
        // 当前字母位数对应之前的数量
        int startCount = 0;
        for (int i = 1; i < s.length(); i++) {
            startCount += Math.pow(26, i);
        }
        
        // 加上前期数量
        count += startCount;
        count += 1;
        
        // 计算当前位数的数量：start + ('A' - 65)*26^(n-1) + ('A' - 65)*26^(n-2) + ... + ('A' - 65) + 1
        char[] sCharArr = s.toCharArray();
        for (int i = sCharArr.length - 1, j = 0; i >= 0; i--, j++) {
            count += (sCharArr[j] - 65) * Math.pow(26, i);
        }
        return count;
    }
}
```

###他山之石：
最Hot的一个解决方法，只需要三行代码，把计算公式进行了化简，得出了一个特别简单的计算过程：
```java
int result = 0;
for (int i = 0; i < s.length(); result = result * 26 + (s.charAt(i) - 'A' + 1), i++);
return result;
```
也是把代码行数节约到了极致。

[回到目录](#Catalogue)

-------------------------

## <a name="217. Contains Duplicate"/>217. Contains Duplicate
###题目：
>Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

###大意：
>给出一个int型的数组，判断数组是否包含了重复的数。如果有任何的数值在函数中出现过至少两次，你的数组就应该返回true，如果每个数值都是单一的，那么就返回false。

###思路：
一开始我采用之前一个判断字母数的同样的思路，用一个10位的数组记录0~9的出现次数，后来运行说还有负数。。。于是加上了-9~-1的9个数字，将数组改成19位，运行又发现还有极大的数。。。而不是我想的单一的个位数，这就超过数组的承受能力了，一开始又不说清楚= =。
于是换了一种思路，先将数组中的数字进行排序，排序之后数组中的内容就是按顺序排列的，如果有相同的数值，那一定是相邻排列的，所以只要遍历数组检查是否有相邻的两个数值相等就可以啦。这次终于ac了，看了一下Discuss的最Hot的方法，跟我的思路一样，太开心了。
关于排序有很多种方法，Java的数组自带有排序函数，也可以采用一些排序算法，可以参考这个博客：[http://blog.csdn.net/fengyifei11228/article/details/2623980](http://blog.csdn.net/fengyifei11228/article/details/2623980)，写的还蛮全的。

###代码（Java）：

```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);// 先数组内排序，参考：http://blog.csdn.net/fengyifei11228/article/details/2623980
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == nums[i + 1]) return true;// 循环判断排序后有没有两个相同的数字
        }
        return false;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="169. Majority Element"/>169. Majority Element
###题目：
>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

>You may assume that the array is non-empty and the majority element always exist in the array.

###大意：
>给出一个尺寸为n的数组，找到主要的元素。所谓主要的元素是指出现次数超过n/2的元素。
>你可以假设数组不为空且主要元素一定存在。

###思路：
第一直觉是先排序把相同的元素都放到一起再说，因为主要元素的出现次数大于n/2，那么排序后最中间的元素一定是主要元素，不管怎么移动位置，最中间的都一定是它，所以可以很简单地完成代码啦。

###代码（Java）：

```java
public class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);// 先排序
        return nums[nums.length/2];// 出现次数超过n/2次的元素排序后一定会出现在中间
    }
}
```

###他山之石：
现在让我们看看Discuss最hot的答案，我的做法并不是最快的，因为排序需要时间，他说他的时间复杂度为O(1)，看了一下代码，他的做法是：用一个变量记录主要元素，初始化为第一个元素，一个变量记录出现次数，初始化为1，遍历数组中的元素，与当前记录的主要元素相同的话，次数就加1，不同就减1，如果次数减到0，那就将主要元素换成新遍历到的元素，这样遍历完一轮得到最后记录的主要元素，就是我们要的结果。因为主要元素出现的次数大于n/2，所以可以想见最后留下来的一定会是主要元素。别的元素即使记录过也会因为次数归零抛弃掉的。这个方法只需要遍历一次数组就可以了，确实不容易想到。代码如下：

```java
public class Solution {
    public int majorityElement(int[] num) {

        int major=num[0], count = 1;
        for(int i=1; i<num.length;i++){
            if(count==0){
                count++;
                major=num[i];
            }else if(major==num[i]){
                count++;
            }else count--;

        }
        return major;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="206. Reverse Linked List"/>206. Reverse Linked List
###题目：
> Reverse a singly linked list.

###大意：
> 反转一个简单链表。

###思路：
题目的意思就是给出一个链表，本来是从头指向尾的，现在要你做成从尾指向头，并且返回原来的尾，现在的头。这个肯定是要用递归或者迭代来做。只要屡清楚过程，会比较绕。大体的流程就是，把下一个节点的next指向自己，一个个迭代、递归下去，最后返回最后的原来的尾节点

###他山之石：
这里给出Discuss中最火的方法。
迭代实现：
```java
public ListNode reverseList(ListNode head) {
    /* iterative solution */
    ListNode newHead = null;
    while (head != null) {
        ListNode next = head.next;
        head.next = newHead;
        newHead = head;
        head = next;
    }
    return newHead;
}
```

递归实现：
```java
public ListNode reverseList(ListNode head) {
    /* recursive solution */
    return reverseListInt(head, null);
}

private ListNode reverseListInt(ListNode head, ListNode newHead) {
    if (head == null)
        return newHead;
    ListNode next = head.next;
    head.next = newHead;
    return reverseListInt(next, head);
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="326. Power of Three"/>326. Power of Three
### 问题：
> Given an integer, write a function to determine if it is a power of three.

> Follow up:
Could you do it without using any loop / recursion?

### 大意：
> 给出一个整数，写一个函数来判断它是否是3的次方数。
> 进阶：
> 你能不能不用循环和递归来做？

### 思路：
一开始看这个题目没明白是什么意思，后来查了一下才知道是判断是否3的次方数，所谓次方数就是n个3相乘得出的数咯，总是容易想到立方上去。这个题其实最简单的就是不断地除以3，直到结果为0，看有没有余数，有则不是，没有则是。这个做法无论是用循环还是递归都差不多，不过题目的进阶要求是不用循环与递归，这就要想办法了。找了会规律并没有找到，看了看别人的想法发现自己数学敏感性还是太差了，这直接可以转换成求对数的计算：

n = 3^x
⇒ log3(n) = x

要判断给出的整数是不是3的立方数，只用看x是不是整数就好了。而：

log3(n) = log10(n) / log10(3)

这里在做的时候我们直接用语言中的log函数去计算，但是要注意一点，必须要使用log10这个函数，而不能用ln或者其他数字做底数的log函数，否则在遇到243这个数字的时候会判断错误，我在这里也出了问题，这应该是一个底层计算中的巧合，在计算的时候：

log(243) = 5.493061443340548    log(3) = 1.0986122886681098
   ==> log(243)/log(3) = 4.999999999999999

log10(243) = 2.385606273598312    log10(3) = 0.47712125471966244
   ==> log10(243)/log10(3) = 5.0

由于我们的判断依据是log后的结果是否是一个整数，如果用其他数作为log的底数，那计算出来应该是整数的243结果却不是整数，因为计算机在计算log(3)时实际上结果会稍微大一点点，这就坑爹了，所以只能用log10。

要判断是不是整数很简单，直接%1看余数是不是0就好了。另外别忘了还有n=0的初始情况要考虑在内。再有值得一提的就是Math并不需要额外import就可以直接使用

### 代码（Java）：

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        return (n > 0 && (Math.log10(n) / Math.log10(3)) % 1 == 0);
    }
}
```
[回到目录](#Catalogue)

-------------------------

## <a name="231. Power of Two"/>231. Power of Two
### 问题：
> Given an integer, write a function to determine if it is a power of two.

### 大意：
> 给出一个整数，写一个函数判断它是否是2的次方数。

### 思路：
这道题和另一道[判断是否是3的次方数的题目](http://blog.csdn.net/cloudox_/article/details/52582841)很像，但是这个更简单，因为有一个二进制的东西存在，我们要判断一个数是不是2的次方数，不用去一次次除以2，也不用用log去算，直接转换成二进制，如果是2的次方数，那一定是最高位为1，其余位均为0的二进制数，所以只用判断这个二进制数是不是符合这个情况就可以了。
此外还有一个地方要小心，与判断3的次方数的题目描述有一点不同在于，这里没说给出的是非负数。。。所以一定还对负数的情况进行判断，很阴险。

### 代码（Java）：

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n < 0) return false;
        String binaryStr = Integer.toBinaryString(n);
        for (int i = 0; i < binaryStr.length(); i++) {
            if (i == 0 && binaryStr.charAt(i) != '1') return false;
            else if (i > 0 && binaryStr.charAt(i) != '0') return false;
        }
        return true;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="202. Happy Number"/>202. Happy Number
### 问题：
> Write an algorithm to determine if a number is "happy".

> A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

> Example: 19 is a happy number

> 1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1

### 大意：
> 写一个算法来判断一个数字是否“happy”。
> 一个happy数字是通过下面的过程来判别的：从一个正整数开始，用其各位数字的平方和来代替它，然后重复这个过程直到数字等于1（此时就保持不变了），或者它会一直循环而不等于1。那些得到1的数字就是happy的数字。
> 距离：19是一个happy数字
> 1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1

### 思路：
一看到这个题目我是懵逼的，看一个数字是不是happy，出题人真有童心。想找规律吧算了几个数字感觉没得规律找啊。从最简单的思路来看就是不断循环看最后得到的是不是1了，但是返回true的判断容易，什么时候就可以下结论说这个数字不happy呢？这才是问题。首先我们得到的数不知道是几位数，但是经过计算后最后肯定会变成个位数，而如果这个个位数是1那就是happy了，如果不是1应该就是不happy吧。所以我一开始的做法是循环求平方和，直到结果是个位数了就看是不是1来给出结果，这里还用到了一个递归，如果计算一次平方和还不是个位数就继续递归计算。
提交后发现有个错误，那就是1111111这个数，也是一个happy数字，但我判断为不是了。我数了一下一共七个1，平方和是7，才知道原来到了个位数后还会继续计算，我算了一下发现7还真能最后算出1来，那只能对于1~9九个个位数都看看是不是能算出1来了，算了一下觉得太麻烦了，于是想到了一个简单的方法，leetcode是可以自定义测试用例的，勾选Custom Testcase就可以了，然后我把4~9都试了一遍，不用试2、3是因为就等于4、9，测完发现只有1和7是的，所以在代码里把7也算成true就可以了。
最后的时间是4ms，还不错，看了看discuss也没有看到特别好的方法，那大抵就是这样了吧。

### 代码（Java）：

```java
public class Solution {
    public boolean isHappy(int n) {
        int sum = 0;
        while (n > 0) {
            sum += Math.pow((n % 10), 2);
            n = n / 10;
        }
        if (sum >= 10) return isHappy(sum);
        else if (sum == 1 || sum == 7) return true;
        else return false;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="83. Remove Duplicates from Sorted List"/>83. Remove Duplicates from Sorted List
### 问题：
> Given a sorted linked list, delete all duplicates such that each element appear only once.

> For example,
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.

### 大意：
> 给出一个排好序的链表，删除所有的重复的数字，让每个元素只出现一次。
> 比如：
> 给出 1->1->2, 返回1->2.
给出1->1->2->3->3, 返回1->2->3.

### 思路：
既然链表本身已经排好序了，那么只用比较当前位置的值和next的值是否一样，一样就把next指向下一个再继续判断就好了，思路还是比较简单，但是有几个容易忽略的点需要注意。

1. 首先是首节点为空的情况要考虑；
2. 其次是只有当当前数字和下一个数字不一样时才把操作的节点换成下一个节点去继续向后操作，因为有可能有多个重复的数字串在一起，不能删除一个节点后就直接往后移进行判断，要判断删了一个以后下一个是否还是一样；
3. 如果链表的最后几个数字都是重复的，我们在检测到重复的数字时会删除它然后将当前节点的next指向next的next，但是这里要注意判断next是否还有next，如果没有却进行操作，那就会出错了。

在自己检测时可以试试代码对下面几个测试用例是否能通过：

* []
* [1,1]
* [1,1,2]
* [1,1,1]

### 代码（Java）：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return head;
        ListNode p = head;
        while (p.next != null) {
            ListNode q = p.next;
            if (q.val == p.val) {
                if (q.next != null) {
                    p.next = q.next;
                }
                else p.next = null;
            } 
            else p = p.next;
        }
        return head;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="191. Number of 1 Bits"/>191. Number of 1 Bits
### 问题：
> Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

> For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

### 大意：
> 写一个函数，获取一个无符号整型数并返回它拥有的‘1’bits的个数（也称为Hamming weight）。
> 比如，32位整型数‘11’二进制表示为00000000000000000000000000001011，所以函数应该返回3。

### 思路：
题目的意思其实就是问一个无符号整型数的二进制形式中有多少个1。这里无符号的意思是没有负数都是正数，直接的思路就是将它转换成二进制后一个个数里面1的个数，很简单。

### 代码（Java）：

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        String binaryStr = Integer.toBinaryString(n);
        int result = 0;
        for (int i = 0; i < binaryStr.length(); i++) {
            if (binaryStr.charAt(i) == '1') result++;
        }
        return result;
    }
}
```

### 他山之石：

```java
public static int hammingWeight(int n) {
	int ones = 0;
    	while(n!=0) {
    		ones = ones + (n & 1);
    		n = n>>>1;
    	}
    	return ones;
}
```

按照我的方法做完提交后虽然过了，也只有4ms，但是在结果统计中依然算慢的了，应该是转换成二进制那一步耗时了，然后一般数字都会有很多零，而我都会一个个判断一次，其实就不必要了。看了看Discuss中的好方法，确实挺好，直接让n和1去按位与，如果n的最后一位是1就会结果加一，然后将n右移一位继续判断，这里注意用到的右移运算发是三个箭头“>>>”，这是因为这是无符号数的右移运算符，有符号数就是两个箭头“>>”。同时循环的结束条件是n为0，这就免去了很多多余的判断，确实很赞。

[回到目录](#Catalogue)

-------------------------

## <a name="263. Ugly Number"/>263. Ugly Number
### 问题：
> Write a program to check whether a given number is an ugly number.

> Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

> Note that 1 is typically treated as an ugly number.

### 大意：
> 写一个程序来检查给出的数字是否是一个丑数字。
> 丑数字是指只能被2、3、5整除的正数。比如说，6、8是丑数字而14就不是丑数字因为它还有7这个约数。
> 注意1也被看待成丑数字。

### 思路：
leetcode中的题目都有有意思，一会happy数字一会ugly数字，也不知道是国外就这么叫的还是纯粹出题人有童心。这个题想着也没什么好办法，只能分别对2、3、5去看能不能被整除，能就除一下继续判断，直到不能被2、3、5整数了为止，看结果是不是1，是的话就是丑数字了，不是则不丑。看了看别人的做法，也大都是这个思路，这是实现上可能有点小差异。
还有一个要注意的是题目说丑数字是个正数，但没说给出的数字都是正数，在这里栽了个跟头，被0和负数弄得错了两次，我的Accepted率啊。。。

### 代码（Java）：

```java
public class Solution {
    public boolean isUgly(int num) {
        if (num <= 0) return false;
        while (true) {
            if (num % 2 == 0) {
                num = num / 2;
            } else if (num % 3 == 0) {
                num = num / 3;
            } else if (num % 5 == 0) {
                num = num / 5;
            } else if (num == 1) {
                return true;
            } else {
                return false;
            }
        }
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="70. Climbing Stairs"/>70. Climbing Stairs
### 问题：
> You are climbing a stair case. It takes n steps to reach to the top.

> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

### 大意：
> 你在爬一个楼梯。需要n节楼梯到达顶部。
> 每次你可以爬一节或者两节楼梯。你总共有多少种爬到顶部的方法？

### 思路：
总觉得这个题目小时候做过。一开始想着找找规律，按照全程走一个两节的、两个两节的、三个两节的这么去算，列了一下算式发现并没有什么规律。。。
后来想我每到一节都面临两个选择，即走一节还是走两节，于是想到用递归去做，不断返回在某一节为止走两节和走一节的走法数量之和。按照这种方法做了之后，一开始是能够解决的，测试到了44节楼梯的时候，就超时了，看了看答案给出的总走法数，确实是一个很大的数字，用递归要算的太多了。
既然往后面的走法去算走不通，那就往前看，我每来到一节新的位置的走法数量都是到上一节位置的走法数加上到上两节位置的走法数之和，一个是走一节楼梯到当前节，一个是走两节楼梯到当前节，这样从第二节开始去计算（第一节明显是一种走法，第二节开始才可以计算两节以前的位置走法数（即处于0位置时，设其为1）加上一节以前的位置走法数（即处于1位置时，设其为1）。）走到第二节的走法之和，慢慢算到最后一层。这里用一个数组去计算每一层的走法数。当然如果要节省空间也可以就用三个变量，只是每次去改变其值就可以了。

### 代码（Java）：

```java
public class Solution {
    public int climbStairs(int n) {
        int[] result = new int[n+1];
        result[0] = 1;
        result[1] = 1;
        for (int i = 2; i <= n; i++) {
            result[i] = result[i-1] + result[i-2];
        }
        return result[n];
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="404. Sum of Left Leaves"/>404. Sum of Left Leaves
### 问题：

> Find the sum of all left leaves in a given binary tree.

> Example:
> 
     3
    / \
    9  20
      /  \
     15   7
There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

### 大意：
> 计算一个二叉树中所有左叶子节点的和

> 例子:
> 
     3
    / \
    9  20
      /  \
     15   7
在这个二叉树中有两个左叶子节点，分别为9和15。因此返回24。

### 思路：
从思路来说也没有什么特别的地方，就是去做判断，细心一点不要有漏洞就好。
大体上分为判断有没有左节点和有没有右节点。如果有左节点，看左节点有没有子节点，没有（即左叶子节点）则直接用起值去加，有则继续对左节点递归。如果有右节点，且右节点有子节点，则对右节点递归，否则不管是没有右节点还是右节点没有子节点（即右叶子节点）都直接看做加0。需要注意的是如果本身节点自己是null，要返回0。另外如果只有根节点自己，也要返回0，因为题目说的是左叶子节点，根节点是不算的。最后要注意的就是在判断所有节点的子节点或者值之前，要对该节点本身是否为null做出判断，否则会有错误的。

### 代码（Java）：

```java
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
    public int sumOfLeftLeaves(TreeNode root) {
        if (root == null) return 0;
        else if (root.left == null && root.right == null) return 0;
        else {
            return ((root.left != null && root.left.left == null && root.left.right == null) ? root.left.val : sumOfLeftLeaves(root.left)) + ((root.right != null && (root.right.left != null || root.right.right != null)) ? sumOfLeftLeaves(root.right) : 0);
        }
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="121. Best Time to Buy and Sell Stock"/>121. Best Time to Buy and Sell Stock
### 问题：
> Say you have an array for which the ith element is the price of a given stock on day i.

> If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

> Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5

> max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:
Input: [7, 6, 4, 3, 1]
Output: 0

> In this case, no transaction is done, i.e. max profit = 0.

### 大意：
> 说你有一个由每天的股票价格组成的数组。
> 如果你只能进行一次交易（比如购买或者销售一个股票），设计一个算法来获取最大利润。
> 例子1：
> Input: [7, 1, 5, 3, 6, 4]
> Output: 5
> 最大的利润为：6-1 = 5（不是7-1 = 6，因为销售价格需要比购买价格大）
> 例子2：
> Input: [7, 6, 4, 3, 1]
> Output: 0
> 这个例子中，无法进行交易，所以最大收益为0。

### 思路：
这道题的意思就是，数组里的数按照顺序是每天的股票价格，你可以选择在某一天购买，然后再之后的某一天销售掉，销售的日子当然必须在购买的日子之后，也就是数组的顺序要靠后一些。要计算在哪两天进行买卖收益最大。这道题乍一看需要n*n的循环去计算每出一个价格后的最优解，我也是这样一开始就这样做，但是这样做时间复杂度太高，会超时，实际上也不用这么复杂。我们只需要每出一个新价格后，先判断这个价格减去我之前选择的买进价格后是否比之前的收益要大，以及这个新价格是否比我之前的买入价格要低，然后进行相应的操作即可，如果收益更大，就把这个收益记录下来，如果比买入价格低，就把买入价格换成这个价格。不需要担心这样直接换了之后往后计算的收益会不会不如之前，因为我们已经记录了在此之前的最大收益了，每次都会做对比的，而更换了更低的买入价格后，我们继续往后看能不能获得更大的收益，因为对于后面的数字来说这个数就是之前最小的买入价格了。其实想清楚后要进行的操作很简单，但如果想不清楚，就会觉得可能性太多了，要面面俱到总是会出问题，这里就要求头脑清晰了。

### 代码（Java）：

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int result = 0;
        int small = 0;
        if (prices.length == 0) return 0;
        else small = prices[0];
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] - small > result) result = prices[i] - small;
            if (prices[i] < small) small = prices[i];
        }
        return result;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="235. Lowest Common Ancestor of a Binary Search Tree"/>235. Lowest Common Ancestor of a Binary Search Tree
### 问题：
> Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

> According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”
>
        _______6______
       /              \
    ___2__          ___8__
    /      \        /      \ 
    0      _4       7       9
          /  \
          3   5
For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

### 大意：
 > 给出一个二叉查找树（BST），在其中找到给出的两个节点的最低的共同祖先（LCA）。

> 根据维基百科对LCA的定义：“最低共同祖先是指两个节点v和w在T中有v和w作为后代节点的最低节点（我们允许节点是自己的祖先）。”
>
        _______6______
       /              \
    ___2__          ___8__
    /      \        /      \ 
    0      _4       7       9
          /  \
          3   5
比如说，2和8的LCA是6。另一个例子，2和4的LCA是2，因为根据LCA的定义，一个节点可以是它自己的祖先。

### 思路：
这里要注意的地方是给出的二叉树是一个二叉查找树，所谓二叉查找树是指：

1. 若左子树不空，则左子树上所有结点的值均小于它的根结点的值；
2. 若右子树不空，则右子树上所有结点的值均大于它的根结点的值；
3. 左、右子树也分别为二叉排序树；
4. 没有键值相等的结点。

对于这个问题，如果是一个随意的二叉树要找LCA是比较麻烦的，要先找到目标节点的位置然后又反过来一层层找最低祖先。但是对于二叉查找树就要简单的多了，因为是排好序了的，可以简单地找到位置。

我们根据目标节点的值和根节点的值来判断目标节点在跟节点的左子树上还是右子树上，如果一个在左一个在右，就说明其LCA是根节点；如果都在左或者都在右，就对跟节点的左或者右子节点调用同样的方法进行递归。

因为没有键值相等的节点，所以判断时不用考虑等于的情况，这道题中也不需要考虑节点为null的特殊情况，所以代码很简单。

### 代码（Java）：

```java
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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val - p.val > 0 && root.val - q.val > 0) return lowestCommonAncestor(root.left, p, q);
        else if (root.val - p.val < 0 && root.val - q.val < 0) return lowestCommonAncestor(root.right, p, q);
        else return root;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="21. Merge Two Sorted Lists"/>21. Merge Two Sorted Lists
### 问题：
> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

### 大意：
> 合并两个有序链表并返回一个新链表。新链表应该包含原先两个链表中全部节点。

### 思路：
合并两个有序的链表其实思路还挺直接的，从两个链表的第一个节点开始比较大小，将小的那个放到新链表里，然后后移继续比较，大概思路就是这样，只是实现起来麻烦一点。另外其实还想到了一个奇葩的思路，就是将两个链表中的键值放到一个数组中，对数组进行排序，然后将数组里的元素按顺序放到新建的节点里去然后放入一个新链表就可以了哈哈哈。

### 代码（Java）：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        else if (l2 == null) return l1;
        
        ListNode result;
        ListNode mark;
        
        if (l1.val <= l2.val) {
            result = l1;
            l1 = l1.next;
        } else {
            result = l2;
            l2 = l2.next;
        }
        mark = result;
        
        while (l1 != null) {
            if (l2 != null && l2.val < l1.val) {
                mark.next = l2;
                mark = mark.next;
                l2 = l2.next;
            } else {
                mark.next = l1;
                mark = mark.next;
                l1 = l1.next;
            }
        }
        if (l2 != null) mark.next = l2;
        return result;
    }
}
```

### 他山之石：

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2){
		if(l1 == null) return l2;
		if(l2 == null) return l1;
		if(l1.val < l2.val){
			l1.next = mergeTwoLists(l1.next, l2);
			return l1;
		} else{
			l2.next = mergeTwoLists(l1, l2.next);
			return l2;
		}
}
```

这个方法的思路其实差不多，但是用的是递归的方式。耗时1ms，而上面我的代码耗时16ms，真的有这么大的差异么。。。

[回到目录](#Catalogue)

-------------------------

## <a name="345. Reverse Vowels of a String"/>345. Reverse Vowels of a String
### 问题：
> Write a function that takes a string as input and reverse only the vowels of a string.

> Example 1:
Given s = "hello", return "holle".

> Example 2:
Given s = "leetcode", return "leotcede".

> Note:
The vowels does not include the letter "y".

### 大意：
> 写一个函数，输入一个字符串然后翻转里面的元音字母。

> 例1：
> 给出  s = "hello"，返回"holle"。

> 例2：
> 给出 s = "leetcode"，返回"leotcede"。

> 注意：
> 元音不包括字母“y”。

### 思路：
首先想到的一个思路是遍历字符串中每个字母，遇到元音字母就记录下字母和所在的位置。遍历完后，对着记录下来的元音字母，将字符串中的元音按照反序替换一遍就好了，这种做法也做出来了，但是结果非常耗时，花了200多ms。
后来想到了第二种方法，在字符串的头和尾都放一个指针进行遍历，两端向中间去遍历，当两端都遇到元音字母后，就对换。直到两个指针碰头为止。这个方法就快多了，同时优化一下检查是否是元音字母的方法，只需要几ms就搞定了。
需要注意的是题目中并没有说字符串是纯大写或者小写，所以大小写都要考虑，这个容易忽略。


### 代码1（Java）：

```java
public class Solution {
    public String reverseVowels(String s) {
        int[] vowelIndex = new int[s.length()];
        char[] vowelChar = new char[s.length()];
        int index = 0;// 标记上面两个数组记录的位置
        // 记录元音字母及出现的位置
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == 'a' || s.charAt(i) == 'e' || s.charAt(i) == 'i' || s.charAt(i) == 'o' || s.charAt(i) == 'u' || s.charAt(i) == 'A' || s.charAt(i) == 'E' || s.charAt(i) == 'I' || s.charAt(i) == 'O' || s.charAt(i) == 'U') {
                vowelChar[index] = s.charAt(i);
                vowelIndex[index] = i;
                index++;
            }
        }
        // 替换元音字母位置
        if (index == 0) return s;
        else {
            StringBuffer buffer = new StringBuffer(s);
            for (int i = 0; i < index; i++) {
                buffer.replace(vowelIndex[i], vowelIndex[i]+1, String.valueOf(vowelChar[index-i-1]));
            }
            return buffer.toString();
        }
    }
}
```

### 代码2（Java）：

```
public class Solution {
	static final String vowels = "aeiouAEIOU";
	public String reverseVowels(String s) {
	    int first = 0, last = s.length() - 1;
	    char[] array = s.toCharArray();
	    while(first < last){
		    // 正向找元音
	        while(first < last && vowels.indexOf(array[first]) == -1){
	            first++;
	        }
	        // 逆向找元音
	        while(first < last && vowels.indexOf(array[last]) == -1){
	            last--;
	        }
	        // 对换
	        char temp = array[first];
	        array[first] = array[last];
	        array[last] = temp;
	        first++;
	        last--;
	    }
	    return new String(array);
	}
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="342. Power of Four"/>342. Power of Four
### 问题：
> Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

> Example:
Given num = 16, return true. Given num = 5, return false.

> Follow up: Could you solve it without loops/recursion?

### 大意：
> 给出一个数字（有符号32位），写一个函数来检查它是不是4的次方数。

> 例子：
> 给出 num = 16，返回true。给出 num = 15，返回false。

> 进阶：你能不能不用循环或者递归来解决它。

### 思路：
这道题也是老题目了，既可以用[判断2的次方数](http://blog.csdn.net/cloudox_/article/details/52583486)的方法稍作修改，即转化为二进制数后判断1后面的0个数是不是双数。也可以直接用[判断3的次方数](http://blog.csdn.net/cloudox_/article/details/52582841)的方法来做，直接求对数。

### 代码1（Java）：

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
		//　转化为二进制数来判断
        if (num < 0) return false;
        String binaryStr = Integer.toBinaryString(num);
        for (int i = 0; i < binaryStr.length(); i++) {
            if (i == 0 && binaryStr.charAt(i) !='1') return false;
            else if (i > 0 && binaryStr.charAt(i) != '0') return false;
        }
        if (binaryStr.length() % 2 != 1) return false;
        return true;
    }
}
```

### 代码2（Java）：

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
	    // 求对数
        return (num > 0 && (Math.log10(num) / Math.log10(4)) % 1 == 0);
    }
}
```


[回到目录](#Catalogue)

-------------------------

## <a name="24. Swap Nodes in Pairs"/>24. Swap Nodes in Pairs
### 问题：
> Given a linked list, swap every two adjacent nodes and return its head.

> For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

> Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

### 大意：
> 给出一个链表，交换每两个相邻的节点然后返回头节点。

> 例子：
> 给出 1->2->3->4，你应该返回链表 2->1->4->3。

> 你的算法应该只使用恒定的空间。你不能修改链表中的值，只有节点本身可以被改变。

### 思路：
题目里把最好用的一种方法禁止了，就是直接交换两个节点的值就可以了。但也还好做，就交换相邻节点的next指向的节点就可以了，然后递归下去，要注意判断节点是不是null的情况。不过这种做法一定要创建新的节点来临时存储节点，不知道这算不算不遵守题目要求呢。

### 代码（Java）：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head != null && head.next != null) {
            ListNode next = head.next;
            head.next = swapPairs(next.next);
            next.next = head;
            return next;
        } else return head;
    }
}
```


[回到目录](#Catalogue)

-------------------------

## <a name="198. House Robber"/>198. House Robber
## 问题：
> You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

> Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## 大意：
> 你是一个专业的盗贼，计划偷一条街上的马。每匹马都带着明确数量的金钱，唯一阻止你偷所有马的原因是相邻的马都连接了安全系统，如果相邻的两匹马在同一天夜里被偷走就会自动联系警察。

> 给出一个非负数的数组表示每匹马所带的金钱数量，计算你今晚可以在不惊动警察的情况下偷到的最大金钱数。

## 思路：
面对这么一道题，感觉没什么思路，总觉得可能性太多了，不知道怎么去快速地判断计算，看了看Discuss的讨论，看到一个方法，想一想也有点道理，但又总觉得不确定是不是完全正确，试了试测试时通过了的，还是记录下来吧。

先考虑初始情况，如果没有马，则返回0，如果只有一匹马，那就直接偷了。如果有多匹马，那么对遇到的每匹马都进行一个判断：偷这匹马（为了不惊动警察所以不偷上一匹马）所得到的总金额和偷上一匹马（为了不惊动警察所以不偷这匹马）所得到的总金额哪个更大？哪个大就偷哪个，这样一直判断到最后一匹马。当然为了要达成这个判断就需要有两个变量来记录一些数据才能进行比较。这种判断就是在每两匹马之间判断哪个得到的效果更好，应该是对的吧。

## 代码（Java）：

```java
public class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        int last = 0;
        int now = 0;
        for (int i = 0; i < nums.length; i++) {
            int temp = last;
            last = now;
            now = Math.max(temp + nums[i], last);
        }
        return now;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="409. Longest Palindrome"/>409. Longest Palindrome
### 问题：
> Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

> This is case sensitive, for example "Aa" is not considered a palindrome here.

> Note:
Assume the length of given string will not exceed 1,010.

> Example:

>> Input:
"abccccdd"

>> Output:
7

>> Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.

### 大意：
> 给出一个由小写或大写字母组成的字符串，找到能被其中的字母组成的最长的回文的长度。

> 这是区分大小写的，比如“Aa”就不能认为是回文。

> 注意：
> 假设给出的字符串长度不会超过1010。

> 例子：

>> 输入：
>“abccccdd”

>> 输出：
>7

>> 解释：
>最长的回文为“dccaccd”，长度为7。

### 思路：
这里回文的意思就是正着和反着都是一样的字母顺序。思路大家都是比较一致的，先看看字符串有哪些字母以及各自的数量，把成双成对的数量的字母都挑出来，取其能成双的最大数量，这样可以对称地放在回文的两边，然后看有没有落单的字母或者在成双后还有剩余一个的字母，有就放在回文最中间，这样就是最长的回文了，数量也就出来了。这里是区分大小写的，所以要分开算。不过题目中的1010这个最长字符串长度没发现有什么特别的用处。

### 代码（Java）：

```java
public class Solution {
    public int longestPalindrome(String s) {
        int[] letterNum = new int[26*2];
        char[] sArray = s.toCharArray();
        for (int i = 0; i < sArray.length; i++) {
             if ((sArray[i] - 'a') >= 0) {// 小写字母
                 letterNum[(sArray[i] - 'a')]++;
             } else {// 大写字母
                 letterNum[(sArray[i] - 'A' + 26)]++;
             }
        }
        
        int result = 0;
        boolean hasSingle = false;// 有无单个字符的标记
        boolean hasOdd = false;// 有无2个以上奇数数量字符的标记
        for (int i = 0; i < 26*2; i++) {
            if (letterNum[i] > 0 && letterNum[i] < 2) hasSingle = true;
            if (letterNum[i] > 1) {
                result += letterNum[i] / 2 * 2;
                if (letterNum[i] % 2 == 1) hasOdd = true;
            }
        }
        result += hasSingle || hasOdd ? 1 : 0;
        return result;
    }
}
```

### 他山之石：

```java
public int longestPalindrome(String s) {
        boolean[] map = new boolean[128];
        int len = 0;
        for (char c : s.toCharArray()) {
            map[c] = !map[c];         // flip on each occurrence, false when seen n*2 times
            if (!map[c]) len+=2;
        }
        if (len < s.length()) len++; // if more than len, atleast one single is present
        return len;
    }
```

这个做法其实思路是一样的，只是更加精简巧妙，boolan数组初始化时都是false，128的长度是为了包含所有ASCII码，懒得特意去判断大小写了，每次遇到一个字母就将其对应的位置取反，如果出现两次就会又变回false，那么每出现两次就可以将回文长度加2。最后看加起来的长度和原字符串长度是否相同，不同则说明有单个字符剩余，就可以放在回文正中间，跟我的做法比，思路差不多，代码却巧妙多了，厉害呀。

[回到目录](#Catalogue)

-------------------------

## <a name="415. Add Strings"/>415. Add Strings
### 问题：
> Given two non-negative numbers num1 and num2 represented as string, return the sum of num1 and num2.

> Note:

> 1、The length of both num1 and num2 is < 5100.
2、Both num1 and num2 contains only digits 0-9.
3、Both num1 and num2 does not contain any leading zero.
4、You must not use any built-in BigInteger library or convert the inputs to integer directly.

### 大意：
> 给出两个字符串形式的非负数num1和num2，返回num1和num2之和。

> 注意：

> 1、num1和num2的长度都小于5100。
> 2、num1和num2都只包含数字0-9。
> 3、num1和num2都不包含处于首位的0。
> 4、你不能使用任何内置的大数库或者直接将输入转化成整型。

### 思路：
题目不允许直接转化成整型去计算，也就是要我们一位一位地将数字加起来实现一次加法了。从两个字符串的最末尾开始去加，注意判断是否要进位，一位位加到两个字符串都遍历完为止，为了速度这里要使用StringBuilder，如果直接用 + 去进行字符拼接就太慢了，注意我们每次对每位数进行加时还是用整型来计算，这还是允许的，不然也太麻烦了，代码比较容易看懂。

### 代码（Java）：

```java
public class Solution {
    public String addStrings(String num1, String num2) {
        if (num1.length() == 0) return num2;
        else if (num2.length() == 0) return num1;
        
        boolean hasUp = false;// 是否进位
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        StringBuilder sb = new StringBuilder();
        while (i >=0 || j >= 0) {
            int n1 = i >= 0 ? num1.charAt(i) - '0' : 0;
            int n2 = j >= 0 ? num2.charAt(j) - '0' : 0;
            int sum = n1 + n2 + (hasUp ? 1 : 0);
            if (sum >= 10) {
                sb.insert(0, Integer.toString(sum - 10));
                hasUp = true;
            } else {
                sb.insert(0, Integer.toString(sum));
                hasUp = false;
            }
            i--;
            j--;
        }
        if (hasUp) sb.insert(0, "1");
        return sb.toString();
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="107. Binary Tree Level Order Traversal II"/>107. Binary Tree Level Order Traversal II
### 问题：
> Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

> For example:
Given binary tree [3,9,20,null,null,15,7],
>>    3
>>   / \
>>  9  20
　 	 /  \
　   15   7
    
> return its bottom-up level order traversal as:
>>[
　  [15,7],
　  [9,20],
　  [3]
]

### 大意：
> 给出一个二叉树，返回从下到上的节点值序列。（比如，从左到右，一层层地从叶子到根）。

> 例子：
> 给出二叉树 [3,9,20,null,null,15,7]，

![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/107Image1.png)
    
> 返回从下到上的层级序列为:

![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/107Image2.png)

### 思路：
这道题比较麻烦，要遍历二叉树，返回反过来顺序的二阶List。有两种方法，也就是经常说到的DFS深度优先遍历和BFS广度优先遍历。

BFS：
广度优先遍历就是一层层地攻略过去，把每一层的所有节点都记录下来再走向下一层。因为每层会有多个节点，不是简单的一个左节点一个右节点的，所以这里用到队列，用队列的先进先出特性来记录每一层的节点，保证对每层的每个节点都处理到其子节点，并将值记录下来。队列用到Queue这个类，offer方法可以添加一个元素，peek方法获取队首的元素，poll方法会从队首移除一个元素并获取它。

DFS：
深度优先遍历一般用递归来实现，也就是对每个方向都用递归来找到最底层的叶子节点，一层层处理回来，把每层的节点值添加到当前层的List中去。

### 代码：
BFS：

```java
public class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        List<List<Integer>> wrapList = new LinkedList<List<Integer>>();
        
        if(root == null) return wrapList;
        
        queue.offer(root);
        while(!queue.isEmpty()){
            int levelNum = queue.size();
            List<Integer> subList = new LinkedList<Integer>();
            for(int i=0; i<levelNum; i++) {
                if(queue.peek().left != null) queue.offer(queue.peek().left);
                if(queue.peek().right != null) queue.offer(queue.peek().right);
                subList.add(queue.poll().val);
            }
            wrapList.add(0, subList);
        }
        return wrapList;
    }
}
```

DFS：

```java
public class Solution {
        public List<List<Integer>> levelOrderBottom(TreeNode root) {
            List<List<Integer>> wrapList = new LinkedList<List<Integer>>();
            levelMaker(wrapList, root, 0);
            return wrapList;
        }
        
        public void levelMaker(List<List<Integer>> list, TreeNode root, int level) {
            if(root == null) return;
            if(level >= list.size()) {
                list.add(0, new LinkedList<Integer>());
            }
            levelMaker(list, root.left, level+1);
            levelMaker(list, root.right, level+1);
            list.get(list.size()-level-1).add(root.val);
        }
    }
```


[回到目录](#Catalogue)

-------------------------

## <a name="141. Linked List Cycle"/>141. Linked List Cycle
### 问题：
> Given a linked list, determine if it has a cycle in it.

> Follow up:
Can you solve it without using extra space?

### 大意：
> 给出一个链表，判断它有没有回环。

> 进阶：
> 你能不能不用额外的空间来解决？

### 思路：
这道题我利用Java中Set集合的特性，即集合中不允许出现相同的对象。

我们遍历链表，边遍历边把每个节点放入一个Set集合中，并且每次都判断Set集合内对象的个数是否增加了，如果没增加，说明有相同的对象加入，也就是有回环了。

我看别人的解决办法，很多都是判断相邻的节点间有没有回环，其实不太理解，是不是回环只有相邻的这种情况呢，那如果存在大回环不是就判断不出来了么，还是觉得Set的方法比较保险。

### 代码（Java）：

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) return false;
        HashSet list = new HashSet();
        list.add(head);
        int num = 1;
        while (head.next != null) {
            list.add(head.next);
            num++;
            if (num > list.size()) return true;
            head = head.next;
        }
        return false;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="66. Plus One"/>66. Plus One
### 问题：
> Given a non-negative number represented as an array of digits, plus one to the number.

> The digits are stored such that the most significant digit is at the head of the list.

### 大意：
> 给出一个非负数的代表数字的数组，给这个“数字”加一。

> 这个数字的存储形式为最高位的数再数组的最前端。

### 思路：
但看题目还看不懂是什么意思，跑了几个测试用例后看答案看明白了，就是数组的每一个位置代表一个数的每一位，有个位十位百位等，如[8]表示数字8，[1，2]表示数字12等等，题目要求将给出的数字代表的数字加一并用同样的形式返回结果。

这个题目的要点在于对加法进位的判断，从个位数开始，如果加一后等于10，那么就要进位，而进位时也要不断对高位进行判断是否还要进位，所以只要把这个逻辑理清楚，代码还是好写出来的，我自己写出来的代码很复杂，明显可以进行优化。

后来看了下别人写的代码，思路差不多，也是判断进位，但是代码精简了许多，从最低位开始，如果不进位就直接返回，否则就按照要进位的方式去一遍遍循环，简单明了多了。

### 代码（Java）：

```java
public class Solution {
    public int[] plusOne(int[] digits) {
        int length = digits.length;
        int last = digits[length-1];
        last++;
        if (last < 10) {
            digits[length-1] = last;
        } else {// 最后一位要进位
            digits[length-1] = 0;// 最后一位记得置零
            int position = length-1;
            while (position >= 0) {
                if (position == 0) {// 只有一个数
                    // 在第0位插入一个数
                    int[] newDigits = new int[length+1];
                    newDigits[0] = 1;
                    for (int i = 0; i < length; i++) {
                        newDigits[i+1] = digits[i];
                    }
                    digits = newDigits;
                    break;
                } else {// 有多位数
                    position--;
                    int num = digits[position]+1;
                    if (num < 10) {
                        digits[position] = num;
                        break;
                    } else {// 要进位，置零后继续循环
                        digits[position] = 0;
                    }
                }
            }
        }
        return digits;
    }
}
```

### 他山之石：

```java
public int[] plusOne(int[] digits) {
        
    int n = digits.length;
    for(int i=n-1; i>=0; i--) {
        if(digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        
        digits[i] = 0;
    }
    
    int[] newNumber = new int [n+1];
    newNumber[0] = 1;
    
    return newNumber;
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="27. Remove Element"/>27. Remove Element
### 问题：
> Given an array and a value, remove all instances of that value in place and return the new length.

> Do not allocate extra space for another array, you must do this in place with constant memory.

> The order of elements can be changed. It doesn't matter what you leave beyond the new length.

### 大意：
> 给出一个数组和一个数，移除数组中所有等于该数的值并返回新长度。

> 不要使用额外的空间来创建另一个数组，你必须在恒定的内存中做。

> 元素的顺序可以改变。新长度以外的内容无所谓是什么样子。

### 思路：
这道题的要求在于不创建新数组，而是在原有的数组内容来进行操作，按题目的意思就是将所有不等于那个值的数放到数组前面，然后返回这些数的数量，也就是数组的一个长度，这个长度后面的数是什么样子的都没有关系。

按照这个思路很明显就是检测如果不一样就放到前面来了。我们弄两个指针，一个遍历数组中的数，一个记录不一样的数的数量，那么记录数量的数一定是小于等于遍历的那个指针数的，所以每当遍历到不一样的数时，就放在数组中记录不一样的数的位置，因为第二个指针一定是不会大于第一个数的，所以不会存在覆盖一些没遍历到的数的问题，这相当于是把不一样的数都集中到数组前面了，等遍历完了，后面的数其实还是保持原样的，跟题目要求的很契合。

### 代码（Java）：

```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        int position = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[position] = nums[i];
                position++;
            }
        }
        return position;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="101. Symmetric Tree"/>101. Symmetric Tree
### 问题：
> Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

> For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

>>![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/101Image1.png)

> But the following [1,2,2,null,3,null,3] is not:

>>![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/101Image2.png)

>Note:
Bonus points if you could solve it both recursively and iteratively.

### 大意：
> 给出一个二叉树，检查它是否是自己的镜像（中心对称）。

> 比如，二进制数 [1,2,2,3,4,4,3] 是对称的

>>![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/101Image1.png)

>但 [1,2,2,null,3,null,3] 就不是：

>>![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/101Image2.png)

> 注意：
> 如果可以用递归和迭代来做会加分

### 思路：
这道题我没想出来，总觉得要递归地去比较中间那么多数字是不是对称的不好做到，看了看别人的做法，还是很简单的，只能怪自己没想明白，想得太复杂了。

先检查root啊、左右子节点啊是不是null这些情况直接作出判断，然后用递归去做，每次检查一个节点的左子节点的左子节点和右子节点的右子节点以及左子节点的右子节点和右子节点的左子节点是不是一样的，就可以判断了。听起来有点绕，其实想一想就能明白了，我们总是去对一个节点的左右两个子节点去往下比较，这样就会越往下比较的越开，并不会出现单纯的相邻节点之间进行比较而已。

### 他山之石：

```java
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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        else return isMirror(root.left, root.right);
    }
    
    public boolean isMirror(TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;
        else if (left == null || right == null) return false;
        else return (left.val == right.val) && isMirror(left.left, right.right) && isMirror(left.right, right.left);
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="118. Pascal's Triangle"/>118. Pascal's Triangle
### 问题：
> Given numRows, generate the first numRows of Pascal's triangle.

> For example, given numRows = 5,
Return

>> ![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/118Image1.png)

### 大意：
> 给出一个行数，生出对应行数的杨辉三角形。

> 比如，给出行数 = 5。
> 返回

>> ![](https://github.com/Cloudox/LeetCode-Record/blob/master/Image/118Image1.png)

### 思路：
杨辉三角形好像是小学还是初中学的东西，像上面例子中显示的一样，每行数字递增1，,第一个数和最后一个数都是1，中间的每个数都是上一行对应位置和前一个位置的数之和。

这道题就是要根据给出的行数返回对应的杨辉三角形，那么也可以依据这个特性来做。每一行第一个数和最后一个数肯定都是1，中间的数根据上一行来计算，所以需要保存和更新每一个“上一行”，本行中间 j 位置的数，是上一行 j 位置和 j-1位置的数之和，这样一个个数，一行行计算出来就可以了。这道题要求结果放在ArrayList里，ArrayList经常用到，还是需要了解一下增删改查的用法。

### 代码（Java）：

```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        if (numRows == 0) return new ArrayList<List<Integer>>();
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> lastArr = new ArrayList<Integer>();
        lastArr.add(1);
        result.add(lastArr);
        for (int i = 1; i < numRows; i++) {
            List<Integer> newArr = new ArrayList<Integer>();
            newArr.add(1);
            for (int j = 1; j < i; j++) {
                newArr.add(lastArr.get(j-1) + lastArr.get(j));
            }
            newArr.add(1);
            result.add(newArr);
            lastArr = newArr;
        }
        return result;
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="102. Binary Tree Level Order Traversal"/>102. Binary Tree Level Order Traversal
### 问题：
> Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

> For example:
Given binary tree [3,9,20,null,null,15,7],
>>    3
>>   / \
>>  9  20
　 	 /  \
　   15   7
    
> return its level order traversal as:
>>[
　  [3],
　  [9,20],
　  [15,7]
]

### 大意：
> 给出一个二叉树，返回层级顺序的节点值（从左到右，一层层的）。

> 例子：
> 给出二叉树 [3,9,20,null,null,15,7]。
>>    3
>>   / \
>>  9  20
　 	 /  \
　   15   7

> 返回他的层级顺序为：
>>[
　  [3],
　  [9,20],
　  [15,7]
]

### 思路：
这道题和[LeetCode笔记：107. Binary Tree Level Order Traversal II](http://blog.csdn.net/cloudox_/article/details/52785627)是姊妹题，解题思路都是一样的，只是结果要求的顺序是反的，同样有两种方法，也就是经常说到的DFS深度优先遍历和BFS广度优先遍历。

BFS： 
广度优先遍历就是一层层地攻略过去，把每一层的所有节点都记录下来再走向下一层。因为每层会有多个节点，不是简单的一个左节点一个右节点的，所以这里用到队列，用队列的先进先出特性来记录每一层的节点，保证对每层的每个节点都处理到其子节点，并将值记录下来。队列用到Queue这个类，offer方法可以添加一个元素，peek方法获取队首的元素，poll方法会从队首移除一个元素并获取它。

DFS： 
深度优先遍历一般用递归来实现，也就是对每个方向都用递归来往下找子节点，先用一个空的List占个位置，这一层每找到一个都添加到这个位置的List中去，一直找到最底层为止。

这个题目里BFS会比DFS快一点点。

### 代码（Java）：
BFS：

```java
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        
        if (root == null) return result;
        
        queue.offer(root);
        while (!queue.isEmpty()) {
            int levelNum = queue.size();
            List<Integer> subList = new LinkedList<Integer>();
            for (int i = 0; i < levelNum; i++) {
                if (queue.peek().left != null) queue.offer(queue.peek().left);
                if (queue.peek().right != null) queue.offer(queue.peek().right);
                subList.add(queue.poll().val);
            }
            result.add(subList);
        }
        
        return result;
    }
}
```

DFS：

```java
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        levelMaker(result, root, 0);
        return result;
    }
    
    public void levelMaker(List<List<Integer>> list, TreeNode root, int level) {
        if (root == null) return;
        if (level >= list.size()) {
            list.add(level, new LinkedList<Integer>());
        }
        levelMaker(list, root.left, level+1);
        levelMaker(list, root.right, level+1);
        list.get(level).add(root.val);
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="110. Balanced Binary Tree"/>110. Balanced Binary Tree
### 问题：
> 
Given a binary tree, determine if it is height-balanced.

> For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

### 大意：
> 给出一个二叉树，判断它高度是不是平衡的。

> 对于这个问题，一个高度平衡的二叉树是指每个节点的两个子节点的深度的差异都不超过1的二叉树。

### 思路：
这道题题目说的太简略了也没有例子，根据不断试错摸出来的情况，就是说每个节点的两个子节点的深度不能想查大于1，比如左子节点下还有子节点，右子节点下没有了，这是允许的，深度相差1，但是如果左子节点的子节点还有子节点，深度相差就是2了，就不平衡了。

如果直接判断有无子节点，情况太多了不好做。不如直接递归记录每个节点的深度，然后比较每个节点的两个子节点的深度相差是否大于1。

这里要记录每个子节点的深度可以用递归的方法，叶子节点的深度为1，往上递增，注意在递归算一个节点深度时，要判断左子节点和右子节点的深度哪个更深，取更深的那一个，也就是数值更大的那一个。

然后可以再判断每个节点的左右子节点的深度相差是否大于1。但是要重新遍历一遍所有节点，这无疑增加了时间。在上面我们计算每个节点的深度的时候，有一步是判断左右子节点哪个节点更深，这里明显可以直接比较相差是否大于1，如果大于1，我们将该节点的深度特殊记为-1这个不会出现的深度值，我们希望可以传递到最顶层去告诉题目这个二叉树是不平衡的，因此在计算每个节点的左右子节点的时候，需要判断左右子节点的深度有没有等于-1的，如果有，说明下面有个地方出现不平衡了，这时候直接把-1这个信号往上传就好了。这样一层层递归传回root，就可以根据根节点的深度是否是-1来判断是否平衡了。

### 代码（Java）：

```java
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
    public boolean isBalanced(TreeNode root) {
        if (height(root) == -1) return false;
        else return true;
    }
    
    public int height(TreeNode root) {
        if (root == null) return 0;
        else {
            int leftHeight = height(root.left);
            if (leftHeight == -1) return -1;
            int rightHeight = height(root.right);
            if (rightHeight == -1) return -1;
            if (leftHeight - rightHeight > 1 || leftHeight - rightHeight < -1) return -1;
            return Math.max(height(root.left), height(root.right)) + 1;
        }
    }
}
```

[回到目录](#Catalogue)

-------------------------

## <a name="26. Remove Duplicates from Sorted Array"/>26. Remove Duplicates from Sorted Array
### 问题：
> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

> Do not allocate extra space for another array, you must do this in place with constant memory.

> For example,
Given input array nums = [1,1,2],

> Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

### 大意：
> 给出一个有序数组，移除重复的数字，让每个元素只出现一次，并返回新的长度。

> 不要分配额外的空间给另一个数组，你必须在固定的内存下去做。

> 举例：
> 给出输入的数组为 nums = [1,1,2]，

> 你的函数应该返回长度 = 2，并让前面两个数字为单独的1和2。在新长度之外的位置无所谓你留下了什么内容。

### 思路：
这道题和[LeetCode笔记：27. Remove Element](http://blog.csdn.net/cloudox_/article/details/52856469)这个很类似，只不过这道题的难度在于，在操作中不能随意改变数组中原本元素的位置，因为你要保持它后面的数字还是有序的，才好去比较相邻的数字是否一样。其实也简单，我们弄一个变量记录上一个单独的数字，再弄一个变量记录该数字后面的位置序号，往后遍历，直到遇到不一样的数字，才把那个数字放到该位置序号来，然后把记录单独数字的变量设为这个新数字，记录位置的变量序号+1，继续往后遍历，因为是随着遍历过程往前放数字，所以不会影响到后面的数字顺序。

### 代码（Java）：

```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int position = 1;
        int lastNumber = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > lastNumber) {
                nums[position] = nums[i];
                position++;
                lastNumber = nums[i];
            }
        }
        return position;
    }
}
```

[回到目录](#Catalogue)

-------------------------

不断更新中...

更多内容查看[我的博客](http://blog.csdn.net/column/details/cloudox-column2.html)
