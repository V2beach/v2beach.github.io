c++里就是用map和set，不是自己写。

但是关于这些STL里container的原理，需要读读看[Effective STL](https://github.com/V2beach/books/blob/main/effective%20stl.pdf)。

一个语法：`map[key] = value`会自动对象，举两个例子——`map["int"] += 1`，这个`map<string, int>`就算没有对应键也会初始化int值为0；`map["vector"].push_back(1)`，这个`map<string, vector<int>>`就算没有对应键也会初始化空vector。

排列组合用英文学一遍，记公式。  
不要觉得写代码就不用公式，最需要公式（142公式推导很巧妙、精彩、经典）！比如图形学里最基本算个两点距离就是公式  
矩阵遍历方法https://github.com/wisdompeak/LeetCode/tree/master/Binary_Search/378.Kth-Smallest-Element-in-a-Sorted-Matrix  
等差等比级数公式  

930 sliding window + hashtable prefixsum，这题让我脑子很乱，证明这两类题还没刷够。