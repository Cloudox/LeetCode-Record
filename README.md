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

不断更新中...

更多内容查看[我的博客](http://blog.csdn.net/column/details/cloudox-column2.html)
