# Ch2




## 2*

> 一棵树T有 $ n_i $ 个 度数为 $ i $ 的顶点， $ i = 2,3, \dots , k$  , 其余顶点都是树叶，则T有几片树叶？

由图的性质有：
$$
2 \epsilon(T) = \sum_{i=1}^{k} in_i
$$
由树的性质有：
$$
\epsilon(T) = v(T)-1 =  \sum_{i=1}^{k} n_i -1
$$
上面两个式子联立可得：
$$
n_1 =  \sum_{i=2}^{k}(i-2)n_i +2
$$




## 4*

> 证明：如果T是树，且 $ \Delta(T) \geq n$，则T至少有n片树叶

由2.2题的结论我可以可以得到：
$$
n_1 =  \sum_{i=2}^{k}(i-2)n_i +2  \geq (\Delta(T)-2)*1 +2 = \Delta(T) \geq n
$$
得证





## 6*

> 证明：树有一个中心或两个中心，且有两个中心时，这两个中心相邻

### 方法一

可以使用删除叶子节点的方法，即证明删除$T$中所有叶子结点后，新树$T'$的中心不变。

对于  $\forall v \in V(T)$，如果要使$d(u,v)$最大，v显然是叶子。那么删除所有 $T$中叶子结点后，必然有：
$$
max_{\forall v \in V(T')}d(u,v) = max_{\forall v \in V(G)}d(u,v)-1
$$


所以u仍为$T'$的中心。

重复执行上述操作，最后只能得到$K_1，K_2$这两种情况，即一个顶点或者两个相邻顶点，得证。



### 方法二

可以用最长轨法证明最长轨的中点为树的中心。



## 11*

> 求 $K_{2,3}$生成树的个数

![Ch2_11](./images/Ch2_11.png)



## 14*

> 用Kruskal算法求图中边权图最小的生成树

![Ch2-14](/Users/sakura/USTC_Graph_Theory/homework/images/Ch2-14.png)



Kruskal的算法是有限选择边权较小的边，选择的顺序是和Prim算法不一样的是，如下图所示，红色标记的是最小生成树，序号则是顺序。

![Ch2-14-2](/Users/sakura/USTC_Graph_Theory/homework/images/Ch2-14-2.png)






## 15*

> 边权图里的最小生成森林是权最小的生成森林，并且在生成森林中 保持原图中任意两个顶点的连通性。如何修改 Kruskal 算法来构造最小 生成森林，并指出时间复杂度。

**Kruskal算法 ** ：

- 输入：加权图$G = (V(G),E(G),\omega), v=|V(G)|$
- 输出：G的一棵生成树的边子集${e1,e2,\dots,e_{v-1}}$

**过程如下**：

1. 从E$(G)$中选权最小的边$e_1$;
2. 若已经选定边$e_1,e_2,\dots,e_i$，则从$E(G)-{}{e_1,e_2,\dots,e_i}$中选取边$e_{i+1}$，使得
   - (i)边导出子图$G[\{e_1,e_2,\dots,e_i\}]$不含圈；
   - (ii)在满足(i)的前提下，$\omega(e_{i+1})$的权最小，即$\omega(e_{i+1})= min_{e \in E(G)-\{e_1,e_2,\dots,e_i\}}\omega(e)$
3. 反复执行第(2)步，直到选出$e_{v-1}$为止



下面分类讨论：

1. 如果知道G的连通片数，设为k

   则在各连通片上分别执行原Kruskal算法，时间复杂度为：$O(\sum_{i=1}^k \epsilon_ilog\epsilon_i) = O(\epsilon log  \epsilon)$

2. 如果不知道G的连通片数， 则需修改循环中止条件：

   改为反复执行第(2)步，直到从剩余边集中选出任意一条边都会使边导出子图$G[\{e_1,e_2,\dots,e_i\}]$含圈

   时间复杂度为$O(\epsilon log  \epsilon)$



## 20*

> 画出带权 0.2,0.17,0.13,0.1,0.1,0.08,0.06,0.07,0.03 的 Huffman 树

需要注意的是此题的权重之和并不是1，许多人误以为权重之和必须是1。

![Ch2-20](/Users/sakura/USTC_Graph_Theory/homework/images/Ch2-20.png)







## 22*

> 证明引理2.1 
>
> 给定$\omega_1 \leq\omega_2 \leq \dots \leq\omega_t$，则存在一课Huffman树，使得$\omega1,\omega2$对应的顶点时兄弟，且这两个顶点在二叉树中的深度都等于树高

不妨设$w_i$对应的顶点为$v_i,i=1,2,\dots,t$，假设任意Huffman树中$v_1$中的深度不等于树高，即存在$v_k,2\leq k\leq t$，使得$v_k$的深度等于树高 ，显然有$L(v_k)\geq L(v_1)$。

因为
$$
WPL(T) = w_1L(v_1) + w_2L(v_2) + \dots + w_tL(v_t)
$$
且
$$
w_1 \leq w_2 \leq \dots \leq w_t
$$
交换$v_1,v_k$的位置，得到$T'$ ，则有
$$
\begin{align}
WPL(T')& = w_1L(v_k) + w_2L(v_2) + \dots + w_tL(v_1) \\
 & = WPL(T) + (w_1-w_k)[L(v_k)-L(v_1)]\
\end{align}
$$

1. 当$w_1 = w_k$时，$WPL(T') = WPL(T)$，与树$T'$同为Huffman树；
2. 当$w_1 \lt w_k$时，$WPL(T') \le WPL(T)$，与树$T$为Huffman矛盾；



则$v_1$的深度等于树高，且同理可证得
$$
L(v_1) \geq L(v_2) \geq\dots \geq L(v_t)
$$
若$v_1$无兄弟，则由Huffman树WPL最小规则，$v_1$的深度还可以再缩短直至$v_1$有兄弟。

由$L(v_1) \geq L(v_2) \geq\dots \geq L(v_t)$可得$v_2$为$v_1$的兄弟，则有$\omega1,\omega2$对应的顶点为兄弟，且这两个顶点在二叉树中的深度都等于树高。



## 25

> 证明： 在$v \geq 3$阶的连通图G中 ，存在至少两个顶点，从G中删除这两个顶点后所得图仍为连通。

由推论2.2可知连通图$G$有生成树，记为$T$。

由定理2.2可知树T至少有两片叶，记为$v_1,v_2$。

从$T$中删去$v_1,v_2$得树$T'$显然$T'$仍然连通

从G中删去$v_1,v_2$得到图中$G'$，易知$\forall u_1,u_2 \in V(G'), u_1,u_2 \in V(T')$且存在轨道$p(u_1,u_2) \in E(T') \subseteq E(G')$， 则$G'$ 仍然连通。
