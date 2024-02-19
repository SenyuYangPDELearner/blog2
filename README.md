<style>
.bjimg{
  position: fixed;
  top: 0;
  left: 0;
  width:100%;
height:100%;
min-width: 1000px;
z-index:-10;
zoom: 1;
  background-image: url(https://mathinstitutes.org/uploads/2021/07/images/12424_highlight_40.png);
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center 0;
  opacity: 0.3;
  }
</style>
<head>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>
<div class="bjimg"></div>

# 组合学的多项式方法：有限域Kakeya猜想

Kakeya猜想是目前数学界最重要也是最困难的问题之一，横跨调和分析，加性组合，几何测度论，解析数论等诸多领域，过去五十年里Fefferman, Bourgain, Wolff, Tao, Guth等顶尖学者们为她倾尽心血. Kakeya猜想建立在欧氏空间$\mathbb{R}^n$上，而Wolff在1995年提出离散的有限域版本，以期为原版提供线索. 此后包括Bourgain, Tao等人数学家动用分析，组合和数论中相当艰深的工具做了大量工作，始终与猜想的完全解决隔着一层窗户纸. 人们据此相信，有限域版本和原版的难度相差无几. <br/>

直到2009年，理论计算机科学家[Dvir](https://www.cs.princeton.edu/~zdvir/)的论文[1]横空出世. Dvir仅仅运用简单的线性代数和多项式理论便干净利落地解决了**有限域Kakeya猜想**，震惊了数学界. 论文的核心部分经不断发展形成了所谓的**多项式方法**(polynomial method)，如今成为组合，分析乃至编码理论的重要技术. 这篇博客的主题就是复盘Dvir的绝妙证明(堪称proof from the Book)，一窥多项式方法的思想. <br/>

本文参考了以下文献：<br/>
[1] Zeev Dvir. On the size of Kakeya sets in finite fields. Journal of the American Mathematical Society, 22(4):1093–1097, 2009.<br/>
[2] Larry Guth. Polynomial Methods in Combinatorics. American Mathematical Society, University Lecture Series, vol. 64.

##  Kakeya集和Kakeya猜想

为了叙述Kakeya猜想，我们先介绍Kakeya集(有些文献称为Besicovitch集)的定义.
>**定义1**. $n$维欧式空间$\mathbb{R}^n$的子集$K$称为**Kakeya集**，如果对任意单位向量$x\in \mathbb{R}^n $，存在$y\in \mathbb{R}^n $使得*单位线段*

$$
L_{x,y}=\{y+tx: 0\leq t\leq 1\}\subset K.$$

用人话讲，Kakeya集包含了每个方向的一条单位线段. 显然全空间$\mathbb{R}^n$是一个Kakeya集，那么有更小的Kakeya集吗？直观上Kakeya集不能太稀疏，读者可以自己尝试构造$\mathbb{R}^2$中的一些例子，最简单的是半径1/2 的圆盘. 然而Besicovitch在1920年得到一个惊人的构造：

> **命题2.** $\mathbb{R}^n$中存在体积(测度)为$0$的Kakeya集.

自然Besicovitch的例子有许多怪异的性质，这里我们不会谈及具体的构造(背景图是它的一个近似). 但是从维数上看，“Kakeya集不能太稀疏”似乎成立：Besicovitch例子的Hausdorff维数是$n$(不熟悉Hausdorff维数和分形的读者不必纠结于这个概念，理解有限域版本并不需要它). 于是有

> **Kakeya猜想** $\mathbb{R}^n$中的Kakeya集的Hausdorff维数是$n$.

乍一看这个奇怪的猜想仿佛是数学家为了饭碗生造出来的玩具，但就如文章开头所说，她的深度和广度远超最初的预期，要讲清楚这点可能需要无穷篇博客(笑). <br/>

下面我们引入离散的有限域版本. 从现在开始，$q$是一个正整数，$\mathbb{F}_q$是一个有$q$个元素的有限域，$\mathbb{F}_q^n$是$\mathbb{F}_q$上的$n$维向量空间. 熟悉抽象代数的读者可能知道$q$一定是某个素数的幂并且$\mathbb{F}_q$在同构意义下是唯一的. 不熟悉有限域的读者也不必担心，事实上Dvir的证明仅用到有限域的以下性质：
- $\mathbb{F}_q$元素个数有限, $\vert \mathbb{F}_q^n\vert =q^n$.(这很废话但确实重要)
- 对任意$x\in \mathbb{F}_q $, $qx=0,x^q=x$.(这与实数域很不一样，我们没法除以$q$)
- 如果$v\in F_{q}^n$，存在某个非零的$t\in\mathbb{F}_q$使得$tv=0$，则$v=0$.

第三个性质其实在说尽管有第二个性质，有限域和实数域一样可以做除法，即乘法有逆：
- 对任意*非零*的$a\in\mathbb{F}_q$，存在非零的$b\in\mathbb{F}_q$使得$ab=ba=1$，记$b=a^{-1}$.

读者可以对最简单的有限域——素域$\mathbb{F}_p$($p$是素数)验证上述性质以熟悉有限域的性质：集合$\\{0,1,2,…,p-1\\}$上定义加法为整数加法模$p$，乘法为整数乘法模$p$.

> **定义3.** $\mathbb{R}^n$的子集$K$称为**有限域Kakeya集**，如果对任意$a\in \mathbb{F}\_q^n$，存在$b\in\mathbb{F}_q^n$使得*直线*

$$
L_{a,b}=\{b+ta: t\in \mathbb{F}_q\}\subset K.$$

我们一样可以问：有限域Kakeya集可以多小？

> **有限域Kakeya猜想** 存在只关于$n$的正常数$0\<c_n\<1$，对任意Kakeya集$K\subset \mathbb{F}_q^n$都有

$$
\vert K\vert \geq c_n q^n.$$

现在猜想已经得到证明，所以我们知道有限域Kakeya集确实不能太小(至少包含c_n比例的点). 

## 消失引理

论文的核心是两个关于多项式的引理，我们按照Guth在[2]中的叫法称为消失引理(vanishing lemma)和计数引理(parameter counting lemma). 这节讨论前者. 约定好记号：
- $\mathbb{F}$是一个域.
- $Poly(\mathbb{F}^n)=\mathbb{F}[x_1,…,x_n] $是$\mathbb{F}$上的所有$n$元多项式，$(x_1,…,x_n) \in \mathbb{F}^n$. 一元多项式简记为$\mathbb{F}[t]$.
- $\mathrm{deg} $代表多项式的次数. $ Poly_d(\mathbb{F}^n)$是所有次数不超过$d$的$n$元多项式.

> **定理4.** 设$P\in Poly_d(\mathbb{F}^n)$. 如果$P$在直线$L_{a,b}\subset \mathbb{F}^n$上有$d+1$个零点，则$P$在$L_{a,b}$上取值为$0$.

如果引入$Q\in\mathbb{F}[t]: Q(t)=P(b+ta)$并注意到$\mathrm{deg} Q\leq \mathrm{deg} P$，定理就是以下消失引理的直接推论.

> **消失引理** 设$Q\in Poly_d(\mathbb{F})$. 如果$Q$有$d+1$个零点，则$Q$是零多项式.

*注*. 消失引理只对一元多项式成立！

尽管引理的内容为人熟知，Guth却在[2]对其予以极高的地位：*a fundamental fact that will play a role throughout the book*. 为了保证文章的连贯性这里不给出证明(读者可以查阅任何一本高等代数教材)，我们谈谈引理代表的想法：多项式的**刚性**. 其实引理就讲了一件事：只用“很少”个点上的取值就能确定整个多项式(所谓的插值)，这对于“松软”的光滑函数自然是不可想象的. 古往今来这类“局部拼贴出整体”的结论都属于数学中最梦幻的一部分，在复分析，几何甚至数论(比如Gauss最爱的二次互反律)都能看到它的影子. 我们将在Dvir的证明中看到消失引理以及这个想法的威力. 


## 计数引理

这节讨论第二个引理：

> **计数引理** 设$n\geq 2$，任意一个有限子集$S\subset \mathbb{F}_q^n$，$\vert S\vert=s$，则存在一个非零多项式$P\in Poly(\mathbb{F}^n)$使得$P$在$S$上取值为$0$，且

$$
\mathrm{deg} P\leq \sqrt[n]{n!} s^{1/n}.$$

我们翻译一下定理的内容. 如果用多项式的零点集覆盖$S$，一个直接的做法是构造

$$
A(x)=\prod_{y\in S}(x_1-y_1),$$

其中$x=(x_1,…,x_n)$. 计算得到$\mathrm{deg} P=s$，远大于引理的结果，为什么呢？从几何上看，$A(x)$相当于用$s$个超平面$x_i-y_i=0$覆盖$S$，每个点要占用$1$个超平面，这个方案显然不经济. 这么一看计数引理其实已经带有组合学的风味，本质上在寻找用多项式零点集覆盖$S$的最优方案. <br/>

一般来讲最优化问题都是十分困难的，但计数引理实质上是一个简单的线性代数问题(这也意味着计数引理的结果相当粗糙，当然已经足够好用). 注意到$Ploy_d(\mathbb{F}_q^n)$也构成了$\mathbb{F}_q$上的向量空间，一组典范的基底是所有次数不超过$d$的单项式. 构造映射

$$
T: Ploy_d(\mathbb{F}_q^n)\to \mathbb{F}_q^{s}, $$

$$
T(P)=(P(v_1),…,P(v_s)), S=\{v_1, …, v_s\}.$$

简单验证可知$T$是一个**线性映射**，根据维数公式，如果

$$
\dim Ploy_d(\mathbb{F}_q^n)> s, $$

就存在一个非零多项式$P$使得$T(P)=0$，即$P$在$S$上取值为$0$. 

> **命题5.** $\dim Poly_d(\mathbb{F}\_q^n)= C_{n+d}^d=(n+d)!/(n!d!)$. ($C_m^k$是组合数)

*证明*. 只需计算所有次数不超过$d$的单项式数量. 我们用$d$个物品和$n$个隔板给这些单项式编码. 单项式$x_1^{d_1}…x_n^{d_n}$($d_i\geq 0, \sum d_i \leq d$)对应了以下序列：先放置$d_1$个物品，然后放置一块隔板，再放置$d_2$个物品，然后放置一块隔板，…，放置最后一块隔板后，放置剩余所有物品(如果有的话). 现在共有$(n+d)!$种编码，但要考虑物品之间没有顺序之分，隔板之间也没有顺序之分，所以单项式共有$(n+d)!/(n!d!)$个. $\Box$

现在根据一个简单的估计$(n+d)!/(n!d!)\>d^n/n!$，$d=\sqrt[n]{n!}s^{1/n}$时存在符合题意的多项式，我们完成了计数引理的证明.  $\Box$

## 完成证明，总结

有了两个核心引理，这一节着手有限域Kakeya猜想的完整证明. 取$c_n=1/n!$，我们采用反证法.

- 假设$\vert K\vert=c_n’q^n, c_n’<c_n$，根据计数引理，存在非零多项式$P\in Ploy(\mathbb{F}_q^n)$，$\mathrm{deg} P=\sqrt[n]{n!c_n}\cdot q<q$，且$P$在$K$上取值为$0$.(倘若没有计数引理，我们只能得到什么？)

- 对任意非零的$a\in\mathbb{F}\_q^n$，取落在$K$中的直线$L_{a,b}$. 令$Q\in\mathbb{F}[t]$，$Q(t)=P(b+ta)$, $\forall t\in\mathbb{F}_q$, 于是$\mathrm{deg} Q\leq\mathrm{deg} P$. 直接计算得到$Q(t)$的$\mathrm{deg} P$次项系数恰好是$P_d(a)$，其中$P_d$是$P$的最高次项. 但$Q$有$q$个零点(这点不是显然的，请用有限域的性质验证)，由消失引理可知$Q$是零多项式，所以$P_d(a)=0$. 由$a$的任意性，$P_d$在$\mathbb{F}_q^n\setminus\\{0\\}$上取值为$0$；另外$P_d$是非常值齐次多项式，所以$P_d(0)=0$. 综合以上所述，$P_d$在整个$\mathbb{F}_q^n$上取值为$0$.

- 有限域上很容易犯错的一点在于：取值恒为$0$的多项式不一定就是零多项式！利用$\mathbb{F}_q$的性质$x^q=x$，一元多项式$x^q-x$就是一个反例. 因此在前面所有论述中我们一直采用表述“多项式xx取值为$0$”而不是“多项式xx为$0$”. 不过$\mathrm{deg} P< q$，而下面的命题让现实没有太过反常：
  > **命题6.** 设$P\in Poly_{q-1}(\mathbb{F}_q^n)$. 如果$P$在$\mathbb{F}_q^n$上取值为$0$，那么$P$是零多项式. (有兴趣证明的读者可以尝试对$n$用数学归纳法，并利用消失引理)
  
  因此我们断言$P$的最高次项$P_d$就是零多项式，这与第一步中$P$非零的条件矛盾！有限域Kakeya猜想得证.  $\Box$<br/>

<br/>
总结起来，Dvir的证明大致为两部分：

- 如果$K$太小，可以用计数引理构造次数足够低的非零多项式，其零点覆盖$K$.
- 但$K$的几何性质(比如包含足够多的直线)又指出多项式零点“很多”，由多项式的刚性推出矛盾.

至此我们用多项式的魔法再现了Dvir的奇迹. 值得补充的是，这个简洁高效的证明并没有使得过去Bourgain, Tao的工作黯然失色. 他们引入的大量工具和思想(主要来自调和分析和算术组合)同样深刻地影响了多个领域的未来. **数学研究不仅为了解决问题，更要让人对事物有更好的了解.** 另外有一段小历史：Dvir最开始的证明也没有完全解决猜想——下界只有$c_nq^{n-1}$，后来经Alon(极值组合学的泰斗)和Tao(陶哲轩)的修改才彻底完成. 两位负有盛名的学者也慷慨地让出论文署名权，二人的名字只出现在致谢中.

--------------------------------------------------------------------------------<font size=2>分割线</font>--------------------------------------------------------------------------------

更正：经一位朋友提醒，Dvir的证明已经被收入*The Proof from the Book*（中译本《数学天书中的证明》）第五版，所以导言部分“堪称proof from the book”已经过时了(笑)

<br/>
[<font size="3">少女祈祷中...</font>](https://senyuyangpdelearner.github.io/)
