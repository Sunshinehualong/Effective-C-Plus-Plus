
# 数据结构部分  

## 最基本的线性结构 序列(sequence)

- 向量 vector 逻辑次序与物理存储次序完全吻合  
- 列表 list   逻辑上相邻，物理上未必相邻  

### 动态数组 vector的实现
- 对于元素的访问(读取和修改) 在常数时间内完成， A+i*s(访问只需要一次加法和一次乘法运算)  
- 逻辑次序也称为秩 为0-n的正整数
 

> - 构造函数 指定初始容量、申请内存空间、创建模板类型数组
> - 析构函数  释放内存空间
> - **控制可扩充向量的溢出策略**：数据溢出，申请一个更大的数组(2倍)，原数据集体搬迁到新空间，释放原空间
> - [Vector较数组更加灵活，只要系统尚有可用空间，规模不受初始容量限制] 
> - [每次从n到2n,扩容都花费O(n)时间，平摊时间为O(1),装载因子总是在高于50%，又不超过100%，size(n)<capacity(n)<2∙size(n)]
> - [单次操作的执行速度极其敏感的应用场合以上策略并不适用扩容和缩容，其中缩容操作甚至可以完全不予考虑]
> - 重载 赋值操作符 `=`
> - 重载 直接引用操作符 `[]`  时间复杂度O(1)
> - 置乱器算法  [从末元素开始`V[i-1]`，每次与前V`[0,i)`中某一元素随机交换] 时间复杂度 O(3n) 因为有swap

> - 插入元素 首先考虑是否溢出，然后后面的元素都要右移， 时间复杂度 O(_size-r+1)=O(n) 正比于向量的实际规模
> - 删除，插入的逆操作  删除单个元素是删除区间的特例 _elem[lo++] = _elem[hi++];  时间复杂度O(hi-lo)
> - [因为删除需要整体移动，所以能成片删除就能减少移动，把单个看成区间的特例]

> - [唯一化 剔除重复元素] 
> - 无序的，从首个元素开始，查看是否与其前缀雷同  备份size  调用find remove
> - [每次迭代 find对应于前驱的长度， remove对应于后继的移动，所以一次迭代时间O[n],总的迭代 时间O[n^2]]
> - 有序的低效实例和高效思路差别很大，高效的是直接进行，比较、copy、截断 时间复杂度O[n]

> - 无序查找 从后向前，顺序查找 时间复杂度 O(n)
> - 有序查找 二分查找 O(logn)

> - 排序
> - 冒泡排序，每一趟 肯定能把最大元素筛到最后面 [每一趟相邻的比较，看是否需要交换] 时间复杂度 O(n^2)
> - bubbleSort 是稳定的， 重复元素的相对次序在排序前后保持一致
> - 二路归并 采用[分治策略] (无序向量递归分解，有序向量逐层归并)  最坏最佳平均复杂度均为O(nlogn)
> - [归并 最后一层子问题时间为常数c 有n个所以是cn，总共有logn +1 层，所以时间复杂化度O(nlogn)]
> - [归并排序的计算量主要消耗于有序子向量的归并操作,子向量的划分不费时间]
> - [快速排序 排序可以在O(1)内完成，而将原问题划分成两个子问题需要O(n)] [快排序反复交换，稳定性不足]
> - 随机选一个轴点pivot，不断地迭代，找出它的位置，就可以实现一次轴点划分， 最坏的情况是类似冒泡排序O(n^2), 一般情况O(nlogn)]




> - 中位数查找  K查找
> - [记住，一组元素中 “第k大的元素” 所包含的信息量，远远少于经过全排序后得到的整个有序序列]
> - 两路归并序列的中位数 [找出每一个的中位数，减而治之]  复杂度O(logn)
> - 对于一般无须的一组元素， 使用优先级队列的结构进行K查找
> - [花费O(n)时间将全体元素组织为一个小顶堆, k次delMin()操作, 小顶堆顶即为第k个元素 O(n + klogn)]
> - [任取k个元素，并在O(k)时间以内将其组织为大顶堆, 将剩余的n-k个元素逐个插入堆中；每插入一个，随即删除堆顶 O(k + 2(n - k)logk)]
> - [分两组，构建一个K个元素大顶堆和(n-k)元素的小顶堆]
> - 当K趋于 n/2时，复杂度退化为 蛮力算法的O(nlogn)

### List vector的实现

- vector 是逻辑上和物理上都是对应的， 所谓[call by rank]  静态特性好，索引
- List 元素逻辑上线性次序，物理地址可以任意，所谓[call by link/position] 动态特性好(插入/删除) 

> 链表 linkedList是一种典型的动态存储结构， 数据分散为一系列的节点，节点间通过指针相互索引， 插入删除只调整局部少量指针， 大大降低了动态操作的成本
> 首尾添加哨兵节点，使得list内 任意一个Node都有前驱和后继

> - [初始化过程] 设置哨兵节点， 设置前驱后继的双向链表指向，设定size
> - [静态索引 时间复杂度O(r+1)] 从首节点依次查找 Rank为r的node
> - [静态无序查找 时间复杂度O(n)] find(e,p,n) 在无序列表内节点p的n个前驱中，找到值为e的最后者，从后往前一个一个查找

> - [双向链表的插入 O(1)] 在ListNode中实现，断开原来的两个指向，新增四个指向，在创建Node会先指定两个
> - 插入节点，size+1 只影响局部的指向，所以动态特性好
> - 基于复制的构造，先构造一个空链表，然后不断使用插入构造

> - [双向列表的删除 O(1)] 只要将要调整的节点的前驱和后继的指向重新调整一下(p前驱的后继、 后继的前驱)
> 清空列表， 反复remove 首节点
> - [列表的唯一化] 同向量的思路一样 find remove
> 无序去重 [O(n^2)]：查找与所有前驱中是否重复，remove, 每次positon向后移动一个
> 有序去重 [O(n)]: 相邻对pq, q为p的succ, 比较数值，相同的删除

> [List 排序]
> - [插入排序 O(n^2)] 每次查找前缀中对用位置，插入， 完全有序也需要O(n),逆序要O(n^2)
> - [选择排序 O(n^2)] 无序前缀和有序后缀，每次选择前缀最大者，插入后缀, 如果selectMax能够到O(logn)就快了
> - [列表的二路归并排序 O(nlogn)] 


### 栈与队列

-  相对于向量和列表，栈与队列的外部接口更为简化和紧凑，故亦可视作向量与列表的特例
- Stack 后进先出的，逆序输出
- Queue 先进先出的，正序输出

> 栈的接口很紧凑 只有 size() empty() push() pop() top()
> 操作系统大多都是采用`栈`来实现函数(递归)调用的，记录调用与被调用函数(递归)实例之间的关系
> [栈结构适合解决什么问题？  以逆序计算输出的问题]
> 无论是递归还是迭代实现， 该序列都是依逆序计算输出的,
> 输入和输出规模不确定，难以事先确定盛放输出数据的容器大小。
> 因其特有的“后进先出” 特性及其在容量方面的自适应性，使用栈来解决此类问题可谓恰到好处

> 利用栈实现进制转换
> [栈混洗] 从一个栈转移到另一个栈，中间还有一个缓冲栈
> 括号匹配问题

> stack 可以基于Vector 实现，也可以基于List实现
> push pop top 都是操作Vector的尾元素 size()-1 [时间复杂度均为常数]


## 二叉树
- [树 半线性结构]
- 前面基于 Vector List实现的的数据结构都是线性数据结构，有的静态特性好，有的动态特性好
- 而树形结构并不存在天然的直接前驱、后继，只要附加某种约束，也能确定某种线性次序
> **树的基本概念**
> node edge depth(v) v到r所经过边的数目 
> ancestor descendant  parent child degree deg(v)孩子总数 leaf
> subtree(v) height(T)=height(r)所有节点深度的最大值[单节点高度为0，空树高度为-1]  height(v) v子树的高度
> 有序二叉树、真二叉树

> 多叉树的表示： 每个元素保留自己data外，可以保存 parent rank/position, child position
> 根据自己的使用场合，兼顾对父节点和子节点的插入删除,动态地维护和更新树的拓扑结构

> - 用二叉树表示有序多叉树， 使用双指针，一个指向长子(竖)，一个指向下一个兄弟(横)
> 二进制编码 PFC编码树，无歧义编码，[只要所有字符都对应叶节点即可]

### 特殊的二叉树
>斜二叉树   【所有节点都只有左子树或者右子树】 所以说List是二叉树的一种特例  
>满二叉树   【每个分支节点都有左子树和右子树， 所有叶子都在同一层】  
>完全二叉树 【所有节点与同样深度的满二叉树，按层次编号相同】   
满二叉树一定是完全二叉树，完全二叉树不一定是满二叉树  
完全二叉树的特点：叶子节点只能出现在最下两层，同样节点数的二叉树，完全二叉树的深度最小

### 二叉树性质
每一层： 至多有 2^(i-1)个节点 【根节点是第一层】
所有层： 深度为k的二叉树，至多有2^k - 1个节点，至少有k个节点 【根节点深度为1】
所有层： n个节点的完全二叉树，深度为 [log2^n]+1
任意一颗二叉树： n0 = n2 +1, 度为2的节点比叶子节点多一个。




### 二叉树节点 以及 二叉树的实现
-完全二叉树 可以用顺序结构来表示，(一般也只有完全二叉树用数组，其他二叉树用链表)
- 其他二叉树用二叉链表[data lchild rchild]、或者三叉链表[data lchild rchild parent]

- **BinNode** 包含 data parent/lc/rc的位置，节点的高度
> BinNode size(当前节点后代的个数，包括自己) 通过递归的方式得到 s += lc->size();
> insertAsLC/insertAsRC  创建一个BinNode(父节点是this), lc/rc 指向这个 new node
> succ 取得当前节点的直接后继 


- **BinTree** 
> 记录树的规模 根节点位置
> 构造树的时候，_size _root指向NULL 
> 树的[插入]
> 以根节点插入空树 _size=1 _root 指向新节点
> 以LChild/RChild 插入节点： _size++  插入节点 更新祖先高度 返回孩子的位置
> 将一棵树S作为另一颗树节点x的child接入：S的根节指向孩子，x作为父亲指向根， 更新_size height , 释放S
> 树的[删除]
> 子树的删除，首先切断父节点的指针，更新高度、释放子树 removeAt(递归方式，分别释放lc rc的数据和指向)
> 子树的分离，首先切断父节点的指针，更新高度、new一个新树S(根节点是x,_size是x的)
> 二叉树的[遍历]
> 二叉树用图形表示很直观，但是计算机只能用循环、判断等方式处理 线性序列，
所以需要把二叉树转化成某种意义上的线性序列  
> 层次遍历： 一层一层来
  先序遍历： 根左右 
  中序遍历： 左根右
  后序遍历： 左右根


### 图的定义与实现

> 顶点和边   degree(v)与顶点v关联的边数  有向图的入度和出度
> path 通路与环路 (起止顶点相同称为环路) 欧拉环路(经过图中各边一次且恰好一次的环路)[长度等于图中的总边数] 对偶的 哈密尔顿环路(经过图中各顶点一次的环路)
>  含有n个顶点的无向完全图，边的数目 n*(n-1)/2  [两两之间都有边]
>  含有n个顶点的有向完全图，边的数目 n*(n-1)    [两两之间都有双向边]
>  带权图，通常称为网 [比如多个城市距离之间的加权]
>图的时间和空间复杂度 
>输入规模由顶点和边数总和来度量  n个顶点 无向图最多有n(n-1)/2边；有向图最多有n(n-1)条  
> 图的存储： 一个数据域，多个指针域  

> 邻接矩阵方式：所以通过一个一维数组[存储顶点]和一个二维邻接矩阵[存储边]表示一个图   
> 邻接矩阵 主对角线都为零， 矩阵竖轴表示入度，横轴表示出度，不带权的值为1，带权的值为 Wij

> 邻接表方式： 通过一个一维数组[存储顶点]，每一个顶点所有的邻接点构成一个线性表  
> 线性表指向所连接的顶点，带权值的还会加一个权值的数据域

[图的遍历]  
- 深度优先遍历(depth first search) 类似于树的先序遍历
- 广度优先遍历(breadth first search) 类似于树的层次遍历

[最小生成树问题 - 构建联通网的最小代价生成树] 
- prim算法
- kruskal算法
 

