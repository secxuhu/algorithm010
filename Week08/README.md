# Table of Contents

- [Table of Contents](#table-of-contents)
  - [第 8 周](#第-8-周)
    - [第 16 课 | 位运算](#第-16-课--位运算)
      - [位运算基础及实战要点](#位运算基础及实战要点)
        - [XOR - 异或](#xor---异或)
        - [指定位置的位运算](#指定位置的位运算)
        - [实战位运算要点](#实战位运算要点)
        - [参考链接](#参考链接)
      - [实战题目](#实战题目)
    - [第 17 课 | 布隆过滤器和 LRU 缓存](#第-17-课--布隆过滤器和-lru-缓存)
    - [第 18 课 | 排序算法](#第-18-课--排序算法)
      - [初级排序和高级排序的实现和特性](#初级排序和高级排序的实现和特性)
        - [基础](#基础)
        - [初级排序 - O(n²)](#初级排序---on²)
        - [高级排序 - O(N \* logN)](#高级排序---on--logn)
        - [特殊排序 - O(n)](#特殊排序---on)
        - [参考链接](#参考链接-1)
    - [作业](#作业)
      - [简单](#简单)
      - [中等](#中等)
      - [困难](#困难)
    - [下周预习](#下周预习)
      - [预习题](#预习题)

## 第 8 周

### 第 16 课 | 位运算

#### 位运算基础及实战要点

##### XOR - 异或

- 异或：相同为 0，不同为 1。也可用 `不进位加法` 来理解
- 异或操作的一些特点：

  ```Python
  x ^ 0 = x
  x ^ 1s = ~x
  x ^ (~x) = 1s  # 注意 1s = ~0
  x ^ x = 0
  c = a ^ b  # a ^ c = b, b ^ c = a 交换两个数
  a ^ b ^ c = a ^ (b ^ c) = (a ^ b) ^ c  # associative
  ```

##### 指定位置的位运算

1. 将 x 最右边的 n 位清零：`x & (~0 << n)`
2. 获取 x 的第 n 位值(0 或者 1)：`(x >> n) & 1`
3. 获取 x 的第 n 位的幂值：`x & (1 << n)`
4. 仅将第 n 位置为 1：`x | (1 << n)`
5. 仅将第 n 位置为 0：`x & (~(1 << n))`
6. 将 x 最高位至第 n 位(含)清零：`x & ((1 << n) - 1)`
7. 将第 n 位至第 0 位(含)清零：`x & (~((1 << (n + 1)) - 1))`

##### 实战位运算要点

- 判断奇偶
  - `x % 2 == 1` —> `(x & 1) == 1`
  - `x % 2 == 0` —> `(x & 1) == 0`
- `x >> 1—> x / 2`，即: `x = x / 2`；—> `x = x >> 1`; `mid = ( left + right) / 2`；—> `mid = (left + right) >> 1`;
- `x = x & (x - 1)` 清零最低位的 1
- `x & -x` => 得到最低位的 1
- `x & ~x` => 0

##### 参考链接

- [如何从十进制转换为二进制](https://zh.wikihow.com/%E4%BB%8E%E5%8D%81%E8%BF%9B%E5%88%B6%E8%BD%AC%E6%8D%A2%E4%B8%BA%E4%BA%8C%E8%BF%9B%E5%88%B6)
- [N 皇后位运算代码示例](https://shimo.im/docs/YzWa5ZZrZPYWahK2)

#### 实战题目

### 第 17 课 | 布隆过滤器和 LRU 缓存

### 第 18 课 | 排序算法

#### 初级排序和高级排序的实现和特性

##### 基础

- 排序算法
  1. 比较类排序
     - 通过比较来决定元素见的相对次序，由于其时间复杂度不能突破 O(nlogn)，因此也称为非线性时间比较类排序
  2. 非比较类排序
     - 不通过比较来决定元素间的相对次序，它可以突破基于比较排序的时间下界，以线性时间运行，因此也称为线性时间非比较类排序

##### 初级排序 - O(n²)

1. 选择排序（Selection Sort）：每次找最小值，然后放到待排序数组的起始位置
2. 插入排序（Insertion Sort）：从前到后逐步构建有序序列；对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入
3. 冒泡排序（Bubble Sort）：嵌套循环，每次查看相邻的元素如果逆序，则交换

##### 高级排序 - O(N \* logN)

1. 快速排序（Quick Sort）：数组取标杆 pivot，将小元素放在 pivot 左边，大元素放右侧，然后依次对右边和右边的子数组继续快排；已达到整个序列有序
2. 归并排序（Merge Sort）- 分治
   1. 把长度为 n 的输入序列分成两个长度 n/2 的子序列
   2. 对这两个子序列分别采用归并排序
   3. 将两个排序好的子序列合并成一个最终的排序序列
3. 堆排序（Heap Sort） - 堆插入 O(logN)，取 最大/最小 O(1)
   1. 数组元素依次建立小顶堆
   2. 依次取顶堆元素，并删除

- 总结：归并 和 快排具有相似性，但步骤顺序相反
  1.  归并：先排序左右子数组，然后合并两个有序的子数组
  2.  快排：先调配出左右子数组，然后对于左右子数组进行排序

##### 特殊排序 - O(n)

1. 计数排序（Counting Sort）： 计数排序要求输入的数据必须是有确定范围的整数。将输入的数据值转化为键存储在额外开辟的数组空间中；然后依次把计数大于 1 的填充回原数组
2. 桶排序（Bucket Sort）：桶排序的工作原理，假设输入数据服从均匀分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或者递归方式继续使用桶排序进行排）
3. 基数排序（Radix Sort）：基数排序是按照低位先排序，然后收集；再按照高位排序，然后再收集；依次类推，直到最高位。有时候有些属性是有优先级顺序的，先按低优先级排序，再按高优先级排序

##### 参考链接

- [十大经典排序算法](https://www.cnblogs.com/onepixel/p/7674659.html)
- [快速排序代码示例](https://shimo.im/docs/TX9bDbSC7C0CR5XO)
- [归并排序代码示例](https://shimo.im/docs/sDXxjjiKf3gLVVAU)
- [堆排序代码示例](https://shimo.im/docs/M2xfacKvwzAykhz6)
- [9 种经典排序算法可视化动画](https://www.bilibili.com/video/av25136272)
- [6 分钟看完 15 种排序算法动画展示](https://www.bilibili.com/video/av63851336)

### 作业

#### 简单

1. [位 1 的个数](https://leetcode-cn.com/problems/number-of-1-bits/)

   ```Python
   class Solution:
       def hammingWeight(self, n: int) -> int:
           # 位运算
           ans = 0
           while n:
               n = n & (n - 1)
               ans += 1
           return ans

       def hammingWeight(self, n: int) -> int:
           # 暴力求解，O(n)
           ans = 0
           for i in bin(n):
               if i != 1: continue
               ans += 1
           return ans
           # return bin(n).count('1') # 内置方法求解
   ```

2. [2 的幂](https://leetcode-cn.com/problems/power-of-two/)

   ```Python
   class Solution:
       def isPowerOfTwo(self, n: int) -> bool:
           # 暴力求解
           ans = 1
           while ans < n:
               ans <<= 1
           return ans == n

       def isPowerOfTwo(self, n: int) -> bool:
           # 位运算：获取二进制中最右边的 1
           if n == 0:
               return False
           return n & -n == n
   ```

3. [颠倒二进制位](https://leetcode-cn.com/problems/reverse-bits/)
4. 用自己熟悉的编程语言，手写各种初级排序代码，提交到学习总结中
5. [数组的相对排序](https://leetcode-cn.com/problems/relative-sort-array/)
6. [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)

#### 中等

1. [LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/#/)
2. [力扣排行榜](https://leetcode-cn.com/problems/lru-cache/#/)
3. [合并区间](https://leetcode-cn.com/problems/merge-intervals/)

#### 困难

1. [N 皇后](https://leetcode-cn.com/problems/n-queens/description/)
2. [N 皇后 II ](https://leetcode-cn.com/problems/n-queens-ii/description/)
3. [翻转对](https://leetcode-cn.com/problems/reverse-pairs/)

### 下周预习

#### 预习题

1. [不同路径](http://leetcode-cn.com/problems/unique-paths/)
2. [最小路径和](http://leetcode-cn.com/problems/minimum-path-sum/)
