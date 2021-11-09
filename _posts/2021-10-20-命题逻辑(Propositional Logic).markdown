---
layout: post
title:      命题逻辑(Propositional Logic)
subtitle:   
author:     uans3k
header-img: img/post-bg-2015.jpg
tags:
    - 逻辑
    - 形式逻辑
---

一些问题用自然语言描述，由于自然语言的特点，问题的描述会过于繁琐,因此我们应该限制自然语言的语法，但是需要指出，语法的限制不代表表达能力(expression ability)的限制，这个表达能力得做特别的讨论。我们这里将要构建命题逻辑语言($L^0$)。相对于构建的$L^0$称为目标语言（target language），我们描述所使用的语言称为元语言(meta language)。  

## 1 $L^0_F$定义

### 1.1 定义 $L^0_F-符号$
> 命题变量集合$\Pr = \{p_0,p_1...\}$  
> 任何属于函数集合$F=\{f_1,f_2...\}$的n元布尔变量到布尔变量的函数,称为真值函数
> - 任何属于$F$的$f$和属于$\Pr$的p称为$L^0_F-符号$  

### 1.2 定义 $L^0_F-公式$
>- 任何属于$\Pr$的$p$是$L^0_F-公式$  
>- 如果$\phi$属于$L^0_F-公式$,对任意一元真值函数符号$f$,$f(\phi)是$L^0_F-公式$  
> - 如果$\phi_1,\phi_2$属于$L^0_F-公式$,对任意2元真值函数符号$f$,$f(\phi_1,\phi_2)$是$L^0_F-公式$  
>- ...  
>- 如果$\phi_1,\phi_2,...,\phi_n$属于$L^0_F-公式$,对任意n元真值函数符号$f$,$f(\phi_1,\phi_2,...,\phi_n)$是$L^0_F-公式$  
>- 只有这些是$L^0_F-公式$

### 1.3 定义 赋值(assignment)  

>对任意$L^0_F-公式\ \phi$,我们用 $\sigma [[\phi]]$表示$\sigma$对$\phi$的**赋值**。对任意$\phi$可以定义**赋值**$\sigma$:  
>- $\sigma[[p]]$ 属于 {True,False}  
>- $\sigma[[f(\phi_1,...,\phi_1)]]=f(\sigma[[\phi_1]],...\sigma[[\phi_n]])$   

### 1.4 定义 满足（satisfy）
> $\Gamma$ 为$L^0_F-公式$集合,$\sigma$为赋值,我们称$\sigma$**满足**$\Gamma$(记为$\sigma \vDash \Gamma$)当且仅当任意属于$\Gamma$的$\phi$有 $\sigma [[\phi]]=True$,相反则称为**不满足**记为
$\sigma \nvDash \Gamma$。特别地,我们用$\sigma \vDash \phi$表示$\sigma \vDash \{\phi\}$,$\sigma \nvDash \phi$表示$\sigma \nvDash \{\phi\}。$

### 1.5 定义 重言蕴含(tautological implication)
> $\Gamma$ 为$L^0_F-公式$集合,$\phi$ 为$L^0_F-公式$,我们称$\Gamma$ **重言蕴涵**$\sigma$(记为$\Gamma \vDash \phi$)当且仅当对任意赋值$\sigma$,若$\sigma \vDash \Gamma$则$\sigma \vDash \phi$。

### 1.6 定义 重言等值(tautological equivalence)
>$L^0_F-公式 \phi 和 \psi$称为**重言等值**当且仅当对任意赋值$\sigma$有$\sigma[[\phi]]=\sigma[[\psi]]$

### 1.7 定义 重言式(tautological formula)、矛盾式(contradictory formula)、或然式(probable formula)
>对任意$L^0_F-公式 \phi$,$\phi$称为**重言式**当且仅当对任意赋值$\sigma$有$\sigma \vDash \phi$。    
>对任意$L^0_F-公式 \phi$,$\phi$称为**矛盾式**当且仅当对任意赋值$\sigma$有$\sigma \nvDash \phi$。   
>对任意$L^0_F-公式 \phi$,$\phi$称为**或然式**当且仅当存在一个$\sigma$有$\sigma \nvDash \phi$且存在一个$\sigma^\prime$有$\sigma^\prime \vDash \phi$。

## 2 $L^0_F$性质
1节中定义了$L^0_F$,其中1.1-1.2是$L^0_F$语法，1.3-1.7是$L^0_F$的语义。语法描述了如何构成一个语言句子,而语义则告诉我们怎么理解这些句子。我们知道，语法的不同不代表表达能力的不同，但会影响表达的复杂程度和人类的使用难度。这一节旨在指出$L^0_F$的表达能力，以及选择一个易于使用的$L^0_F$。
### 2.1 定义 表达(expression)
>$\phi$是包含n个命题变量$(p_1,...,p_n)$的$L^0_F-公式$,$f$是n元真值函数。  
>我们称 $\phi$在$L^0_F$下**表达**$f$当且仅当对任意赋值$\sigma$有$\sigma[[\phi]]=f(\sigma[[p_1],...,\sigma[[p_n]])$.  
>我们称$f$在$L^0_F$下**可被表达**当前仅存在一个$\phi$**表达**$f$

### 2.2 定义 函数完全(funcion completeness)
>$L^0_F$称为**函数完全**的当且仅当任意真值函数在$L^0_F$下**可被表达**

2.1-2.2描述了任意**函数完全**的$L^0_F$具有相同的表达能力且任意$L^0_F\prime$能表达的**函数完全**的$L^0_F$也能表达。**函数完全**的$L^0_F$是$L^0$语言表达能力的上限。

### 2.3 定义 合取(conjunction)、析取(disjunction)、蕴涵(implication)、否定(negation)、等价(equivalence)

>我们定义真值函数:  
>$f_\vee(b_1,b_2)=True$当且仅当 $b_1=True且b_2=True$  
>$f_\wedge(b_1,b_2)=True$当且仅当 $b_1=True或b_2=True$  
>$f_\neg(b)=True$当且仅当 $b=False$  
>$f_\Rightarrow(b_1,b_2)=True$当且仅当$b_1=False$或者$b_1$和$b_2$同时等于$True$  
>$f_\equiv(b_1,b_2)=True$当且仅当$b_1$和$b_2$同时为$True$或者同时为$False$

### 2.4 定理 函数完全定理(funcion completeness theory)
> $L^0_{f_\neg,f_\wedge}$是函数完全的  
>>证明：
>>对任意n元真值函数,令
>>$B^j=(b_1^j,...,b_n^j) 是使f(b_1^j,...,b_n^j)=True的真值序列,j \leq k=2^n$.    
>>$\theta_i^j = \begin{cases}
    p_i^j ,若 b_i^j= True ;\\
    ～p_i^j,若b_i^j=False \\
\end{cases}$  
>>$\psi^j= \theta_1^j \wedge ... \wedge \theta_n^j$  
>>$\phi= \neg(\neg \psi^1 \wedge ... \wedge \neg \psi^j)$
>> - 若赋值$\sigma$使$f(\sigma[[p_1]],...,\sigma[[p_n]])=True$,那么$(\sigma[[p_1]],...,\sigma[[p_n]])$为某个真值序列$B^j$,
>>那么$\sigma[[\psi^j]]=True$,因此$\sigma[[\phi^j]]=True$
>> - 若赋值$\sigma$使$\sigma[[\phi^j]]=True$,那么存在一个$\psi^j=True$,既对任意i有$\theta_i^j=True$,因此$若p_i^j=True则b_i^j=True$,$若p_i^j=False则b_i^j=False$,既$\sigma[[p_1]],...,\sigma[[p_n]]$是使f(b_1^j,...,b_n^j)=True的真值序列$B^j$,因此$f(\sigma[[p_1]],...,\sigma[[p_n]])=True$  
>>     
>> 因此对任意赋值$\sigma$有$\sigma[[\phi]]=f(\sigma[[p_1]],...,\sigma[[p_n]])$,$L^0_{\{f_\neg,f_\wedge\}}$是函数完全的.  

2.4定理说明了只要$F$包含了$f_\neg,f_\wedge$那么就达到了$L^0$表达能力的上限。因此我们可以选择一个包含了$f_\neg,f_\wedge$的$F$构建我们的$L^0$语言。

### 2.5 定义 $L^0$语言 
> $L^0$语法由下述定义:   
>- $(b_1 \vee b_2)= f_\vee(b_1,b_2)$  
>- $(b_1 \wedge b_2)= f_\wedge(b_1,b_2)$  
>- $(b_1 \Rightarrow b_2)=f_\Rightarrow(b_1,b_2)$   
>- $(b_1 \equiv b_2)=f_\equiv(b_1,b_2)$  
>- $(\neg b)=f_\neg(b)$  
>  
>去除括号时以$\neg$更高的优先级结合。当我们去除括号后表达的意思一致时，可以去除括号。
>$L_{\vee,\wedge,\Rightarrow,\equiv,\neg}^0$简记为$L^0$  
> $L^0$语义由1.4-1.7定义

## 3 $L^0$演绎$H^0$  
1,2节定义了$L^0$语言的语法与语义,构建$L^0$的语言的目标包含2个:
>- 判定$L^0-公式$是否为**重言式**
>- 判定2个$L^0-公式$集合是否**重言蕴涵**

其他诸如**重言等值**可以判定是否互为**重言蕴涵**来判定,**矛盾式**可以由$\neg(L^0-公式)$是否为**重言式**来判定.**或然式**则可以看$L^0-公式$是否为**重言式**来判定.  
根据语义定义，我们可以用**穷举**赋值(复杂度为$2^n$,n为命题变量的数量)来验证所有的**重言式**以及**重言蕴涵关系**,但我们可以通过元定理(元语言所证明的定理)来构建一个演算体系，可以避免**穷举**.我们称这样一个演算体系为$H_r^0$演算,其中$r$为一个规则集合，包含**公理(axiom)**和**操作(operator)**.我们把**公理**定义为$L^0$的重言式,这可以通过**穷举**验证,另外我们将讨论**操作**的性质

## 3.1 公理体系

### 3.1.2 定义 操作(operator)
> 从一个公式或多个公式得到另外一个公式的动作称为**操作**

### 3.1.3 定义 代入(substitute)
>s是一个$L^0-公式$到$L^0-公式$的映射,对所有$L^0-公式$,$\phi<s>$是一个**操作**称为**代入**:
> - 若$p$是一个命题变量则$p<s>=s(p)$
> - 若$f(\psi_1,...,\psi_n)<s>=f(\psi_1<s>,...,\psi_n<s>)$
>       
>特别地,我们记$f<\psi_1/p_1,...,\phi_n/p_n>,其中p_i<s>=\psi_i$. 称为**有穷代入**    
>简记代入操作为SUB  

### 3.1.4 定义 分离(modus ponens)
>从$\phi,\phi \Rightarrow \psi$得到$\psi$的动作称为**分离**,简记分离操作为MP

### 3.1.4 定义 公理体系与演绎(deduction)
> 一个包含**操作**和$L_0$的重言式的体系称为**公理体系**,其中$L_0$的重言式被称为**公理**,**公理**和**操作**的集合被称为**规则**记为$r$,该**公理体系**被记为$H_r^0$.      
> $H_r^0$中的公式集$\Gamma$到公式$\phi$的**演绎**是满足下列条件的任意公式序列$\phi_1,...,\phi_n$:
>- $\phi_n=\phi$
>- 对任意$k \le n$,$\phi_k$或是$H_r^0$的**公理**,或是$\Gamma$中的**公式**,或是从$\phi_{j_1},...,\phi_{j_m},j_i \le k$通过动作得到的.   
>     
>我们记其为$\Gamma \vdash \phi$,称$\phi$在$H_r^0$下从$\Gamma$**可演绎(deducible)**,$\phi$是$H_r^0$下$\Gamma$的**演绎后承(deductive consequence)**,特别地,若$\Gamma=\varnothing$,记$\vdash \phi$

## 3.2 公理体系的性质
前面定义了公理体系及其演绎，但他们与**重言式**与**重言蕴涵**有什么关系没有说明,这一节讲指出$H_r^0$与$L^0$的关系,帮助我们使用$H_r^0$来判定$L^0$的语义。

### 3.2.1 元定理与内定理
所有能从空集演绎得到的公式被称作$H_r^0$的内定理，而$H_r^0$本身的性质，需要我们用元语言描述，因此我们称其为元定理。例如$\Gamma \vdash \phi$并不是$L^0$的公式，因此如果$\Gamma \vdash \phi$恒成立是元定理，但得到这个元定理的证明是通过$L^0$语义和$H_r^0$的演绎,因为这个定理本质上是用来描述$H_r^0$系统的。利用一系列元定理，可以更简单的得到演绎结果而不需要走完整的演绎过程。而利用演绎可以避免**穷举赋值**。

### 3.2.2 定义 可靠性(soundness)
>对任意$H_r^0$下的$\Gamma$和$\phi$,如果$\Gamma \vdash \phi$则$\Gamma \vDash \phi$,特别地如果$\vdash \phi$则$\vDash \phi$,那么我们称$H_r^0$具有**可靠性**

一个**公理系统**$H_r^0$具有可靠性,那么我们可以通过**演绎**来正确的确定**重言蕴涵**关系，但是没有说明是否任意**重言蕴涵**关系可以通过**演绎**来证明。因此我们需要一个性质来描述。

### 3.2.3 定义 完全性(completeness)
>对任意$H_r^0$下的$\Gamma$和$\phi$,如果$\Gamma \vDash \phi$则$\Gamma \vdash \phi$,特别地如果$\vDash \phi$则$\vdash \phi$,那么我们称$H_r^0$具有**完全性**

完全性描述了任意**重言蕴涵**关系可以通过**演绎**得出.3.2.2-3.2.3表明来演绎的作用,通过演绎可以无需**穷举**赋值来确定**任意重言式和重言蕴涵**关系

### 3.2.4 定义 一致性(consistency)
>**公理系统**具有**一致性**当前仅当不存在$L^0-公式\phi$使得$\vdash \phi 且\vdash \neg \phi$.  
>$\Gamma$在$H_r^0$下具有一致性当且仅当不存在$L^0-公式\phi$使得$\Gamma \vdash \phi 且\Gamma \vdash \neg \phi$.  

### 3.2.5 定理 可靠性定理
>若r只包含**公理**、代入操作、分离操作则$H_r^0$具有**可靠性**.

我们令
>$$r_1=\begin{cases}
    1:p \Rightarrow (q \Rightarrow p) \\
    2:(p \Rightarrow (q \Rightarrow r))\Rightarrow ((p \Rightarrow q) \Rightarrow (p \Rightarrow r)) \\
    3:(\neg p \Rightarrow q) \Rightarrow ((\neg p \Rightarrow \neg q) \Rightarrow p)\\
    4:SUB\\
    5:MP
\end{cases}$$

> $$r_2=\begin{cases}
    1:\phi \Rightarrow (\psi \Rightarrow \phi) \\
    2:(\phi \Rightarrow (\psi \Rightarrow \chi))\Rightarrow ((\phi \Rightarrow \psi) \Rightarrow (\phi \Rightarrow \chi))\\
    3:(\neg \phi \Rightarrow \psi) \Rightarrow ((\neg \phi \Rightarrow \neg \psi) \Rightarrow \phi)\\
    4:MP
\end{cases}$$  
 
### 3.2.6 定理 完全性定理

> $H_{r_1}^0,H_{r_2}^0$具有**完全性**.

### 3.2.7 定理 一致性定理

> $H_{r_1}^0,H_{r_2}^0$具有**一致性**.    
> 若$H_r^0$具有一致性,那么对任意公式集$\Gamma$在$H_r^0$下:
>- $\Gamma$**不一致**当且仅当$\Gamma$的某个有穷子集**不一致**
>- $若\Gamma$**一致**则$\Gamma$的所有**演绎后承**集**一致**
