<!-- ex_nolevel -->
# 双指针
用到两个指针的算法都可以叫作two pointers，但通常是条件判断控制指针移动而不是双层for循环，其中两个指针向同一个方向移动且先后不变的都可以叫sliding window滑动窗口 。

## sliding window protocol
关于滑动窗口协议，[这篇文章](https://zhuanlan.zhihu.com/p/133307545)写得很好（已经传到[github](https://github.com/V2beach/books/blob/main/TCP%20重传、滑动窗口、流量控制、拥塞控制%20-%20知乎.pdf)以防链接失效），读维基读得很懵，中文维基只在TCP(OSI layer 4 transport layer)里提过，但其实其在data link layer (OSI layer 2)亦有应用。

![diagram1](/assets/unnamed-2.png)

![diagram2](/assets/unnamed.png)

滑动窗口在网络中用来控制连续传输数据而不需要确认ACK(acknowledgment)的最大长度，顾名思义，如果在传完窗口size的数据前提前收到了ACK，那窗口就会滑动，限定新的最大传输范围。

其实这个协议也可以看成是双指针算法，SND.UNA和SND.NXT。(可传输的窗口大小 = SND.WND -（SND.NXT - SND.UNA）)

![window](/assets/v2-0b51bf628f6031dea5e88ff5abca8d22_1440w.webp)

>当收到之前发送的数据 32~36 字节的 ACK 确认应答后，如果发送窗口的大小没有变化，则滑动窗口往右边移动 5 个字节，因为有 5 个字节的数据被应答确认，接下来 52~56 字节又变成了可用窗口，那么后续也就可以发送 52~56 这 5 个字节的数据了。

![sliding](/assets/v2-609be3306d058eafc9a45c89adb21840_1440w.webp)

## 快慢指针
顾名思义指针一慢一快，是很巧妙的判断链表中环的算法，若有环在可接受的时间内两指针一定相遇。  
https://leetcode.com/problems/linked-list-cycle-ii

## 双指针解决triplet的问题
pair(2-tuple)的问题是自然而然的，triplet(3-tuple)最直接的自然是三层循环O(n^3)，但可以确定一个对另外两个当tuple用two pointers。

为什么能提速？brutal的特点是几层for指针从头部遍历到尾，twopointers特点是while循环按判断结果移动指针。

那么更多呢？quater(4-tuple)怎么办？更多的(5/6/7-tuple)呢？

while代替if

跟binary search一样，一般是有序序列？

two pointers相向或反向要灵活判断，3sum就是反向。

关于“quater(4-tuple)怎么办？”——

Given an integer array nums, return all the quaters [nums[i], nums[j], nums[k], nums[x]] such that i != j, i != k, and j != k, i != x, j != x, k != x, and , and nums[i] + nums[j] + nums[k] + nums[x]== 0.

Notice that the solution set must not contain duplicate quaters.
code it in c++

chatgpt的做法是两层for循环套two pointers