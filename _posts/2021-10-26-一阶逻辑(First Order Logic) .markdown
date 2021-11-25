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

### 1.1.1 定义 $L_{C,F,R}^1-符号$
>$L^1$语言的$L^1-符号$由以下构成:  

>- 常量集$C=\{c_1,...c_m\}$
>- n元函数集$F=\{f_1,...,f_l\}$
>- n元关系(谓词)集$R=\{r_1,...,r_o\}$
>- 变量(符号表)$x_1,...,x_n$
>- 真值函数-命题联结词-逻辑符号:$\neg,\wedge,\vee,\Rightarrow,\equiv$
>- 量词$\exists,\forall$
>- 括号:$(,)$  
>
> 其中变量、命题链接词、量词、括号称为**逻辑符号(logical symbol)**,他们在任何$L_{C,F,R}^1$语言中是不可或缺的,
$C,F,R$被称为**非逻辑符号(extralogical symbols)**,不同的$C,F,R$构成了不同的$L_{C,F,R}^1$语言
### 1.1.2 定义 $L_{C,F,R}^1-项$
>$L^1$语言的$L^1-项t$由以下构成:  
>- 变量
>- 常量
>- 任意n元$L^1-项$序列$t_1,...,t_n$和n元函数$f$:$f(t_1,...,t_n)$
>  
> 没有变量的**项**称为**闭项**

### 1.1.3 定义 $L_{C,F,R}^1-公式$
>$L^1$语言的$L^1-公式$由以下构成: 
>- 任意**n元关系**$R$和$L^1-项$序列$t_1,...,t_n:R(t_1,...,t_n)$
>- 任意$L^1-公式\phi,\psi$:$\neg \phi$,$\phi \wedge\psi$,$\phi \vee\psi$,$\phi \Rightarrow \psi$,$\phi \equiv \psi$
>- 任意$L^1-公式\phi$,**变量**$x$:$\exists x \phi,\forall x \phi$

### 1.1.4 $L_{C,F,R}^1$的BNF
> $formula ::=\\   
> |relation \ '('\ term \  (,term)* \ ')'\\
> |'('? \ unit-connectives \ formula \ ')'?\\
> | '('? \ formula \  \ bin-connectives \ formula \ ')'?\\
> |'\forall' formula\\
> |'\exists' formula$  
> $term ::= var|const|function \ '('\ term \  (,term)* \ ')'$  
> $relation ::=\ 'r_i','r_i' \in R$  
> $unit-connectives::=\ '\neg'$  
> $bin-connectives::=\ '\wedge'|'\vee'|'\Rightarrow'|'\equiv'$  
> $function::=\ 'f_i','f_i' \in F$  
> $var::=\ 'x_1'｜'x_2'|...$  
> $const::=\ 'c_i','c_i' \in C$

### 1.1.5 高阶语言$L^n$
$L_{C,F,R}^1$语言引入了量词、变量、常量、关系、函数，使得可以构造命题内部结构，但量词只能量化变量不能量化关系、函数如$\forall r_i,\exists f_i$,$L^2$允许量化关系和函数,而$L^3$允许关系、函数作为关系、函数的参数，依次可以构成$L^n$语言

后面无特殊说明,我们用$L^1$表示**任意**的$L_{C,F,R}^1$的语言

## 1.2 语义

### 1.2.1 定义 集合上的函数与关系
>- 集合A上的**n元函数**$f_i$是A的系列n元序列到A元素的映射
>- 集合A上的**n元关系**$r_i$是A的系列n元序列的集合,集合上n元序列具有关系$r_i$当且仅当n元序列是$r_i$的元素

### 1.2.2 定义 模型
>一个$L^1$**模型**是一个有序对$M=(A,I)$,其中A是一个非空的集合被称为M的**论域**,I被称为**解释**,是一个满足如下条件的函数:
>- 任意$L^1$中的常量$c_i$,$I(c_i)$是A的元素,记为$M[[c_i]]$
>- 任意$L^1$中的n元函数$f_i$,$I(f_i)$是A上的**n元函数**,记为$M[[f_i]]$
>- 任意$L^1$中的n元关系$r_i$,$I(r_i)$是A上的**n元关系**,记为$M[[r_i]]$

### 1.2.3 定义 赋值
>$M=(A,I)$是一个$L^1$**模型**,$M$上的赋值$\sigma$是一个有序对$\sigma=(M,\omega)$,$\omega$是变量到A的函数,$L^1$在$\sigma$的赋值下满足:  
>- $\sigma[[c_i]]=M[[c_i]]$  
>- $\sigma[r_i]=M[[r_i]]$
>- $\sigma[[f_i]]=M[[f_i]]$
>- $\sigma[[x_i]]=\omega(x_i)$  
>    
>$\sigma(a/x_k)$是$M$上的一个赋值,其中$a属于A$:
>- $\sigma(a/x_k)[[t]]=a$若$t=x_k$
>- $\sigma(a/x_k)[[t]]=\sigma[[t]]$若$t \neq x_k$

### 1.2.4 定义 塔尔斯基语义
>$M=(A,I)$上的赋值$\sigma=(M,\omega)$,$\sigma$对$L^1-公式$的**解释**是一个$L^1-公式$到布尔值的映射,可以递归的定义为:  
>对所有的$L_{C,F,R}^1-项$有:
>- 变量$x_i:\sigma[[x_i]]$
>- 常量$c_i:\sigma[[c_i]]$
>- 任意n元$L^1-项$序列$(t_1,...,t_n)$和n元函数$f$:$\sigma[[f(t_1,...,t_n)]]=\sigma[[f]](\sigma[[t_1]],...,\sigma[[t_n]])$
> 
> 对所有的$L_{C,F,R}^1-公式$有:
>- $\sigma[[r(t_1,...,t_n)]]=True$ 当且仅当 $(\sigma[[t_1]],...,\sigma[[t_1]])属于\sigma[[r]]$
>- $\sigma[[\neg \phi]]=True$ 当且仅当 $\sigma[[\phi]]=False$
>- $\sigma[[\phi \vee \psi]]=True$ 当且仅当 $\sigma[[\phi]]=True或\sigma[[\psi]]=True$
>- $\sigma[[\phi \wedge \psi]]=True$ 当且仅当 $\sigma[[\phi]]=True且\sigma[[\psi]]=True$
>- $\sigma[[\phi \Rightarrow \psi]]=True$ 当且仅若 $\sigma[[\phi]]=True则\sigma[[\psi]]=True$
>- $\sigma[[\phi \equiv \psi]]=True$ 当且仅若 $\sigma[[\phi]]=\sigma[[\psi]]$
>- $\sigma[[\forall x \phi]]=True$当且仅当**所有**属于$A$的$a$有$\sigma(a/x)[[\phi]]=True$
>- $\sigma[[\exists x \phi]]=True$当且仅当**存在**属于$A$的$a$有$\sigma(a/x)[[\phi]]=True$
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

### 1.2.9 定理 $L^1$语义的性质
> 1. 若 $\phi \in \Gamma$ 则 $\Gamma \vDash \phi$
> 2. $\phi,\phi \Rightarrow \psi \vDash \psi$
> 3. $\Gamma$不可满足则对所有公式$\phi$有$\Gamma \vDash \phi$
> 4. 若$\Gamma \vDash \phi$且$\phi$与$\psi$逻辑等值则$\Gamma \vDash \psi$
> 5. $\Gamma,\phi \vDash \psi$ 当且仅当 $\Gamma \vDash \phi \Rightarrow \psi$
> 6. $\Gamma,\phi \vDash \psi$ 当且仅当 $\Gamma,\neg \psi \vDash \neg \phi$
> 7. $\Gamma,\phi$不可满足当且仅当$\Gamma \vDash \neg \phi$,$\Gamma,\phi$可满足当且仅当$\Gamma \nvDash \neg \phi$
> 8. $\phi$与$\psi$逻辑等值当且仅当$\phi \vDash \psi$且$\psi \vDash \phi$
> 9. 若$\Gamma,\phi_1,...,\phi_n \vDash \psi$且对任意i有$\Delta \vDash \phi_i$则$\Gamma,\Delta \vDash \psi$
> 10. 若$\Gamma \vDash \phi$且$\phi \vDash \psi$则$\Gamma \vDash \psi$
> 11. 若对任意$1 \le i \le n$有$\Gamma \vDash \phi_i$则$\Gamma \vDash \phi_1 \wedge ... \wedge \phi_n$
> 12. $\Gamma,\phi_1,...,\phi_n \vDash \psi$当且仅当   $\Gamma,\phi_1 \wedge ... \wedge \phi_n \vDash \psi$
> 13. $\vDash \phi \wedge \psi$当且仅当$\vDash \phi$且$\vDash \psi$
> 14. $\vDash \phi \vee \psi$当且仅当$\vDash \phi$或$\vDash \psi$  
> 15. 若$\vDash \phi \equiv \psi$则$\vDash \phi$当且仅当$\vDash \psi$  
> 16. $\vDash \phi \equiv \psi$当且仅当 $\vDash \phi \Rightarrow \psi$且$\vDash \psi \Rightarrow \phi$

>证:
>大部分证明是由语义定义平凡得到的,我们证  
>7. 若$\Gamma,\phi$不可满足那么不存在赋值$\sigma[[\Gamma]]=True且\sigma[[\phi]]=True$,那么对所有赋值🈶️$\sigma[[\phi]]=False$既对所有赋值$\sigma[[\neg \phi]]=True$,平凡的有$\Gamma \vDash \neg \phi$.  
若$\Gamma,\phi$可满足那么存在赋值$\sigma[[\Gamma]]=True且\sigma[[\phi]]=True$,那么存在赋值$\sigma[[\Gamma]]=True且\sigma[[\neg \phi]]=True$既$\Gamma \nvDash \neg \phi$.

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
>- $L^1-项 t_1,...,t_n$和n元关系$r$,$r(t_1,...,t_n)$称为**原子公式**
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
>- 任意赋值$\sigma$有$\sigma \vDash \phi_{t/x}<t/x>$当且仅当$\sigma(\sigma[[t]]/x) \vDash \phi$
>- $\forall x \phi \vDash \phi_{t/x}<t/x>$
>- $\phi_{t/x}<t/x> \vDash \exists x \phi$

## 4 $L^1$的演绎$H^{L^1}$
跟$L^0$的$H^0$演绎一样,我们可以通过定义建立**公理系统**,采用演绎的形式得到**逻辑蕴涵**、**逻辑有效式**和**逻辑等值**而避免**穷举赋值**,我们将选定**逻辑有效式**和**操作**作为**规则(rule)**,并讨论这么选择和做法的性质,主要包括**紧致性**,我们限制$L^1$的量词为$\forall$以及**逻辑联结词**为$\neg$和$\Rightarrow$,事实上,所有其他逻辑联结词形成的公式的语义总可以与用以上逻辑联结词构成的公式相同:
>- $\sigma[[\phi \vee \psi]]=\sigma[[\neg \phi \Rightarrow \psi]]$
>- $\sigma[[\phi \wedge \psi]]=\sigma[[\neg (\phi \Rightarrow 
\neg \psi)]]$  
>- $\sigma[[\phi \equiv \psi]]=\sigma[[(\phi \Rightarrow 
\psi) \wedge (\psi \Rightarrow 
\phi)]]$
>- $\sigma[[\exists x \phi]]=\sigma[[\neg (\forall x \neg \phi)]]$  
因此限制后的$L^1$跟原$L^1$的**表达能力**是完全相同的,其相关性质也是相同的,后面会更详细的描述.

### 4.1 $H^{L^1}$相关定义

### 4.1.1 定义 操作(operator)
> 从一个公式或多个公式得到另外一个公式的动作称为**操作**

### 4.1.2 $H_r^{L^1}$ 公理系统
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

可以看出若$H^{L^1}$具有**完全性、紧致性**,则其所有的**逻辑蕴涵**、**逻辑等值**、**逻辑有效**关系是**可判定**的.

### 4.2 $H^{L^1}$性质
### 4.2.1 定义 分离操作(modus ponens)
>从$\phi,\phi \Rightarrow \psi$得到$\psi$的动作称为**分离**,简记分离操作为MP
### 4.2.2 定义 $r_1$规则
>$$r_0=MP$$
>$$r_1=\begin{cases}
    r_0 \\
    1:\phi \Rightarrow (\psi \Rightarrow \phi) \\
    2:(\phi \Rightarrow (\psi \Rightarrow \chi))\Rightarrow ((\phi \Rightarrow \psi) \Rightarrow (\phi \Rightarrow \chi))\\
    3:(\neg \phi \Rightarrow \psi) \Rightarrow ((\neg \phi \Rightarrow \neg \psi) \Rightarrow \phi)\\
\end{cases}$$  

### 4.2.3 $H_{r_1}^1$相关定理
对$H_{r_1}^1$下的公式集合$\Gamma 、\Delta$,公式$\phi、\psi、\chi$
> 1. SUB(子集,subset):若$\Gamma \vdash \phi$则存在$\Gamma$的**有穷子集**$\Delta$有$\Delta \vdash \phi$
> 2. SUP(父集,superset):若$\Gamma \vdash \phi$且$\Delta$是$\Gamma$的子集则$\Delta \vdash \phi$
> 3. CUT (剪切定理): 若$\Gamma,\phi_1,...\phi_n \vdash \psi$且$\Delta \vdash \phi_i,i \leq m$则$\Gamma \cup \Delta \vdash \psi$
> 4. Tran (传递性,transitivity):若$\Gamma \vdash \phi,\phi \vdash \psi$则$\Gamma \vdash \psi$
> 5. MP (分离定理,肯定前件,modus ponens):若$\Gamma \vdash \phi,\Gamma \vdash \phi \Rightarrow \psi$则$\Gamma \vdash \psi$
> 6. DT (演绎定理,deduction theorem):若$\Gamma,\phi \vdash \psi$则$\Gamma \vdash \phi \Rightarrow \psi$
> 7. HS (假言三段论,hypothetical syllogism):若$\Gamma \vdash \phi \Rightarrow \psi,\Delta \vdash \psi \Rightarrow \chi$则$\Gamma \cup \Delta \vdash \phi \Rightarrow \chi$
> 8. IE (非一致性效应,inconsistency effect):若$\Gamma \vdash \phi,\Gamma \vdash \neg \phi$则$\Gamma \vdash \psi$,若$\Gamma,\phi \vdash \neg \phi$则$\Gamma ,\phi,\vdash \psi$  
> 9. SRAA (简单归谬律,简单反证法,simple reductio ad absudrum):若$\Gamma,\neg \phi \vdash \phi$则$\Gamma \vdash \phi$,若$\Gamma,\phi \vdash \neg \phi$则$\Gamma \vdash \neg \phi$
> 10. RAA (归谬律,反证法, reductio ad absudrum):$\Gamma \vdash \phi$当且仅当$\Gamma , \neg \phi \vdash \psi,\Gamma ,\neg \phi \vdash \neg \psi$
> 11. DN (双重否定,dounble neg):$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$,$\Gamma,\psi\vdash \phi$当且仅当$\Gamma,\neg \neg \psi \vdash \phi$
> 12. Contrap (假言对位):$\Gamma ,\phi \vdash \psi$当前仅当$\Gamma,\neg \psi \vdash \neg \phi$,$\Gamma ,\phi \vdash \neg \psi$当前仅当$\Gamma,\psi \vdash \neg \phi$    


>证明:  
> (8)若$\Gamma \vdash \phi,\Gamma \vdash \neg \phi$则$\Gamma \vdash \psi$ @    
> 1:$\phi,\neg \phi \vdash \psi$@  
>> 1.1:$\neg \phi \Rightarrow (\neg \psi \Rightarrow \neg \phi)$#$r_1.1$  
>> 1.2:$\neg \phi$#hyp  
>> 1.3:$\neg \psi \Rightarrow \neg \phi$#$MP(1.1,1.2)$  
>> 1.4:$\phi \Rightarrow (\neg \psi \Rightarrow \phi)$#$r_1.1$  
>> 1.5:$\phi$#hyp  
>> 1.6:$\neg \psi \Rightarrow \phi$#$MP(1.4,1.5)$  
>> 1.7:$(\neg \psi \Rightarrow \phi) \Rightarrow ((\neg \psi \Rightarrow \neg \phi) \Rightarrow \psi)$#$r_1.3$  
>> 1.8:$(\neg \psi \Rightarrow \neg \phi) \Rightarrow \psi$#$MP(1.6,1.7)$  
>> 1.9:$\psi$#MP(1.8,1.3)   
>>
> 2:$\Gamma \vdash \phi$@hyp   
> 3:$\Gamma \vdash \neg \phi$@hyp   
> 4:$\Gamma \vdash \psi$@CUT(1,2,3)     
> 
> (9) 若$\Gamma,\neg \phi \vdash \phi$则$\Gamma \vdash \phi$@  
> 1: $\vdash \phi \Rightarrow \phi$@  
>> 1.1:$\phi \Rightarrow ((\phi \Rightarrow \phi) \Rightarrow\phi))$#$r_1$  
>> 1.2:$(\phi \Rightarrow ((\phi \Rightarrow \phi) \Rightarrow\phi)) \Rightarrow ((\phi \Rightarrow(\phi \Rightarrow \phi)) \Rightarrow(\phi \Rightarrow \phi))$#$r_1$  
>> 1.3:$(\phi \Rightarrow (\phi \Rightarrow \phi)) \Rightarrow (\phi \Rightarrow \phi)$#MP(1.1,1.2)  
>> 1.3:$\phi \Rightarrow (\phi \Rightarrow \phi)$#$r_1$  
>> 5:$\phi \Rightarrow \phi$#MP(3,4)     
>>  
> 2:$\neg \phi \Rightarrow \phi \vdash \phi$@
>> 2.1:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \phi$@
>>> 2.1.1: $\neg \phi \Rightarrow  \phi$#假设  
>>> 2.1.2: $\neg \phi$#假设  
>>> 2.1.3: $\phi$#MP(2.1.1,2.1.2)
>>> 
>> 2.2:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \neg (\neg \phi \Rightarrow \phi)$@IE(2.1)  
>> 2.3:$\neg \phi \Rightarrow \phi,\neg \phi \vdash \neg \phi \Rightarrow \phi$@IE(2.1)  
>> 2.4:$\neg \phi \Rightarrow \phi \vdash \neg \phi \Rightarrow \neg (\neg \phi \Rightarrow \phi)$@DT(2.2)  
>> 2.5:$\neg \phi \Rightarrow \phi \vdash \neg \phi \Rightarrow (\neg \phi \Rightarrow \phi)$@DT(2.3)   
>> 2.6:$\neg \phi \Rightarrow \neg (\neg \phi \Rightarrow \phi),\neg \phi \Rightarrow (\neg \phi \Rightarrow \phi) \vdash \phi$@DT($r_1.3$)  
>> 2.7: $\neg \phi \Rightarrow \phi \vdash \phi$@CUT(2.4,2.5,2.6)
>>  
>3:$\Gamma,\neg \phi \vdash \phi$#假设  
>4:$\Gamma \vdash \neg \phi \Rightarrow \phi$#DT(3)  
>5:$\Gamma \vdash \phi$#CUT(2,4)
>
> (11)$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$@  
> 1:若$\Gamma \vdash \phi$则$\Gamma \vdash \neg \neg \phi$@
> > 1.1: $\phi ,\neg \phi \vdash \neg \neg \phi$@  
> > > 1.1.1: $(\neg \phi \Rightarrow \phi) \Rightarrow (\neg \phi \Rightarrow \neg \phi) \Rightarrow \neg \neg \phi$#$r_1.3$  
> > > 1.1.2: $\neg \phi \Rightarrow (\neg \phi \Rightarrow \neg \phi)$#$r_1.1$  
> > > 1.1.3: $\neg \phi \Rightarrow (\phi \Rightarrow \neg \phi)$#$r_1.1$  
> > > 1.1.4: $\neg \phi \Rightarrow \neg \phi$#MP(hyp,1.1.2)  
> > > 1.1.5: $\neg \phi \Rightarrow  \phi$#MP(hyp,1.1.3)  
> > > 1.1.6: $\neg \neg \phi$#MP(MP(1.1.1,5),1.1.4)
> > >
> > 1.2:$\phi \Rightarrow \neg \neg \phi$@SRAA(1.1)  
> > 1.3:$\Gamma \vdash \neg \neg \phi$@CUT(hyp,1.2)
> >
> 2:若$\Gamma \vdash \neg \neg \phi$则$\Gamma \vdash \phi$@
> > 同理
> >
> 3:$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \neg \neg \phi$@1,2
>
>(12) $\Gamma ,\phi \vdash \psi$当前仅当$\Gamma,\neg \psi \vdash \neg \phi$@  
> 1:若$\Gamma ,\phi \vdash \psi$则$\Gamma,\neg \psi \vdash \neg \phi$#  
>> 1.1:$\Gamma ,\phi ,\neg \psi \vdash \neg \phi$#IE(hyp)  
>> 1.2:$\Gamma ,\neg \psi \vdash \neg \phi$#SRAA(1.1)  
>> 1.3:$\Gamma \vdash \neg \psi \Rightarrow \neg \phi$DT(1.2)
>>
> 其他类似

### 4.2.3 $r_2规则$
$r_1$未包括量化规则,$r_2$填上了相关公里
>$$r_2=
\begin{cases}
  r_1  \\
  4:\forall x(\phi \Rightarrow \psi) \Rightarrow (\forall \phi \Rightarrow \forall \psi) \\
  5:\forall x \phi_{t/x} \Rightarrow \phi_{t/x}<t/x> \\
  6:\phi_{+x} \Rightarrow \forall x \phi_{+x} \\ 
  7: \forall x_1,...,x_n \phi,\phi为任意r_2公理
\end{cases}
>$$

### 4.2.3 $H_{r_2}^{L^1}$相关定理
$H_{r_2}^{L^1}$除了$H_{r_1}^{L^1}$相关定理,还包含一些量化相关的定理
> 1. QV(量化变量,quantify variable,变量概括):  
> - 若$\Gamma_{+x} \vdash \phi$则$\Gamma_{+x} \vdash \forall x \phi$  
> - 若$\Gamma_{+x},\phi \vdash \psi_{+x}$则$\Gamma_{+x}, \exists x \phi \vdash \psi_{+x}$  
> - 若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\forall x \phi \vdash \forall x \psi$  
> - 若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\exists x \phi \vdash \exists x \psi$、
> 2. RE(置换,replace element):  
> - $\forall \bf{x}(\phi_{\bf{t}/\bf{x}} \equiv \psi_{\bf{t}/\bf{x}}) \vdash \chi<\phi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p> \equiv \chi<\psi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p>$   
> - 若$\Gamma \vdash \forall \bf{x}(\phi_{\bf{t}/\bf{x}} \equiv \psi_{\bf{t}/\bf{x}})$则$\Gamma \vdash \chi<\phi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p> \equiv \chi<\psi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p>$
> - 若$\Gamma_{+\bf{x}} \vdash \phi_{t/x} \equiv \psi_{t/x}$则$\Gamma \vdash \chi<\phi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p> \equiv \chi<\psi_{\bf{t}/\bf{x}}<\bf{t}/\bf{x}>/p>$
> - 若$\Gamma \vdash \phi \equiv \psi$则$\Gamma \vdash \chi<\phi/p> \equiv \chi<\psi/p>$
> 3. CV(变化变量,change variable,变量易字):  
> - $\forall x \phi_{y/x,+y} \vdash \forall y \phi_{y/x,+y}<y/x>$ 且 $\forall y \phi_{y/x,+y}<y/x> \vdash \forall x \phi_{y/x,+y}$   
> - $\exists x \phi_{y/x,+y}\vdash \exists y \phi_{y/x,+y}<y/x>$且$\exists y \phi_{y/x,+y}<y/x> \vdash \exists x \phi_{y/x,+y}$
> - $\phi$及其易字变形$\phi^\prime$有:$\Gamma \vdash \phi$当且仅当$\Gamma \vdash \phi^\prime$,$\Gamma,\phi \vdash \psi$当且仅当$\Gamma,\phi^\prime \vdash \psi$
> - $\vdash \phi \equiv \phi_{t/x}$
> - $\vdash \forall x \phi \Rightarrow \phi_{t/x}<t/x>$
> - $\vdash \phi_{t/x}<t/x> \Rightarrow \exists x \phi$
> 4. QC(量化常量,quantify constant,常量概括):
> - 若$\Gamma_{-c} \vdash \phi_{-c}<c/x>$则$\Gamma_{-c} \vdash \forall x \phi_{-c}$
> - 若$\Gamma_{-c},\phi_{-c}<c/x> \vdash \psi_{-c}$则$\Gamma_{-c},\exists x \phi_{-c}\vdash \psi_{-c}$
> - 若$\Gamma_{-c},\phi_{-c}<c/x> \vdash \psi_{-c}<c/x>$则$\Gamma_{-c},\forall x \phi_{-c}\vdash \forall x \psi_{-c}$
>  - 若$\Gamma_{-c},\phi_{-c}<c/x> \vdash \psi_{-c}<c/x>$则$\Gamma_{-c},\exists x \phi_{-c}\vdash \exists x \psi_{-c}$

>证:  
>(1)  
> 1: 若$\Gamma_{+x} \vdash \phi$则$\Gamma_{+x} \vdash \forall x \phi$ @
>>由假设$\phi_0,...,\phi_n$是$\Gamma_{+x}$到$\phi$的演绎。首先证明对任意$\phi_i$,有$\forall x \phi_i$可从$\Gamma_{+x}$演绎.释归纳于i,(1)$\phi_i$是公理,由$r_2.7$可知$\phi_i$.(2)$\phi_i$属于$\Gamma_{+x}$,由$r_2.6$可知$\forall x \phi_i$可从$\Gamma_{+x}$演绎.(3)由演绎和MP的定义，存在$j,k\le i,\phi_k: \phi_j \Rightarrow \phi_i$,根据归纳假设$\forall x \phi_k = \forall \phi_j \Rightarrow \phi_i$可演绎，$\forall x \phi_j$可演绎，因此由$r_2.4$、DT、CUT可知$\forall x \phi_j$可演绎。由上述证明和假设可知$\Gamma_{+x} \vdash \forall x \phi$   
>> 
> 2: 若$\Gamma_{+x},\phi \vdash \psi_{+x}$则$\Gamma_{+x},\exists \phi \vdash \psi_{+x}$ @  
>>1.1: $\Gamma_{+x},\phi \vdash \psi_{+x}$ @ hyp  
>>1.2: $\Gamma_{+x},\neg \psi_{+x} \vdash \neg \phi$ @ Contrap(1.1)  
>>1.3: $\neg \phi_{+x} \vdash \forall x \neg \phi_{+x}$@DT($r_2.6$)   
>>1.4: $\Gamma_{+x},\neg \psi_{+x} \vdash \forall x \neg \phi$@ CUT(1.3)  
>>1.5: $\Gamma_{+x},\neg  \forall x \neg \phi \vdash \psi_{+x}$ @Contrap(1.4)
>>
> 3:若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\forall x \phi \vdash \forall x \psi$@
>> 3.1:$\forall x \phi \vdash \phi$@DT($r_2$.5)  
>> 3.2:$\Gamma_{+x},\forall x \phi \vdash \phi$@SUP(3.1)  
>> 3.3:$\Gamma_{+x},\phi \vdash \psi$#hyp  
>> 3.4:$\Gamma_{+x},\forall x \phi \vdash \psi$#CUT(3.2,3.3)    
>> 3.5:$\Gamma_{+x},\forall x \phi \vdash \forall x \psi$@1(3.4)  
>>
>4 :若$\Gamma_{+x},\phi \vdash \psi$则$\Gamma_{+x},\exists x \phi \vdash \exists x \psi$@
>> 4.1:$\Gamma_{+x},\neg \psi \vdash \neg \phi$@Contrap(hyp)  
>> 4.2:$\Gamma_{+x},\forall x \neg \psi \vdash \forall x \neg \phi$@3(4.1)  
>> 4.3:$\Gamma_{+x},\neg \forall x \neg \phi \vdash \neg \forall x \neg \psi$@Contrap(4.2)

### 4.2.4 定理 $H_r^{L^1}$的可靠性
>$H_{r_0}^{L^1}$具有可靠性,任意包含$r_0$的规则$r,H_r^{L^1}$具有可靠性

>证:  
>设$\phi_1,...,\phi_n$是从$\Gamma$到$\phi_n$的演绎.施归纳于n我们证$\Gamma \vDash \phi_n$:(1)$\phi_n$属于$r$的公理,那么$\phi_n$是**逻辑有效式**$\Gamma \vDash \phi_n$.(2)$\phi_n$属于$\Gamma$,根据**逻辑蕴涵**的定义$\Gamma \vDash \phi_n$(3)存在$i,j\le n,\phi_j=\phi_i \Rightarrow \phi_n$,有归纳假设$\Gamma \vDash \phi_i$,$\Gamma \vDash \phi_j$,由语义定义
$\Gamma \vDash \phi_n$.由题设，存在$\phi_1,...,\phi_n$是从$\Gamma$到$\phi$的演绎,因此$\Gamma \vDash \phi$  
>证明只采用了MP规则和语义定义,不依赖于具体公理,因此任意包含$r_0$的规则$r,H_r^1$具有可靠性

### 4.2.5 定理 $H_r^{L^1}$的一致性
>$H_{r_0}^1$具有一致性,任意包含$r_0$的规则$r,H_r^1$具有一致性

>证:  
>若$H_{r_0}^{L^1}$的不一致,根据定义存在$\phi$有$\vdash \phi$,$\vdash \neg \phi$,由4.2.5 定理,$\Gamma \vDash \phi$,$\Gamma \vDash \neg \phi$ 由语义定义这是不可能的.  
>证明只采用了MP规则和语义定义,不依赖于具体公理,因此任意包含$r_0$的规则$r,H_r^{L^1}$具有一致性

为了后面的证明,我们指出一些有用的引理,这些引理不是为了导出演绎过程的定理，而是用于证明演绎性质的定理.

### 4.2.6 定理 一致性定理
>设$r$包含$r_1$规则,则在$H_r^{L^1}$系统下有
>1. $\Gamma \vdash \neg \phi$当且仅当$\Gamma ,\phi 不一致$
>2. 若$\Gamma$一致则$\Gamma$与$\phi$一致或$\Gamma$与$\neg \phi$一致
>3. $\Gamma$与$\phi$一致当且仅当 $\Gamma$与$\neg \neg \phi$一致
>4. $\Gamma$ 不一致当且仅当对任意属于$\Gamma$的$\phi$有$\Gamma - \{\phi\} \vdash \neg \phi$
>5. $\Gamma,\phi \Rightarrow \psi$ 一致 当且仅当 $\Gamma,\neg \phi$一致或 $\Gamma,\psi$ 一致
>6. 若$\Gamma_{-y}$与$\neg \forall x \phi_{-y}$一致则$\Gamma_{-y}$与$\neg \phi_{-y}<y/x>$一致
>7. 若$\Gamma_{-c}$与$\neg \forall x \phi_{-c}$一致则$\Gamma_{-c}$与$\neg \phi_{-c}<c/x>$一致

>证:  
>1. 若$\Gamma \vdash \neg \phi$则$\Gamma,\phi \vdash \neg \phi$，再由$\Gamma,\phi \vdash \phi$因此$\Gamma ,\phi$不一致.  
若$\Gamma ,\phi$不一致则$\Gamma ,\phi \vdash \neg \phi$由SRAA知$\Gamma \vdash \neg \phi$
>2. 若$\Gamma$一致,假设$\Gamma$与$\phi$不一致且$\Gamma$与$\neg \phi$不一致,那么由1由$\Gamma \vdash \neg \phi$且$\Gamma \vdash \phi$,既$\Gamma$不一致,矛盾.
>3. 若 $\Gamma$与$\neg \neg \phi$一致,设$\Gamma$与$\phi$不一致,由1有$\Gamma \vdash \neg \phi$, 由DN有$\Gamma \vdash \neg \neg \neg \phi$,由DN$\Gamma$与$\neg \neg \phi$不一致，矛盾.  
若$\Gamma$与$\phi$一致,假设$\Gamma$与$\neg \neg \phi$不一致,连续两次使用1得到$\Gamma$与$\phi$不一致,矛盾.
>4. 若$\Gamma$不一致则$\Gamma - \{\phi\},\phi \vdash \neg \phi$,由SRAA$\Gamma - \{\phi\} \vdash \neg \phi$.  
若对任意属于$\Gamma$的$\phi$有$\Gamma - \{\phi\} \vdash \neg \phi$则$\Gamma - \{\phi\},\phi \vdash \neg \phi$,又有$\Gamma - \{\phi\},\phi \vdash \phi$,因此$\Gamma$不一致
>5. 若$\Gamma,\phi \Rightarrow \psi$一致,假设$\Gamma,\neg \phi$不一致且 $\Gamma,\psi$ 不一致则由1可知$\Gamma \vdash \phi$且 $\Gamma \vdash \neg \psi$,由CUT可得$\Gamma,\phi \Rightarrow \psi \vdash \psi$且$\Gamma,\phi \Rightarrow \psi \vdash \neg \psi$,矛盾.    
若$\Gamma,\neg \phi 或 \Gamma,\psi$一致,假设$\Gamma,\phi \Rightarrow \psi$不一致,则$\Gamma,\phi \Rightarrow \psi \vdash \phi$且$\Gamma,\phi \Rightarrow \psi \vdash \neg \psi$,另一方面$\neg \phi \vdash \phi \Rightarrow \psi$且$\psi \vdash \phi \Rightarrow \psi$,由CUT我们有$\Gamma , \neg \phi \vdash \phi$且$\Gamma ,  \psi \vdash \neg \psi$,既$\Gamma,\neg \phi$不一致 且 $\Gamma,\psi$不一致,矛盾.

### 4.2.7 定义 可数的$L^1$语言
> 若$L^1$所有的项和公式,存在自然数到其的一一映射，我们称这样的$L^1$语言为可数的$L^1$语言

前面的描述，没有限制$L^1$,因此可能存在不能与自然数一一对应的公式和项，我们将限制$L^1$为可数的语言（直觉上这需要限制C,F,R为可数集合),**后面的描述都针对可数的**$L^1$**语言**

为了证明完全性和紧凑性，仿照**henkin**的思路  
直觉上,若$\Gamma \vDash \phi$,假设$\Gamma \nvdash \phi$,由4.6.2.1可知$\Gamma,\neg \phi$一致,假如$\Gamma,\neg \phi$可满足，则与$\Gamma \vDash \phi$矛盾了,直觉上$\Gamma,\neg \phi$一致则可满足,这样就证明了完全性.完整的描述如下

### 4.2.8 定理 完全性的等价描述
> 对所有公式集$\Gamma$有若$\Gamma \vDash \phi$则$\Gamma \vdash \phi$当且仅当所有一致的公式集可满足

>证:  
>如果对所有公式集有若$\Gamma \vDash \phi$则$\Gamma \vdash \phi$且$\Delta$是一致的,假设$\Delta$不可满足,则由1.2.9.3$\Delta \vDash \phi$且$\Delta \vDash \neg \phi$因此$\Gamma \vdash \phi$且$\Gamma \vdash \neg \phi$与$\Delta$一致矛盾.
反过来如果所有一致的公式集可满足且$\Gamma \vDash \phi$,假设$\Gamma \nvdash \phi$,由4.6.2.1可知$\Gamma,\neg \phi$一致,因此$\Gamma,\neg \phi$可满足,由1.2.9.7$\Gamma \nvDash \phi$与$\Gamma \vDash \phi$矛盾.

上述定理描述了语义和演绎的关系,接下来就是如何证明直觉上的**所有一致的公式集可满足**,其关键在于**构造一个赋值**.同时,直接证明**所有一致的公式集可满足**中的**所有**,需要构造所有对应的赋值,真很困难.若我们能找到一个包含所有一致集合的集合,对这个集合构造赋值,那么等于构造了一个适用于所有公式集的赋值.我们接下来更严格的描述这个构想.

### 4.2.9 定义 极大一致集
> $\Gamma$是**极大一致集**当且仅当:
> 1. $\Gamma$是一致的
> 2. 任何一致的公式集合$\Delta$,若$\Gamma 属于 \Delta$则$\Gamma=\Delta$

### 4.2.10 定理 极大一致集的性质    
> 1. $\Gamma$ **极大一致**当且仅当$\Gamma$一致且对任意$\phi$有$\phi \in \Gamma$或$\neg \phi \in \Gamma$
> 2. 若$\Gamma$**极大一致**则对任意$\phi$有$\Gamma \vdash \phi$当前仅当$\phi \in \Gamma$
> 3. 若$\Gamma$**极大一致**则$\phi \in \Gamma$当且仅当$\neg \phi \notin \Gamma$
> 4. 若$\Gamma$**极大一致**则$\phi \Rightarrow \psi \in \Gamma$当且仅当$\phi \notin \Gamma$或$\psi \in \Gamma$

现在,我们先证明一个简单的命题逻辑公理体系$H_{r_2}^{L_{P,F_1}^0}$的完全性.先前的4.2.3、4.2.6和4.2.10相关定理同样适用于它.为了使用**数学归纳法**我们引入**公式复杂度**的概念

### 4.2.11 $L_{P,F_1}^0$ 的公式复杂度
> $L_{P,F_1}^0$公式$\phi$的复杂度$deg(\phi)$被递归的定义为:
> - 若$\phi$是命题变量则$deg(\phi)=0$
> - 若$\phi$是$\neg \psi$则$deg(\phi)=deg(\psi)+1$
> - 若$\phi$是$\psi \Rightarrow \chi$则$deg(\phi)=max(deg(\psi),deg(\chi))+1$

### 4.2.12 定理 $H_{r_2}^{L_{P,F}^0}$极大一致集扩充定理
>设P可数,$H_{r_2}^{L_{P,F}^0}$中的一致集可扩充为极大一致集

>证:
> 因为P可数,因此$L_{P,F_1}^0$可数,可以将$L_{P,F_1}^0$的公式排列为$\phi_1,\phi_2,...$,设$\Gamma$为一致集,令$\Gamma_1=\Gamma$,由4.2.6.2我们可以递归的构建
> $$\Gamma_{i+1}= 
\begin{cases}
    \Gamma_i \cup \{\phi \}若\phi 与 \Gamma一致 \\
    \Gamma_i \cup \{\neg \phi \}若\neg \phi 与 \Gamma一致 \\
\end{cases}
> $$  
>由4.2.6知则$\cup_{i=1}^\infty \Gamma_i$是极大一致集,假设不一致,由一致性定理存在有穷子集$\{\psi_1,...,\psi_n\}$不一致,对每一个$\psi_i$,其对应$\phi_1,\phi_2,...$序列中的$\phi_j$,因此按定义$\psi_i \in \Gamma_j$,取$\{\psi_1,...,\psi_n\}$中对应最大的$\phi_k$则$\{\psi_1,...,\psi_n\} \in \Gamma_k$,既$\{\psi_1,...,\psi_n\}$是一致的,矛盾.

### 4.2.13 定理 $H_{r_2}^{L_{P,F}^0}$满足定理
> $H_{r_2}^{L_{P,F}^0}$的任意一致集$\Gamma$可满足

> 证:
> 由4.2.12 $\Gamma$可扩充为极大一致集$\Gamma^\prime$,由4.2.10任意命题$p_i$或$p_i \in \Gamma^\prime$或$\neg p_i \in \Gamma^\prime$,因此我们可以合法构造如下赋值
> $$\sigma[[p_i]]=\begin{cases}
    True 若 p_i \in \Gamma^\prime \\
    False 若 \neg p_i \in \Gamma^\prime
\end{cases}$$
>我们对 $\Gamma^\prime$公式以公式**复杂度**施**归纳法**,证明任意复杂度的公式$\phi \in \Gamma^\prime$有$\sigma[[\phi]]=True$既$\sigma \vDash \Gamma^\prime$
> $deg(\phi)=0$时,$\phi$是明天变量,按$\sigma$定义可知$\sigma[[p_i]]=True$
> 按归纳复杂度$i \le n$的所有公式$\phi \in \Gamma$当且仅当$\sigma[[\phi]]=True$,设$\psi \in \Gamma$复杂度为n+1:
> - $\psi =\neg \phi$其中$\deg(\phi)=n$:
> $$\begin{aligned}
&\sigma[[ \psi]]= True \\
&当且仅当 \sigma[[ \phi]]=False(语义) \\
&当前仅当 \phi \notin  \Gamma^\prime(归纳)  \\
&当前仅当 \neg \phi \in  \Gamma^\prime(4.2.10)  \\
&当前仅当 \psi \in  \Gamma^\prime
\end{aligned}$$
> 因此由题设$\sigma [[\psi]]= True$
> - $\psi = \phi_1 \Rightarrow \phi_2$,其中$max(deg(\phi_1),deg(\phi_2))=n$:
> $$\begin{aligned}
    &\sigma[[\psi]]= True \\
    &当且仅当 \sigma[[\phi_1]]=False 或 \sigma[[\phi_2]]=True (语义) \\
    &当且仅当 \neg \phi_1 \in \Gamma^\prime 或  \phi_2 \in \Gamma^\prime (归纳) \\
    &当且仅当 \phi_1 \Rightarrow \phi_2 \in \Gamma^\prime (4.2.6)\\
    &当且仅当 \psi \in \Gamma^\prime
\end{aligned}$$
> 因此由题设$\sigma [[\psi]]= True$

仿照上述思路,$H_{r_2}^{L_{C,F,R}^1}$应该也可如此构造**赋值**,对比于$L^0$,$L^1$细化了命题的内部结构以及引入了**量化**,因此仿照上述证明我们首先应该确保赋值使原子公式(相当于$L^0$的命题)满足:
$$\sigma[[r(t_1,...t_2)]]\begin{cases}
    &= True (或 \sigma[[t_1]],...,\sigma[[t_n]] \in \sigma[[r]])若r(t_1,...,t_n) \in \Gamma^\prime \\
    &= False (或 (\sigma[[t_1]],...,\sigma[[t_n]] \notin \sigma[[r]])若\neg r(t_1,...,t_n) \in \Gamma^\prime 
\end{cases}
$$
为了满足这个要求,我们可以很自然的定义$\sigma$的**论域**为所有项既$A=\{t:t是 \Gamma^\prime的项 \}$,同时定义**模型**和**变量赋值**为它们的**符号**,我们严格的定义如下

### 4.2.14 定义 极大一致集$\Gamma$的符号赋值$\sigma_{\Gamma}$
> 我们定义$\sigma_{\Gamma} = (A,M,\omega)$,其中$A=\{t:t是 \Gamma的项 \}$,模型和变量赋值分别为:
>$$\begin{aligned}
&常量c:\sigma[[c]]=c \\
&变量x:\sigma[[x]]=x \\
&函数f:\sigma[[f]](\sigma[[t_1],...,\sigma[[t_n]])=f(\sigma[[t_1],...,\sigma[[t_n]]) = f(t_1,...,t_n)\\
&关系r:(\sigma[[t_1],...,\sigma[[t_n]) \in \sigma[[r]] 当前仅当 r(t_1,...,t_n) \in \Gamma
\end{aligned}$$
>这样定义是合理的,所有$f$在$A$上闭合,因为$f(t_1,...,t_n)$是$A$上的项.

如此定义的赋值可以从4.2.13知道,极大一致集$\Gamma^\prime$下的该赋值使得形如$P(t_1,...,t_n)$,$\neg \phi$,$\phi \Rightarrow \psi$的公式为真,现在只剩下$\forall x \phi$这样的公式是否为真,以及如何扩展为极大一致集.此时我们发现，虽然可以用4.2.12的方法扩展$\Gamma$为极大一致集$\Gamma^\prime$,但这样得到的$\sigma_{\Gamma^\prime}$不能满足$\Gamma^\prime$.我们的目标是$\sigma_{\Gamma^\prime}[[\forall x \phi]]=True$:
$$\begin{aligned}
&\sigma_{\Gamma^\prime}[[\forall x \phi]]=True (目标) \\
&当且仅当 所有a属于A有 \sigma(a/x)[[ \phi]]=True (语义) \\
&当且仅当 所有t属于 \Gamma^\prime的项有\sigma(t/x)[[\phi]]=True (\sigma_{\Gamma^\prime}定义) \\
&当且仅当 所有t属于 \Gamma^\prime的项有\sigma(\sigma[[t]]/x)[[\phi]]=True (\sigma_{\Gamma^\prime}定义) \\
&当且仅当 所有t属于 \Gamma^\prime的项有\sigma[[\phi_{t/x}<t/x>]] (3.9)
\end{aligned}$$
因此我们不仅要扩展$\Gamma^\prime$到一致极大集,还需要满足$所有t属于 \Gamma^\prime的项有\sigma[[\phi_{t/x}<t/x>]]=True$,既仅仅扩展公式集是不够的,为此引入**膨胀**的定义

### 4.2.15 定义 膨胀
> $L^1$语言$L_{C^\prime,F^\prime,R^\prime}$是$L_{C,F,R}$的**膨胀**当且仅当$C \in C^\prime,F \in F^\prime,R \in R^\prime$,其中$L_{C,F,R}$被称为$L_{C^\prime,F^\prime,R^\prime}$的**规约**  
> 设$L_{C^\prime,F^\prime,R^\prime}、L_{C,F,R}$的某个模型分别为$M^\prime、M$,$M^\prime$为$M$的**膨胀**当前仅当对所有$C,F,R$的元素$\alpha$有$M^\prime[[\alpha]]=M[[\alpha]]$,其中$M$被称为$M^\prime$的**规约**  
> 设$M^\prime、M$上的赋值分别为$\sigma^\prime、\sigma$,$\sigma^\prime$称为$\sigma$的**膨胀**当前仅当对所有的$C,F,R$元素及变量$\alpha$有$\sigma^\prime[[\alpha]]=\sigma[[\alpha]]$,其中$\sigma$被称为$\sigma^\prime$的**规约**  

从定义上可知,我们不仅可以扩展公式集,同时还可以扩展$C,F,R$,然后基于它们构建出赋值$\sigma$,最后用$\sigma$的规约作为原语言的赋值.构建的新语言及赋值需要满足$\sigma_{\Gamma^\prime}[[\forall x \phi]]=True 当且仅当 所有t属于 \Gamma的项有\sigma[[\phi_{t/x}<t/x>]]=True$按照$\sigma$的**定义**这要求$\forall x \phi \in \Gamma 当前仅当 所有t属于 \Gamma的项有\phi_{t/x}<t/x> \in \Gamma$,构建所有正例过于繁琐,我们将构建满足**逆否命题**的集来满足。


### 4.2.16 定义 Henkin集
> 1. 设$\neg \forall x \phi \in \Gamma$,称$\neg \forall x \phi$在$\Gamma$有 **见证(witnessing)** 当且仅当存在一个项$\neg \phi_{t/x}<t/x> \in \Gamma$
> 2. $\Gamma$是**见证全集(witnessing total set)**当前仅当每一个 $\neg \forall x \phi \in \Gamma$,$\neg \forall x \phi$有**见证**
> 3. $\Gamma$是**Henkin**集当且仅当$\Gamma$是**见证全集**且是**极大一致集**

### 4.2.17 定理 Henkin集性质
> 若$\Gamma$集是**Henkin**集则$\forall x \phi \in \Gamma 当前仅当 所有t项有\phi_{t/x}<t/x> \in \Gamma$

> 证:  
> 若$\Gamma$是**Henkin**集,$\forall x \phi \in \Gamma$,由4.2.10$\Gamma \vdash \forall x \phi$,由CV任意$\phi_{t/x}<t/x>$有$\Gamma \vdash \phi_{t/x}<t/x>$,再使用4.2.10$所有项t有\phi_{t/x}<t/x> \in \Gamma$  
> 若$\Gamma$是**Henkin**集,所有项t有$\phi_{t/x}<t/x> \in \Gamma$,假设$\forall x \phi \notin \Gamma$,由4.2.10有$\neg \forall x \phi \in \Gamma$,因此$存在一个项t使得\phi_{t/x}<t/x> \in \Gamma$矛盾.

通过**Henkin**集的定义和一致性的性质,我们找到其逆否命题,从而可以单独构建一个逆否命题的正例(原命题的反例)而不是所有原命题的正例来简化构造过程.

最后我们来构造这个**Henkin**集$\Gamma$,其目的在于每个$\forall x \phi$存在一个项t使得$\neg \forall x \phi \Rightarrow \neg \phi_{t/x}<t/x> \in \Gamma$既每个$\forall x \phi$存在一个项t使得$\phi_{t/x}<t/x> \Rightarrow \forall x \phi \in \Gamma$

### 4.2.18 定理 Henkin集构造定理
>任何一致的$L_{C,F,R}^1$公式集可扩展为它的某个膨胀$L_{C^\prime,F^\prime,R^\prime}^1$语言上的Henkin集

> 证:
> 设$\Gamma$是可数的$L_{C,F,R}^1$公式集,我们将膨胀其中的C构成
> $L_{C^\prime,F,R}^1$,$\Gamma$同样是$L_{C^\prime,F,R}^1$上的公式集合.令$d_1,d_2,...$为其新的常量项,这样膨胀的$L_{C^\prime,F,R}^1$也是可数的,因此我们将所有的全称公式$\forall x \phi_1,\forall x \phi_2,...$排成一列.我们定义一个这样的序列$c_1,c_2,...$,每个$c_i$满足  
> 1.$c_i$不在$\forall x \phi_i$中  
> 2.$c_i$不与$c_j$相同,其中$j \le i$  
> 3.$c_i$是满足上面条件且在$d_1,d_2,...$最前面的一个  
> 我们通过一下方法构建$\Gamma_i$公式集序列$\Gamma_1,\Gamma_2,...$:  
> 1.$\Gamma_1$=$\Gamma$  
> 2.$\Gamma_{i+1}$=$\Gamma_i \cup \{\phi_i<t/x> \Rightarrow \forall x \phi_i\}$  
> 首先我们可以证明任意$\Gamma_i$是一致的.我们施归纳法于i.$i=0$时$\Gamma_0=\Gamma$是一致的.若对于任意$\Gamma_i$是一致的,$\Gamma_{i+1}$却不一致,由4.2.6.5有$\Gamma_i$与$\neg \phi_i<t/x>$不一致且$\Gamma_i$与$\forall x \phi_i$不一致,由归纳假设$\Gamma_i$是一致的,因此由4.2.6.2有$\Gamma_i$与$\neg \forall x \phi_i$一致,由于$c_i$不在$\Gamma_i、\phi_i$出现,因此由4.2.6.7可知$\Gamma_i$与$\neg \phi_i<c_i/x>$一致,矛盾,故$\Gamma_{i+1}$一致
> 令$\Gamma_{C^\prime} = \cup_{i=1}^\infty \Gamma_i$,类似4.2.12可知$\Gamma_{C^\prime}$是一致的,接着我们再采用4.2.12的构造方法,可构建极大一致集$\Gamma_{C^\prime}^\prime$.由定义对任意全称公式$\forall x \phi \in \Gamma_{C^\prime}^\prime$存在某个项$t$使得$\phi<t/x> \Rightarrow \forall x \in \Gamma_{C^\prime}^\prime$,由4.2.10和Contrap、DT知若$\neg \forall \phi \in  \Gamma_{C^\prime}^\prime$则存在项t使得$\neg \phi<t/x> \in \Gamma_{C^\prime}^\prime$因此$\Gamma_{C^\prime}^\prime$是**Henkin**集.

为了施归纳法,我们为$L_{C,F,R}^1$定义复杂度
### 4.2.19 $L_{C,F,R}^1$复杂度
> $L_{P,F_1}^0$公式$\phi$的复杂度$deg(\phi)$被递归的定义为:
> - 若$\phi$是原子公式$r(t_1,...,t_n)$则$deg(\phi)=0$
> - 若$\phi$是$\neg \psi$则$deg(\phi)=deg(\psi)+1$
> - 若$\phi$是$\psi \Rightarrow \chi$则$deg(\phi)=max(deg(\psi),deg(\chi))+1$
> - 若$\phi$是$\forall x \psi$则$deg(\phi)=deg(\psi)+1$

### 4.2.20 定理 Henkin集可满足
>设$\Gamma$是Henkin集,$\sigma_{\Gamma}$是其上的**符号赋值**,我们证明$\phi \in \Gamma$当且仅当 $\sigma_{\Gamma} \vDash \phi$.  
对$\Gamma$公式的复杂度施归纳法.$deg(\phi)=0时$,既$\phi = r(t_1,...,t_n)$,由$\sigma_{\Gamma}$的定义$r(t_1,...,t_n) \in \Gamma$当且仅当$(\sigma_{\Gamma}[[t_1]],...,\sigma_{\Gamma}[[t_n]]) \in \sigma_{\Gamma}[[r]]$ ,按语义定义有$\sigma_{\Gamma} \vDash \phi$.$deg(\phi)=k+1$时:
> - $\phi =\neg \psi$其中$\deg(\psi)=n$:
> $$\begin{aligned}
&\sigma_{\Gamma} \vDash \psi \\
&当且仅当 \sigma_{\Gamma} \nvDash \psi(语义) \\
&当前仅当 \psi \notin  \Gamma(归纳)  \\
&当前仅当 \neg \psi \in  \Gamma(4.2.10)  \\
&当前仅当 \phi \in  \Gamma
\end{aligned}$$
> - $\phi = \psi_1 \Rightarrow \psi_2$,其中$max(deg(\psi_1),deg(\psi_2))=n$:
> $$\begin{aligned}
    &\sigma_{\Gamma} \vDash \phi \\
    &当且仅当 \sigma_{\Gamma} \nvDash \psi_1 或 \sigma_{\Gamma}\vDash \psi_2 (语义) \\
    &当且仅当 \neg \psi_1 \in \Gamma 或  \psi_2 \in \Gamma (归纳) \\
    &当且仅当 \psi_1 \Rightarrow \psi_2 \in \Gamma (4.2.6)\\
    &当且仅当 \phi \in \Gamma
\end{aligned}$$
> - $\phi = \forall x \psi$,其中$deg(\psi)=n$:
> $$\begin{aligned}
    &\sigma \vDash \phi \\
    &当且仅当所有a \in A 有\sigma_{\Gamma}(a/x) \vDash \psi(语义) \\
    &当且仅当所有项t有\sigma_{\Gamma}(\sigma_{\Gamma}[[t]]/x) \vDash \psi (\sigma_{\Gamma}定义)\\
    &当且仅当所有项t有\sigma_{\Gamma} \vDash \phi_{t/x}<t/x> （3.9）\\
    &当且仅当 \phi_{t/x}<t/x> \in \Gamma (归纳)\\
    &当且仅当 \forall x \phi \in \Gamma (Henkin集定义)
\end{aligned}$$
因此由归纳法有$\phi \in \Gamma$当且仅当 $\sigma_{\Gamma} \vDash \phi$,$\Gamma$可满足

### 4.2.20 定理 $H_{r_2}^{L^1}$的完全性
> $H_{r_2}^{L^1}$具有完全性

> 证:  
> 由4.2.18任意$H_{r_2}^{L_{C,F,R}^1}$下的公式集$\Gamma$可扩展为某个$H_{r_2}^{L_{C^\prime,F,R}^1}$的Henkin公式集$\Gamma^\prime$,
> 由4.2.20定理可知$\Gamma^\prime$可满足,既存在$\sigma_{\Gamma^\prime} \vDash \Gamma^\prime$,因此可定义其规约$\sigma$有$\sigma \vDash \Gamma$,既任意任意$H_{r_2}^{L_{C,F,R}^1}$下的公式集$\Gamma$可满足,由4.2.8可知$H_{r_2}^{L_{C,F,R}^1}$具有完全性.

### 4.2.21 定理 $H_{r_2}^{L^1}$的紧致性
> $H_{r_2}^{L^1}$具有紧致性

### 4.2.22 $r_3$
>- $\sigma[[\phi \vee \psi]]=\sigma[[\neg \phi \Rightarrow \psi]]$
>- $\sigma[[\phi \wedge \psi]]=\sigma[[\neg (\phi \Rightarrow 
\neg \psi)]]$  
>- $\sigma[[\phi \equiv \psi]]=\sigma[[(\phi \Rightarrow 
\psi) \wedge (\psi \Rightarrow 
\phi)]]$
>- $\sigma[[\exists \phi]]=\sigma[[\neg (\forall \neg \phi)]]$

虽然我们可以按照如上语义将任何$L^1$公式翻译成仅包含$\{\neg,\Rightarrow,\forall,(,)\}$符号的公式,但为了更好的使用**演绎**,我们可以将上述**逻辑等值**的公式引入公理系统并修改MP规则:
>MP:从$\phi和\phi \equiv \psi$可得到$\psi$,从$\psi和\phi \equiv \psi$可得到$\phi$
> $$r_3=\begin{cases}
    r_2\\
    8: \phi \vee \psi \equiv \neg \phi \Rightarrow \psi \\
    9: \phi \wedge \psi \equiv \neg (\phi \Rightarrow 
\neg \psi) \\
    10: (\phi \equiv \psi) \equiv(\phi \Rightarrow 
\psi) \wedge (\psi \Rightarrow 
\phi) \\
    11: \exists x \phi \equiv \neg \forall x \neg \phi
\end{cases}$$
这样我们可以用它们构成的公式进行演绎了

### 4.2.22 $H_{r_3}^{L^1}$的相关定理
>1. Simp(simplification,简化):若$\Gamma \vdash \phi \wedge \psi$则$\Gamma \vdash \phi$且$\Gamma \vdash \psi$
>2. Conj(conjucation,合取):若$\Gamma \vdash \phi$且$\Delta \vdash \psi$则$\Gamma,\Delta \vdash \phi \wedge \psi$.$\Gamma,\phi,\psi \vdash \chi$当且仅当$\Gamma,\phi \wedge \psi \vdash \chi$
>3. Add(addition,引入):若$\Gamma \vdash \phi$则任意$\psi$有
$\Gamma \vdash \phi \vee \psi$且$\Gamma \vdash \psi  \vee \phi$
>4. CA(case argument,分类讨论):若$\Gamma,\phi \vdash \chi$且$\Gamma,\psi \vdash \chi$则$\Gamma,\Delta,\phi \vee \psi \vdash \chi$.若$\Gamma,\phi \vdash \chi$且$\Gamma,\psi \vdash \chi^\prime$则$\Gamma,\Delta,\phi \vee \psi \vdash \chi \vee \chi^\prime$.
>5. 若$\vdash \phi \equiv \psi$则$\vdash Q_1 x_1...\forall x_n \phi \equiv Q_1 x_0...Q_n x_n \psi$,其中$Q_i \in \{\forall , \exists \}$
>6. $\vdash \forall x_1...\forall x_n \phi \equiv \forall x_{k_0}...\forall y_{k_n} \phi$,其中$x_{k_0},...,x_{k_n}$是$x_0,...,x_n$的一个排列
>7. $\vdash \exists x_1...\exists x_n \phi \equiv \exists x_{k_0}...\exists y_{k_n} \phi$,其中$x_{k_0},...,x_{k_n}$是$x_0,...,x_n$的一个排列
>8. $\vdash \forall (\phi \wedge \psi) \equiv \forall x \phi \wedge \forall x \psi$
>9. $\vdash \forall x \phi \vee \forall x \psi \Rightarrow \forall x (\phi \vee \psi)$
>10. $\vdash \forall x (\phi \Rightarrow \psi) \Rightarrow (\forall x \phi \Rightarrow \forall x \psi)$    
>11. $\vdash \forall x (\phi \equiv \psi) \Rightarrow (\forall x \phi \equiv \forall x \psi)$
>12. $\exists x (\phi \vee \psi) \equiv \exists x \phi \vee \exists x \psi$
>13. $\exists x (\phi \wedge \psi) \Rightarrow \exists x \phi \wedge \exists x \psi$
>14. $(\exists x \phi \Rightarrow \exists x \psi)\Rightarrow \exists x (\phi \Rightarrow \psi)$

> 证:  
> 1 若$\Gamma \vdash \phi \wedge \psi$则$\Gamma \vdash \phi$且$\Gamma \vdash \psi$@  
>> 1.1 $\Gamma \vdash \phi$@    
>>> 1.1.1 $\phi \wedge \psi \vdash \neg (\phi \Rightarrow \neg \psi)$@DT($r_3.9$)  
>>> 1.1.2 $\Gamma,\neg \phi \vdash \neg (\phi \Rightarrow \neg \psi)$@CUT(1.1.1,hyp(1))  
>>> 1.1.3 $\Gamma,\neg \phi,\phi \vdash \psi$@IE  
>>> 1.1.4 $\Gamma,\neg \phi \vdash \phi \Rightarrow \neg \psi$@DT(1.1.3)  
>>> 1.1.5 $\Gamma \vdash \phi$@RAA(1.1.2,1.1.4)  
>>>
>>1.2 $\Gamma \vdash \psi$@ 
>>> 类似 
>>> 
> 2 若$\Gamma \vdash \phi$且$\Delta \vdash \psi$则$\Gamma,\Delta \vdash \phi \wedge \psi$.$\Gamma,\phi,\psi \vdash \chi$当且仅当$\Gamma,\phi \wedge \psi \vdash \chi$  
>> 2.1 若$\Gamma \vdash \phi$且$\Delta \vdash \psi$则$\Gamma,\Delta \vdash \phi \wedge \psi$@    
>>> 2.1.1 $\phi,\psi,\phi \Rightarrow \neg \psi \vdash \neg \psi$@MP  
>>> 2.1.2  $\phi,\psi \vdash \neg (\phi \Rightarrow \neg \psi)$@RAA(2..1.1)  
>>> 2.1.3 $\Gamma,\Delta \vdash \neg (\phi \Rightarrow \neg \psi)$@CUT(hyp(2.1),2.1.1.2)  
>>> 2.1.4  $\neg (\phi \Rightarrow \neg \psi) \vdash \phi \wedge \psi$@DT($r.3.9$)  
>>> 2.1.5 $\Gamma,\Delta \vdash \phi \wedge \psi$@CUT(2.1.4,2.1.3)
>>>
>> 2.2 $\Gamma,\phi,\psi \vdash \chi$当且仅当$\Gamma,\phi \wedge \psi \vdash \chi$@
>>> 由1和2.1很容易得到
>>>
>...

## 5 理论与模型
