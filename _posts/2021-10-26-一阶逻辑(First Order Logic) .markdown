---
layout: post
title:      一阶逻辑(First Order Logic)
subtitle:   
author:     uans3k
header-img: img/post-bg-2015.jpg
tags:
    - 逻辑
    - 形式逻辑
---
在[命题逻辑](./2021-10-20-命题逻辑(Propositional%20Logic).markdown)中,我们无法深入到命题内部结构,而一阶逻辑引入了量化、任意函数、关系的语法,可以在语言内部构造命题结构,加强了语言的**表达**能力.
## 1 $L^1$定义

### 1.1 语法

### 1.1.1 定义 $L^1-符号$
>$L^1$语言的$L^1-符号$由以下构成:  
>- 变量: $x_1,...,x_n$
>- 常量: $c_1,...c_m$
>- n元函数: $f_1,...,f_l$
>- n元关系(谓词): $R_1,...,R_o$
>- 真值函数-命题联结词-逻辑符号:$\neg,\wedge,\vee,\Rightarrow,\equiv$
>- 量词:$\exists,\forall$
>- 括号:$(,)$  

### 1.1.2 定义 $L^1-项$
>$L^1$语言的$L^1-项t$由以下构成:  
>- 变量
>- 常量
>- 任意n元$L^1-项$序列$t_1,...,t_n$和n元函数$f$:$f(t_1,...,t_n)$
>  
> 没有变量的**项**称为**闭项**

### 1.1.3 定义 $L^1-公式$
>$L^1$语言的$L^1-公式$由以下构成: 
>- 任意**n元关系**$R$和$L^1-项$序列$t_1,...,t_n$:R(t_1,...,t_n)
>- 任意$L^1-公式\phi,\psi$:$\neg \phi$,$\phi \wedge\psi$,$\phi \vee\psi$,$\phi \Rightarrow \psi$,$\phi \equiv \psi$
>- 任意$L^1-公式\phi$,**变量**$x$:$\exists x \phi,\forall x \phi$

### 1.1.4 $L^1$的BNF
> $formula ::=\\   
> |relation \ '('\ term \  (,term)* \ ')'\\
> |'('? \ unit-connectives \ formula \ ')'?\\
> | '('? \ formula \  \ bin-connectives \ formula \ ')'?\\
> |'\forall'formula\\
> |'\exist'formula$  
> $term ::= var|const|function \ '('\ term \  (,term)* \ ')'$  
> $relation ::=\ 'R_i'$  
> $unit-connectives::=\ '\neg'$  
> $bin-connectives::=\ '\wedge'|'\vee'|'\Rightarrow'|'\equiv'$  
> $function::=\ 'f_i'$  
> $var::=\ 'x_i'$  
> $const::=\ 'c_i'$

### 1.1.5 高阶语言$L^n$
$L^1$语言引入了量词、变量、常量、关系、函数，使得可以构造命题内部结构，但量词只能量化变量不能量化关系、函数如$\forall R_1,\exists f_1$,$L^2$允许量化关系和函数,而$L^3$允许关系、函数作为关系、函数的参数，依次可以构成$L^n$语言

## 1.2 语义

### 1.2.1 定义 集合上的函数与关系
>- 集合A上的**n元函数**$f_i$是A的系列n元序列到A元素的映射
>- 集合A上的**n元关系**$R_i$是A的系列n元序列的集合,集合上n元序列具有关系$R_i$当且仅当n元序列是$R_i$的元素

### 1.2.2 定义 模型
>一个$L^1$**模型**是一个有序对$M=(A,I)$,其中A是一个非空的集合被称为M的**论域**,I被称为**解释**,是一个满足如下条件的函数:
>- 任意$L^1$中的常量$c_i$,$I(c_i)$是A的元素,记为$M[[c_i]]$
>- 任意$L^1$中的n元函数$f_i$,$I(f_i)$是A上的**n元函数**,记为$M[[f_i]]$
>- 任意$L^1$中的n元关系$R_i$,$I(R_i)$是A上的**n元关系**,记为$M[[R_i]]$

### 1.2.3 定义 赋值
>$M=(A,I)$是一个$L^1$**模型**,$M$上的赋值$\sigma$是一个有序对$\sigma=(M,\omega)$,$\omega$是变量到A的函数,$L^1$在$\sigma$的赋值下满足:  
>- $\sigma[[c_i]]=M[[c_i]]$  
>- $\sigma[R_i]=M[[R_i]]$
>- $\sigma[[f_i]]=M[[f_i]]$
>- $\sigma[[x_i]]=\omega[[x_i]]$  
>    
>$\sigma(a/x_k)$是$M$上的一个赋值,其中$a属于A$:
>- $\sigma(a/x_k)[[t]]=a$若$t=x_k$
>- $\sigma(a/x_k)[[t]]=\sigma[[t]]$若$t \neq x_k$

### 1.2.4 定义 塔尔斯基语义
>$M=(A,I)$上的赋值$\sigma=(M,\omega)$,$\sigma$对$L^1-公式$的**解释**是一个$L^1-公式$到布尔值的映射,可以递归的定义为:  
>对所有的$L^1-项$有:
>- 变量$x_i:\sigma[[x_i]]$
>- 常量$c_i:\sigma[[c_i]]$
>- 任意n元$L^1-项$序列$(t_1,...,t_n)$和n元函数$f$:$\sigma[[f(t_1,...,t_n)]]=\sigma[[f]](\sigma[[t_1]],...,\sigma[[t_n]])$
> 
> 对所有的$L^1-公式$有:
>- $\sigma[[R(t_1,...,t_n)]]=True$ 当且仅当 $(\sigma[[t_1]],...,\sigma[[t_1]])属于\sigma[[R]]$
>- $\sigma[[\neg \phi]]=True$ 当且仅当 $\sigma[[\phi]]=False$
>- $\sigma[[\phi \vee \psi]]=True$ 当且仅当 $\sigma[[\phi]]=True或\sigma[[\psi]]=True$
>- $\sigma[[\phi \wedge \psi]]=True$ 当且仅当 $\sigma[[\phi]]=True且\sigma[[\psi]]=True$
>- $\sigma[[\phi \Rightarrow \psi]]=True$ 当且仅若 $\sigma[[\phi]]=True则\sigma[[\psi]]=True$
>- $\sigma[[\phi \equiv \psi]]=True$ 当且仅若 $\sigma[[\phi]]=\sigma[[\psi]]$
>- $\sigma[[\forall x \phi]]=True$当且仅当**所有**属于$A$的$a$有$\sigma(a/x)[[\phi]]=True$
>- $\sigma[[\exist x \phi]]=True$当且仅当**存在**属于$A$的$a$有$\sigma(a/x)[[\phi]]=True$
>  
> 这样的**解释**被称为**塔尔斯基语义**

### 1.2.5 定义 满足
>- 对任意$L^1-公式$集合$\Gamma$,我们称赋值$\sigma$**满足**$\Gamma$当前仅当对任意属于$\Gamma$的公式$\phi$有$\sigma[[\phi]]=True$,记为$\sigma \vDash \Gamma$,特别地,我们记$\sigma \vDash \{\phi\}$为$\sigma \vDash \phi$.我们记$\sigma \nvDash \Gamma$为非$\sigma \vDash \Gamma$,特别地,我们记$\sigma \nvDash \{\phi\}$为$\sigma \nvDash \phi$.
>- 对任意$L^1-公式$集合$\Gamma$,我们称模型$M$**满足**$\Gamma$当前仅当对任意属于$\Gamma$的公式$\phi$和任意M上的赋值$\sigma$有$\sigma[[\phi]]=True$,记为$M \vDash \Gamma$,特别地,我们记$M \vDash \{\phi\}$为$M \vDash \phi$.我们记$M \nvDash \Gamma$为非$M \vDash \Gamma$,特别地,我们记$M\nvDash \{\phi\}$为$M \nvDash \phi$.

### 1.2.6 定义 逻辑蕴涵(logic implie)
> 对任意$L^1-公式$集合$\Gamma$和$L^1-公式 \phi$,我们称$\Gamma$**逻辑蕴涵**$\phi$当且仅当对任意赋值$\sigma$有若$\sigma \vDash \Gamma$则$\sigma \vDash \phi$,我们记$\Gamma \vDash \phi$,$\phi$称为$\Gamma$的逻辑后承。我们记$\Gamma \cup \{\phi_1,...,\phi_n\} \vDash \psi$为$\Gamma,\phi_1,...,\phi_n \vDash \psi$.

### 1.2.7 定义 逻辑等值(logic equive)
>任意$L^1-公式\phi,\psi$称为**逻辑等值**当且仅当$\phi \vDash \psi$且$\psi \vDash \phi$

### 1.2.8 定义 逻辑有效式(logic efficient)
> 我们称$L^1-公式\phi$是逻辑有效式(逻辑真理)当且仅当对任意赋值$\sigma$有$\sigma \vDash \phi$,记为$\vDash \phi$ 

该节定义了$L^1$的语义，其语言的目标在于判定逻辑蕴涵关系、逻辑等值关系和逻辑有效式。

## 2 $L^0$与$L^1$的关系
$L^1$通过引入量化、函数、关系来扩展$L^0$命题的内部,因此再此之外的结构应该是一致的，本节描述这些关系.

### 2.1 定义 $L^0$的$L^1$代入
>s是一个$L^0$命题变量到$L^1$公式的函数,可以递归的定义$L^0$的$L^1$**代入**$\phi<s>$为:
>- 命题变量$p<s>=s(p)$
>- $(\neg \phi )<s>=\neg (\phi<s>)$
>- $(\phi \circ \psi )<s>=(\phi<s> \circ \psi<s>),\circ 为\vee,\wedge,\Rightarrow,\equiv$
>  
>对公式集$\Gamma<t>$表示对其中每一个公式进行代入

### 2.2 定理 $L^0$与$L^1$的关系
>对任意$L^0$的公式集$\Gamma$和公式$\phi,\psi$有:
>- 若$\Gamma \vDash \phi$则$\Gamma<t> \vDash \phi<t>$
>- 若$\phi$是**重言式**则$\phi<t>$是**逻辑有效式**
>- 若$\phi、\psi$**重言等值**则$\phi<t>、\psi<t>$**逻辑等值**
>- 若$\phi$**可满足**则$\phi<t>$**可满足**

利用2.2可以很快的的平移**命题逻辑**的一些结论

## 3 $L^1-公式$的一些描述
由于量化、函数、关系的引入,$L^1-公式$有更复杂的结构,为了描述具有特定结构的$L^1-公式$,我们引入一些定义来代称它们.

### 3.1 定义 原子公式、量化公式
>- $L^1-项 t_1,...,t_n$和n元关系$R$,$R(t_1,...,t_n)$称为**原子公式**
>- $\forall x \phi ,\exists x \phi$称为**量化公式**

### 3.2 定义 代入 
> $L^1$的代入s是**变量**到**项**的函数,我们记**公式**$\phi$的s代入为$\phi<s>$,递归的定义为:
>- $x<s>=s(x)$
>- $c<s>=c$
>- $f(t_1,...,t_n)<s>=f(t_1<s>,...,t_n<s>)$
>- $R(t_1,...,t_n)<s>=R(t_1<s>,...,t_n<s>)$
>- $(\neg \phi)<s>=\neg \phi<s>$
>- $(\phi \circ \psi)<s>=\phi <s>  \circ \psi <s>$,其中$\circ 属于\{\wedge,\vee,\Rightarrow,\equiv \}$    
>- $\bullet x \phi <s> = \bullet x \phi <s^{-x}>$,其中$\bullet 属于 \{\forall,\exists\}$  
>   
> 其中 
> $s^{-x}(v) = \begin{cases}
    v \ 若 v=x \\
    s(v) \ 否则
\end{cases}
$  
> 特别地我们记 $s = \bf{t}/\bf{x}=(t_1/x_1,...,t_k/x_k)$表示
> $s(v) = \begin{cases}
    t_i \ 若 v=x_i \\
    v  \ 否则
\end{cases}
$  
>$s=\bf{t}^{-t_i}/\bf{x}^{-x_i}=(t_1/x_1,...,t_{i-1}/x_{i-1},t_{i+1}/x_{i+1},...,t_k/x_k)$类似

### 3.3 定义 量词的辖域、约束与自由
>$L^1-公式\forall x\phi或\exists x\phi$中量词$\forall x 或\exists x$的**辖域**为$\phi$,$\phi$称为**被辖**的,$\phi$中的任意变量$x$被称为**约束**的,若$x$不属于任何**被辖**的公式则$x$称为自由的.若公式$\phi$内的$x$搜索被**约束**的,我们称$x$在$\phi$**非自由出现**,记为$\phi_{+x}$,若$x$不出现在$\phi$中,记$\phi_{-x}$

### 3.4 定义 自由代入
>对任意$L^1-项t$、公式$\phi$和变量$x$,我们称$t$可自由代入$\phi$中的$x$当且仅当对$t$中所有的变量$y$和在$\phi$中**自由**的$x$,所有量词$\forall y或\exists y$的辖域$\phi$不含有变量$x$,而那些辖域中包含变量$x$的量词被称为$t$代入$x$的障碍量词

例如令$t=f(y)$,$R_1(x) \wedge \exists y R_2(y)$中$x$是可以被$t$自由代入的而$\exists yR_2x$中的$x$是不可被$t$自由代入的

### 3.5 定义 易字式
> $y$不在$\phi$中自由出现且可自由代入x.我们称$\forall y \phi<y/x>$为$\forall x \phi$的**易字式**,$\exists y \phi<y/x>$为$\exists x \phi$的**易字式**

### 3.6 定义 置换
> $\phi,\chi$为任意公式,$p$为**原子公式**,**置换**$\phi<\chi/p>$定义为:
>- $p<\chi/p>=\chi$
>- 任意跟$p$不一样的原子公式$q$,$q<\chi/p>=q$
>- $(\neg \phi)<\chi/p>=\neg \phi<\chi/p>$
>- $(\phi \circ \psi)<\chi/p>=\phi<\chi/p> \circ \psi<\chi/p>$其中$\circ 属于 \{\wedge,\vee,\Rightarrow,\equiv\}$
>- $(\bullet x\phi)<\chi/p>=\bullet x \phi<\chi/p>$其中$\bullet 属于 \{\forall,\exists\}$

### 3.7 定义 易字变形
> 任意公式$\phi,\phi^\prime$,$\phi^\prime$是$\phi$的**简单易字变形**当且仅当存在公式$\psi$和**原子公式**$p$以及**量化公式**$\chi$和其**易字式**$\chi^\prime$使得$\phi=\psi<\chi/p>,\phi^\prime=\psi<\chi^\prime/p>$
> ,$\phi$的**易字变形**为多次的**简单易字变形**.

### 3.8 定义 规范易字变形
> 任意公式 $\phi$、项$t$和变量$x$,$\phi$的$t/x$-**规范易字变形**,记为$\phi_{t/x}$,定义为:
>- 若$t$可自由代入$\phi$中的$x$,$\phi_{t/x}=\phi$
>- 否则,令$\bullet y_1,...,\bullet y_n$为其在$\phi$所有的**障碍量词**序列,令$z_1,...,z_n$为不出现在$t$中的**变量**,对$\phi$中的$\bullet y_i\psi_i$逐一作**简单易字变形**$\bullet z_i\psi_i<z_i/y_i>$,最终得到$\phi$的**易字变形**$\phi^\prime,\phi_{t/x}=\phi^\prime$  
  
从定义可以很简单的得出关于**规范易字变形**的以下结论

### 3.9 定理 
> 对任意公式$\phi$、项$t$和变量$x$:
>- $t$可**自由代入**$\phi_{t/x}$中的$x$
>- $\phi_{t/x}$与$\phi$ 逻辑等值
>- 任意赋值$\sigma$有$\sigma \vDash \phi_{t/x}<t/x>$当且仅当$\sigma(\sigma[[t]]/x) \vDash \phi_{t/x}<t/x>$
>- $\forall x \phi \vDash \phi_{t/x}<t/x>$
>- $\phi_{t/x}<t/x> \vDash \exists x \phi$

## 4 $L^1$的演绎$H^1$
跟$L^0$的$H^0$演绎一样,我们可以通过定义建立**公理系统**,采用演绎的形式得到**逻辑蕴涵**、**逻辑有效式**和**逻辑等值**而避免**穷举赋值**,我们将选定**逻辑有效式**和**操作**作为**规则(rule)**,并讨论这么选择和做法的性质,主要包括**紧致性**,我们限制$L^1$的量词为$\forall$以及**逻辑联结词**为$\neg$和$\Rightarrow$,事实上,所有其他逻辑联结词形成的公式的语义总可以与用以上逻辑联结词构成的公式相同:
>- $\sigma[[\phi \vee \psi]]=\sigma[[\neg \phi \Rightarrow \psi]]$
>- $\sigma[[\phi \wedge \psi]]=\sigma[[\neg (\phi \Rightarrow 
\neg \psi)]]$  
>- $\sigma[[\phi \equiv \psi]]=\sigma[[(\phi \Rightarrow 
\psi) \wedge (\psi \Rightarrow 
\phi)]]$
>- $\sigma[[\exists \phi]]=\sigma[[\neg (\forall \neg \phi)]]$
因此限制后的$L^1$跟原$L^1$的**表达能力**是完全相同的,其相关性质也是相同的,后面会更详细的描述.

### 4.1 $H^1$相关定义

### 4.1.1 定义 操作(operator)
> 从一个公式或多个公式得到另外一个公式的动作称为**操作**

### 4.1.2 $H_r^1$ 公理系统
>包含$L^1$语法及其上的一个**规则**$r$的系统称为$H_r^1$的系统称为**公理系统**,其中规则包含**逻辑有效式**和**操作**,这些$逻辑有效式$称为**公理**

### 4.1.2 $H_r^1$ 演绎
> 任意$L^1$公式集$\Gamma$和公式$\phi$,$\Gamma$到$\phi$的演绎是一个公式序列$\phi_1,...,\phi_n$满足:
> - $\phi_n=\phi$
> - $\phi_k,k<n$或是$H_r^1$的**公理**,或是$\Gamma$的公式,或是存在一个公式$\phi_j=\phi_i \Rightarrow \phi_k,i,j<k$
>  
> 记为$\Gamma \vdash \phi$,$\phi$称为在$H_r^1$从$\Gamma$**可演绎**,特别地$\Gamma=\varnothing$记为$\vdash \phi$,被称为$\phi$在$H_r^1$下**可证**,$\phi$是$H_r^1$下的**定理**

### 4.1.3 定义 可靠性(soundness)
>对任意$H_r^1$下的$\Gamma$和$\phi$,如果$\Gamma \vdash \phi$则$\Gamma \vDash \phi$,特别地如果$\vdash \phi$则$\vDash \phi$,那么我们称$H_r^1$具有**可靠性**

### 4.1.4 定义 一致性(consistency)
>**公理系统**$H_r^1$具有**一致性**当前仅当不存在$L^1-公式\phi$使得$\vdash \phi 且\vdash \neg \phi$.  
>$\Gamma$在$H_r^1$下具有**一致性**当且仅当不存在$L^1-公式\phi$使得$\Gamma \vdash \phi 且\Gamma \vdash \neg \phi$.  


### 4.1.5 定义 完全性(completeness)
>对任意$H_r^1$下的$\Gamma$和$\phi$,如果$\Gamma \vDash \phi$则$\Gamma \vdash \phi$,特别地如果$\vDash \phi$则$\vdash \phi$,那么我们称$H_r^1$具有**完全性**


### 4.1.6 定义 紧致性(compactness)
>**公理系统**$H_r^1$具有**紧致性**当且仅当对任意公式集$\Gamma$,若$\Gamma \vDash \phi$存在$\Gamma$**有穷子集**$\Delta$使得$\Delta \vDash \phi$

可以看出若$H^1$具有**完全性、紧致性**,则其所有的**逻辑蕴涵**、**逻辑等值**、**逻辑有效**关系是**可判定**的.

### 4.2 $H^1$性质
### 4.2.1 定义 分离操作(modus ponens)
>从$\phi,\phi \Rightarrow \psi$得到$\psi$的动作称为**分离**,简记分离操作为MP
### 4.2.2 定义 $r_1$规则
>$$r_1=\begin{cases}
    1:\phi \Rightarrow (\psi \Rightarrow \phi) \\
    2:(\phi \Rightarrow (\psi \Rightarrow \chi))\Rightarrow ((\phi \Rightarrow \psi) \Rightarrow (\phi \Rightarrow \chi))\\
    3:(\neg \phi \Rightarrow \psi) \Rightarrow ((\neg \phi \Rightarrow \neg \psi) \Rightarrow \phi)\\
    MP
\end{cases}$$  

### 4.2.3 $H_{r_1}^1$相关定理
对$H_{r_1}^1$下的公式集合$\Gamma 、\Delta$,公式$\phi、\psi、\chi$
> 1. 若$\Gamma \vdash \phi$则存在$\Gamma$的**有穷子集**$\Delta$有$\Delta \vdash \phi$
> 2. 若$\Gamma \vdash \phi$且$\Delta$是$\Gamma$的子集则$\Delta \vdash \phi$
> 3. CUT (剪切定理): 若$\Gamma,\phi_1,...\phi_n \vdash \psi$且$\Delta \vdash \phi_i,i \leq m$则$\Gamma \cup \Delta \vdash \psi$
> 4. Tran (传递性,transitivity):若$\Gamma \vdash \phi,\phi \vdash \psi$则$\Gamma \vdash \psi$
> 5. MP (分离定理,modus ponens):若$\Gamma \vdash \phi,\Gamma \vdash \phi \Rightarrow \psi$则$\Gamma \vdash \psi$
> 6. DT (演绎定理,deduction theorem):若$\Gamma,\phi \vdash \psi$则$\Gamma \vdash \phi \Rightarrow \psi$
> 7. HS (假言三段论,hypothetical syllogism):若$\Gamma \vdash \phi \Rightarrow \psi,\Delta \vdash \psi \Rightarrow \chi$则$\Gamma \cup \Delta \vdash \phi \Rightarrow \chi$
> 8. IE (非一致性效应,inconsistency effect):若$\Gamma \vdash \phi,\Gamma \vdash \neg \phi$则$\Gamma \vdash \psi$,若$\Gamma,\phi \vdash \neg \phi$则$\Gamma ,\phi,\vdash \psi$  
> 9. SRAA (简单归谬律,简单反证法,simple reductio ad absudrum):若$\Gamma,\neg \phi \vdash \phi$则$\Gamma \vdash \phi$,若$\Gamma,\phi \vdash \neg \phi$则$\Gamma \vdash \neg \phi$
> 10. RAA (归谬律,反证法, reductio ad absudrum):$\Gamma \vdash \phi$当且仅当$\Gamma \cup \phi$不一致
> 11. DN (双重否定,dounble neg):$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$,$\Gamma,\psi\vdash \phi$当且仅当$\Gamma,\neg \neg \psi \vdash \phi$
> 12. Contrap (假言对位):$\Gamma ,\phi \vdash \psi$当前仅当$\Gamma,\neg \psi \vdash \neg \phi$,$\Gamma ,\phi \vdash \neg \psi$当前仅当$\Gamma,\psi \vdash \neg \phi$    


>证明:  
> (8)若$\Gamma \vdash \phi,\Gamma \vdash \neg \phi$则$\Gamma \vdash \psi$     
> 1:$\phi,\neg \phi \vdash \psi$#  
>> 1:$\neg \phi \Rightarrow (\neg \psi \Rightarrow \neg \phi)$#$r_1.1$  
>> 2:$\neg \phi$#hyp  
>> 3:$\neg \psi \Rightarrow \neg \phi$#$MP(1,2)$  
>> 4:$\phi \Rightarrow (\neg \psi \Rightarrow \phi)$#$r_1.1$  
>> 5:$\phi$#hyp  
>> 6:$\neg \psi \Rightarrow \phi$#$MP(4,5)$  
>> 7:$(\neg \psi \Rightarrow \phi) \Rightarrow ((\neg \psi \Rightarrow \neg \phi) \Rightarrow \psi)$#$r_1.3$  
>> 8:$(\neg \psi \Rightarrow \neg \phi) \Rightarrow \psi$#$MP(6,7)$  
>> 9:$\psi$#MP(8,3)   
>>
> 2:$\Gamma \vdash \phi$#hyp   
> 3:$\Gamma \vdash \neg \phi$#hyp   
> 4:$\Gamma \vdash \psi$#CUT(1,2,3)     
> 
> (9) 若$\Gamma,\neg \phi \vdash \phi$则$\Gamma \vdash \phi$#  
> 1: $\vdash \phi \Rightarrow \phi$#  
>>1:$\phi \Rightarrow ((\phi \Rightarrow \phi) \Rightarrow\phi))$#$r_1$  
>> 2:$(\phi \Rightarrow ((\phi \Rightarrow \phi) \Rightarrow\phi)) \Rightarrow ((\phi \Rightarrow(\phi \Rightarrow \phi)) \Rightarrow(\phi \Rightarrow \phi))$#$r_1$  
>> 3:$(\phi \Rightarrow (\phi \Rightarrow \phi)) \Rightarrow (\phi \Rightarrow \phi)$#MP(1,2)  
>> 4:$\phi \Rightarrow (\phi \Rightarrow \phi)$#$r_1$  
>> 5:$\phi \Rightarrow \phi$#MP(3,4)     
>>  
> 2:$\neg \phi \Rightarrow \phi \vdash \phi$#
>> 1:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \phi$#
>>> 1: $\neg \phi \Rightarrow  \phi$#假设  
>>> 2: $\neg \phi$#假设  
>>> 3: $\phi$#MP(1,2)
>>> 
>> 2:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \neg (\neg \phi \Rightarrow \phi)$#IE(1)  
>> 3:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \neg \phi \Rightarrow \phi$#IE(1)  
>> 4:$\neg \phi \Rightarrow \phi \vdash \neg \phi \Rightarrow \neg (\neg \phi \Rightarrow \phi)$#DT(2)  
>> 5:$\neg \phi \Rightarrow \phi \vdash \neg \phi \Rightarrow (\neg \phi \Rightarrow \phi)$#DT(3)   
>> 6:$\neg \phi \Rightarrow \neg (\neg \phi \Rightarrow \phi),\neg \phi \Rightarrow (\neg \phi \Rightarrow \phi) \vdash \phi$#$r_1.3$
>> 7: 
>>  
>3:$\Gamma,\neg \phi \vdash \phi$#假设  
>4:$\Gamma \vdash \neg \phi \Rightarrow \phi$#DT(3)  
>5:$\Gamma \vdash \phi$#CUT(2,4)
>
> (10)$\Gamma \vdash \phi$当且仅当$\Gamma \cup \phi$不一致#  
> 1: 若$\Gamma \cup \phi$不一致则$\Gamma \vdash \phi$#  
>  1:$\Gamma,\phi \vdash \neg \phi$#hyp  
>  2:$\Gamma \vdash \phi \Rightarrow \neg \phi$#DT(2)  
>  3:l
> (11)$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$#  
> 1:若$\Gamma \vdash \phi$则$\Gamma \vdash \neg \neg \phi$#
> > 1: $\phi ,\neg \phi \vdash \neg \neg \phi$#  
> > > 1: $(\neg \phi \Rightarrow \phi) \Rightarrow (\neg \phi \Rightarrow \neg \phi) \Rightarrow \neg \neg \phi$#$r_1.3$  
> > > 2: $\neg \phi \Rightarrow (\neg \phi \Rightarrow \neg \phi)$#$r_1.1$  
> > > 3: $\neg \phi \Rightarrow (\phi \Rightarrow \neg \phi)$#$r_1.1$  
> > > 4: $\neg \phi \Rightarrow \neg \phi$#MP(hyp,2)  
> > > 5: $\neg \phi \Rightarrow  \phi$#MP(hyp,3)  
> > > 6: $\neg \neg \phi$#MP(MP(1,5),4)
> > >
> > 2:$\phi \Rightarrow \neg \neg \phi$#SRAA(1)  
> > 3:$\Gamma \vdash \neg \neg \phi$#CUT(hyp,2)
> >
> 2:若$\Gamma \vdash \neg \neg \phi$则$\Gamma \vdash \phi$#
> > 同理
> >
> 3:$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$#1,2
>
>(12) $\Gamma ,\phi \vdash \psi$当前仅当$\Gamma,\neg \psi \vdash \neg \phi$#  
> 1:若$\Gamma ,\phi \vdash \psi$则$\Gamma,\neg \psi \vdash \neg \phi$#  
>> 1:$\Gamma ,\phi ,\neg \psi \vdash \neg \phi$#IE(hyp)  
>> 2:$\Gamma ,\neg \psi \vdash \neg \phi$#SRAA(1)  
>> 3:$\Gamma \vdash \neg \psi \Rightarrow \neg \phi$DT(2)
>>
> 其他类似

### 4.2.3 $r_2规则$
$r_1$未包括量化规则,$r_2$填上了相关公里
>$$r_2=\begin{cases}
  r_1  \\
  4:\forall x(\phi \Rightarrow \psi) \Rightarrow (\forall \phi \Rightarrow \forall \psi) \\
  5:\forall x \phi_{t/x} \Rightarrow \phi_{t/x}<t/x> \\
  6:\phi_{+x} \Rightarrow \forall x \phi_{+x} \\ 
  7: \forall x_1,...,x_n \phi,\phi为任意r_2公理
\end{cases}$$

### 4.2.3 $H_{r_2}^1$相关定理
$H_{r_2}^1$除了$H_{r_1}^1$相关定理,还包含一些量化相关的定理
> 1. QV(量化变量,quantify variable,变量概括):  
> - 若$\Gamma_{+x} \vdash \phi$则$\Gamma_{+x} \vdash \forall x \phi$  
> - 若$\Gamma_{+x},\phi \vdash \psi_{+x}$则$\Gamma_{+x}, \exists x \phi \vdash \psi_{+x}$  
> - 若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\forall x \phi \vdash \forall x \psi$  
> - 若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\exists x \phi \vdash \exists x \psi$
> 2. RE(置换,replace element):  
> - $\forall \bf{x}(\phi_{\bf{t}/\bf{x}} \equiv \psi_{\bf{t}/\bf{x}}) \vdash \chi<\phi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p> \equiv \chi<\psi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p>$   
> - 若$\Gamma \vdash \forall \bf{x}(\phi_{\bf{t}/\bf{x}} \equiv \psi_{\bf{t}/\bf{x}})$则$\Gamma \vdash \chi<\phi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p> \equiv \chi<\psi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p>$
> 3. CV(变化变量,change variable,变量易字):  
> - $\forall x \phi_{y/x,+y} \vdash \forall y \phi_{y/x,+y}<y/x>$ 且 $\forall y \phi_{y/x,+y}<y/x> \vdash \forall x \phi_{y/x,+y}$   
> - $\exists x \phi_{y/x,+y}\vdash \exists y \phi_{y/x,+y}<y/x>$且$\exists y \phi_{y/x,+y}<y/x> \vdash \exists x \phi_{y/x,+y}$
> - $\phi$及其易字变形$\phi^\prime$有:$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \phi^\prime$,$\Gamma,\phi \vdash \psi$当且仅当$\Gamma,\phi^\prime \vdash \psi$
> 4. QC(量化常量,quantify constant,常量概括):
> - 若$\Gamma_{-c} \vdash \phi_{-c}<c/x>$则$\Gamma_{-c} \vdash \forall x \phi_{-c}$
> - 若$\Gamma_{-c},\phi_{-c}<c/x> \vdash \phi$则$\Gamma_{-c},\exists x \phi_{-c}\vdash \phi$

>证:
>(1)  
> 1: 若$\Gamma_{+x} \vdash \phi$则$\Gamma_{+x} \vdash \forall x \phi$ #  
>>由假设$\phi_0,...,\phi_n$是$\Gamma_{+x}$到$\phi$的演绎。首先证明对任意$\phi_i$,有$\forall x \phi_i$可从$\Gamma_{+x}$演绎.释归纳于i,(1)$\phi_i$是公理,由$r_2.7$可知$\phi_i$.(2)$\phi_i$属于$\Gamma_{+x}$,由$r_2.6$可知$\forall x \phi_i$可从$\Gamma_{+x}$演绎.(3)由演绎和MP的定义，存在$j,k\le i,\phi_k: \phi_j \Rightarrow \phi_i$,根据归纳假设$\forall x \phi_k = \forall \phi_j \Rightarrow \phi_i$可演绎，$\forall x \phi_j$可演绎，因此由$r_2.4$、DT、CUT可知$\forall x \phi_j$可演绎。由上述证明和假设可知$\Gamma_{+x} \vdash \forall x \phi$   
>> 
> 2: 若$\Gamma_{+x},\phi \vdash \psi_{+x}$则$\Gamma_{+x},\exists \phi \vdash \psi_{+x}$ #  
>>1: $\Gamma_{+x},\phi \vdash \psi_{+x}$ # hyp  
>>2: $\Gamma_{+x},\neg \psi_{+x} \vdash \neg \phi$ # Contrap(1)  
>>3: $\neg \phi_{+x} \vdash \forall x \neg \phi_{+x}$#DT($r_2.6$)   
>>4: $\Gamma_{+x},\neg \psi_{+x} \vdash \forall x \neg \phi$  # CUT(3)  
>>5: $\Gamma_{+x},\neg  \forall x \neg \phi \vdash \psi_{+x}$ #Contrap(4)
>>
> 其他由上述可以很自然得到
<!-- >证:  
>$\phi_0$ -->


### 4.2.3 定理 一致性
>任意$H_r^1$具有一致性