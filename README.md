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

Kakeya猜想是目前数学界最重要也是最困难的问题之一，横跨调和分析，加性组合，离散几何，解析数论等诸多领域，过去五十年里Fefferman, Bourgain, Wolff, Tao, Guth等顶尖分析学家们为她倾尽心血. 一般而言Kakeya猜想建立在欧氏空间$\mathbb{R}^n$上，而Wolff在1995年提出了离散的有限域版本，以期为原版提供线索. 此后包括Bourgain, Tao等人数学家动用分析，组合和数论中相当艰深的工具做了大量工作，始终与猜想的完全解决隔着一层窗户纸. 人们据此相信，有限域版本和原版的难度相差无几. <br/>
直到2009年，理论计算机科学家[Z. Dvir](https://www.cs.princeton.edu/~zdvir/)的论文[^1](https://www.cs.princeton.edu/~zdvir/papers/Dvir09.pdf)横空出世. Dvir仅仅依靠简单的线性代数和多项式理论便干净利落地解决了**有限域Kakeya猜想**，震惊了数学界. 论文的核心部分经不断发展形成了所谓的**多项式方法**(polynomial method)，如今成为组合，分析乃至编码理论的重要技术. 这篇博客的主题就是复盘Dvir的绝妙证明(堪称proof from the Book)，一窥多项式方法的思想. <br/>

本文参考了以下文献：
> [1] Zeev Dvir. On the size of Kakeya sets in finite fields. Journal of the American Mathematical Society, 22(4):1093–1097, 2009.<br/>
> [2] Larry Guth. Polynomial methods in combinatorics. 

##  Kakeya集和Kakeya猜想

为了叙述Kakeya猜想，我们先介绍Kakeya集(有些文献称为Besicovitch集)的定义.
> \textbf{定义1}. $n$维欧式空间$\mathbb{R}^n$的子集$K$称为**Kakeya集**，如果对任意单位向量$x\in \mathbb{R}^n $，存在$y\in \mathbb{R}^n $使得___单位线段___

$$
L_{x,y}=\{y+tx: 0\leq t\leq 1\}\subset K.$$

用人话讲，Kakeya集包含了每个方向的一条单位线段. 显然全空间$\mathbb{R}^n$是一个Kakeya集，那么有更小的Kakeya集吗？直观上Kakeya集不能太稀疏 (读者可以自己尝试构造$\mathbb{R}^2$中的一些例子，最简单的是半径1/2 的圆盘)，然而Besicovitch在1920年得到一个惊人的构造：
> **定理2.** $\mathbb{R}^n$中存在体积(测度)为$0$的Kakeya集.
自然Besicovitch的例子有许多怪异的性质，这里我们不会谈及具体的构造. 但是从维数上看，“Kakeya集不能太稀疏”似乎成立：Besicovitch的例子的Hausdorff维数是$n$(不熟悉Hausdorff维数和分形的读者不必纠结于这个概念，理解有限域版本并不需要它). 于是有
> **猜想3.**(**Kakeya猜想**) $\mathbb{R}^n$中的Kakeya集的Hausdorff维数是$n$.
乍一看这个奇怪的猜想仿佛是数学家为了饭碗生造出来的玩具，但就如文章开头所说，她的深度和广度远超最初的预期(要讲清楚这点可能需要无穷篇博客hhh). <br/>
下面我们引入离散的有限域版本. 从现在开始，$q$是一个正整数，\mathbb{F}_q$是一个有$q$个元素的有限域，$\mathbb{F}_q^n$是$\mathbb{F}_q$上的$n$维向量空间(抽象代数告诉我们$q$一定是某个素数的幂；$\mathbb{F}_q$在同构意义下是唯一的，从而上面的向量空间是良好定义的). 
> **定义4.**(**有限域Kakeya集**) $\mathbb{R}^n$的子集$K$称为Kakeya集，如果对任意$a\in \mathbb{F}_q^n$，存在$b\in\mathbb{F}_q^n$使得___直线___

$$
L_{a,b}=\{b+ta: t\in \mathbb{F}_q\}\subset K.$$

我们一样可以问：有限域Kakeya集可以多小？
> **猜想5.**(**有限域Kakeya猜想**) 存在只关于$n$的正常数$0\<c_n\<1$，对任意Kakeya集$K\subset \mathbb{F}_q^n$都有

$$
\vert K\vert \geq c_n q^n.$$

现在猜想已经得到证明，所以我们知道有限域Kakeya集确实不能太稀疏(至少包含c_n比例的点). 

## 有限域补给站

这一节会为不熟悉有限域的读者补给最低限度的知识，熟悉的读者可以跳过本节. 

## 两个核心引理

## 完成证明，总结

<br/>
[<font size="3">少女祈祷中...</font>](https://senyuyangpdelearner.github.io/)
