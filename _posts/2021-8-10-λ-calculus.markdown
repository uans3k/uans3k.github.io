---
layout: post
title:      λ-calculus
subtitle:   
author:     uans3k
header-img: img/post-bg-2015.jpg
tags:
    - 计算性
    - 函数式
    - 程序语言设计
---
# λ-calculus

## 1 定义
语法

exp ::= aexp | cexp
aexp ::= x | λx.exp
cexp ::= (exp exp)

$\alpha等价$
自由参数不影响exp的等价
$λx.x == λy.y$

$\beta规约$
cexp应用时会将第一个exp中的自由参数替换为第二个exp
$(λx.λy.exp\ a)=λy.exp[x:=a]$

## 2 咖喱化 (curring)
通过咖喱化可以定义多变量λ演算
$
\\λ(x\ y).exp:= λx.(λy.exp)) = λx.λy.exp
\ \\
(λ(x\ y).exp\ a\ b)=(λx.λy.exp\ a\ b)=exp
\\ (λ(x\ y).exp\ a)=(λx.λy.exp\ a)=λy.exp[x:=a]
$

## 3 谓词与逻辑
### bool算子
$
true := λ(a\ b).a \\
false := λ(a\ b).b
$

### 与运算
$
and:= λ(a\ b).(a\ b\ false) \\
\ \\
(and\ true\ true)=(true\ true\ false)=true \\
(and\ false\ false)= (false\ false\ false)=false \\
(and\ true\ false)= (true\ false\ false)=false \\
(and\ false\ true)= (false\ true\ false)=false
$

### 或运算
$
or:= λ(a\ b).(a\ true\ b)\\
\ \\
(or\ true\ true) = (true\ true\ false)= true \\
(or\ true\ false) = (true\ true\ false)= false \\
(or\ false\ false) = (flase\ true\ false)= false \\
(or\ false\ true) = (flase\ true\ false)= false 
$

### 否运算
$
not:= λa.(a\ false\ true) \\
\ \\
(not\ true)= (true\ false\ true)=false \\
(not\ false)= (false\ false\ true)=false 
$

### 异或运算
$
xor:= λ(a\ b).(or\ (and\ (not\ a)\ b)\ (and\ a\ (not\ b))\\
\ \\
(xor\ true\ false)=(or\ (and\ (not\ true)\ false)\ (and\ true\ (not\ false))= true  \\
(xor\ true\ true)=(or\ (and\ (not\ true) true)\ (and\ true\ (not\ true))= fasle \\
(xor\ false\ false)=(or\ (and\ (not\ false)\ false)\ (and\ false\ (not\ false))= fasle \\
(xor\ false\ true)=(or\ (and\ (not\ false)\ true)\ (and\ false\ (not\ true))= true \\
$

### c条件选择
$
\\ if:=λ(t\ a\ b).(t\ a\ b)
\\\
\\ (if\ false\ a\ b)=(false\ a\ b)=b
\\ (if\ true\ a\ b)=(true\ a\ b)=a
$

## 4 有序对与列表
### 有序对
$
\\ [a\ b]:=λt.(if\ t\ a\ b)
\\ car:=λp.(p\ true) 
\\ cdr:=λp.(p\ false)
\\\
\\ (car\ [a\ b])=(λt.(if\ t\ a\ b)\ true)=a 
\\ (cdr\ [a\ b])=(λt.(if\ t\ a\ b)\ flase)=b
$

### 列表
$
\\[a\ b\ c]:=[a\ [b\ c]]=λt.(if\ t\ a\ λt2.(if\ t2\ b\ c)) 
\\\
\\(car\ [a\ b\ c])=(car\ [a\ [b\ c]])=a
\\(cdr\ [a\ b\ c])=(cdr\ [a\ [b\ c]])=[b\ c]
$


## 5 自然数

### 自然数算子
相当于将operator 作用在 operand n次
$
0:= λ(f\ x).x \\
1:= λ(f\ x).(f\ x) \\
2:= λ(f\ x).(f\ (f\ x)) \\
...\\
n:= λ(f\ x).(f^n\ x)
$

### 后继
$
succ:= λa.(λ(b\ c).(b\ (a\ b\ c)) \\
\ \\
(succ\ n)=λ(b\ c).(b\ (n\ b\ c))=λ(b\ c).(b\ (b^n\ c))=λ(b\ c).(b^{(n+1)}\ c)=n+1
$

### 加法
$
plus:= λ(m\ n).λ(a\ b).(m a (n a b)) \\
\ \\
(plus\ m\ n)=λ(a\ b).(m\ a\ (n\ a\ b))=λ(a\ b).(m\ a\ (a^n\ b))=(a^m\ (a^n\ b))=(a^{m+n}\ b)
$

### zero比较
$
\\ zero?:=λa.((a\ false\ not) false))
\\\
\\ (zero?\ 2)=((2\ false\ not)\ false)=(1\ false\ false)=false
\\ (zero?\ 0)=((0\ false\ not)\ false)=(not\ false)=true
$

### 前继
$
succ_{pair}:=λa.[(succ\ (car\ a))\ (if\ (zero?\ (car\ a))\ (cdr\ a)\ (succ\ (cdr\ a)))]\\
pred:=λa.(cdr\ (a\ succ_{pair}\ [0\ 0])) \\
\ \\
(succ_{pair}\ [0\ 0])=[(succ\ 0)\ (if\ (zero?\ 0)\ 0\ 1))]=[1\ 0]\\
(succ_{pair}\ [1\ 0])=[(succ\ 1)\ (if\ (zero?\ 1)\ 0\ 1))]=[2\ 1]\\
\ ...\\
(succ_{pair}\ [n-1,n-2])=[(succ\ n-1)\ (if\ (zero?\ n-1)\ n-2\ n-1))]=[n\ n-1]\\
(pred\ n)=(cdr\ (n\ succ_{pair}\ [0\ 0]))=(cdr\ [n\ n-1])=n-1
$

### 减法
$
\\ sub:= λ(m\ n).(n\ pred\ m)
\\\
\\ (sub\ m\ n)=(n-1\ pred\ m-1)=...=(0\ pred\ m-n)=m-n
$

### 乘法
$
mult:= λ(m\ n).λ(a\ b).(m\ (n\ a\ c)\ b)
\\\
\\(mult\ m\ n)=λ(a\ b).(m\ (n\ a)\ b)
\\=λ(a\ b).(m-1\ (n\ a)\ (a^n b))=...=λ(a\ b).(a^{m*n}\ b)=m*n
$

### 指数
$
exp:= λ(m\ n).λ(a\ b).(n\ a\ (m\ a\ b))
$

### 自然数比较
$
\\ ge?:=  λ(m\ n).(zero?\ (sub\ n\ m))
\\ le?:=   λ(m\ n).(zero?\ (sub\ m\ n))
\\ equal?:= λ(m\ n).(and\ (ge?\ m\ n)\ (ge?\ n\ m)) 
\\ g?:= λ(m\ n).(and\ (ge?\ m\ n)\ (not\ (equal?\ m\ n)))
\\ l?:= λ(m\ n).(and\ (le?\ m\ n)\ (not\ (equal?\ m\ n)))
$

## 6 Let-Bound
$
\\ let\ x=M\ in\ N:= ((λx.N)\ M)
$

## 7 迭代
### 不动点算子 (Y组合子,悖论算子)
$
Y := λg.(λx.(g\ (x\ x))\ λx.(g\ (x\ x)))
\\\
\\(Y g)=(g\ (λx.(g\ (x\ x))\ λx.(g\ (x\ x))))
\\ =(g\ (λf.(λx.(f\ (x\ x))\ λx.(f\ (x\ x)))\ g))=(g\ (Y\ g))
$

这样对于任意$f$,令$g=(Y f)$则$f(g)=g$,$g$称为$f$的不动点，用不动点算子可以构造任意算子的不动点

### 利用Y算子构建递归函数

#### 阶乘函数fact
辅助函数 A
$A:=λf.
\\\quad\quad\quad (λn.
\\\quad\quad\quad\quad (
\\\quad\quad\quad\quad\quad(zero?\ n)
\\\quad\quad\quad\quad\quad 1
\\\quad\quad\quad\quad\quad (mult\ n\ (f\ (pred\ n)))
\\\quad\quad\quad\quad )
\\\quad\quad\quad )
$

我们需要找到$f$让$f=(A\ f)$,这样

$
\\ (A\ f\ n)= (mult\ n\ (f\ n-1))=(mult\ n\ ((A\ f)\ n-1))=...=n!
$

利用Y算子我们知道$f=(Y A)$,这样我们就能构造fact函数为
$
\\fact:= (A\ (Y\ A))=(Y\ A)
\\\
\\(fact\ n)=(Y\ A\ n)=(A\ (Y\ A)\ n)=(mult\ n\ (Y\ A\ n-1))=...=n!
$

#### 任意递归函数g
$
\\g:=(Y\ λf.M)
\\\
\\(g\ x)=(Y\ λf.M\ x)=(λf.M\ (Y\ λf.M)\ x)=(M[f=λf.M]\ x)
$