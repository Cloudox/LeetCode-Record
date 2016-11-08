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

不断更新中...

更多内容查看[我的博客](http://blog.csdn.net/column/details/cloudox-column2.html)
