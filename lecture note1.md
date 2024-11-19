# 哈希函数
Collision resistant : $\forall$ PPT ***A*** 

$$
Pr \left[\begin{array}{l}
x \neq x' \land \\
h_i(x) = h_{i}(x') :
\end{array}
\begin{array}{l}
i \leftarrow Gen(\lambda); \\
(x,x') \leftarrow \cal{A}(i)
\end{array}
\right] \leq negl(\lambda)
$$

Universal one-wayness : $\forall$ PPT ***A***

$$
Pr \left[\begin{array}{l}
x \neq x' \land \\
h_i(x)=h_i(x') \colon
\end{array}
\begin{array}{l}
x \leftarrow \cal{A}(\lambda);\\
i \leftarrow Gen(\lambda);\\
x' \leftarrow \cal{A}(i);
\end{array}
\right] \leq negl(\lambda)
$$

TCR(Second Pre-Image Resistance) : $\forall$ PPT ***A***  

$$
Pr \left[\begin{array}{l}
x\neq x' \land \\  
h_i(x)=h_i(x'):
\end{array}
\begin{array}{l}
i \leftarrow Gen(\lambda); \\
x \leftarrow \lbrace 0,1 \rbrace ^* \\
x' \leftarrow \cal{A}(i,x);
\end{array}
\right]\leq negl(\lambda)
$$

Pre-Image Resisttance : $\forall$ PPT ***A*** 

$$
Pr \left[ h_i(x) = h_{i}(x') :
\begin{array}{l}
i \leftarrow Gen(\lambda); \\
x \leftarrow \lbrace 0,1 \rbrace ^* \\
x' \leftarrow A(i, h_i(x));
\end{array}
\right] \leq negl(\lambda)
$$

## 安全规约
CR $\Rightarrow$ UOW $\Rightarrow$ TCR $\Rightarrow$ PIR
### CR $\Rightarrow$ UOW
Proof：

$$
\begin{CD}
CR@>>> UOW\\
@AAA@AAA\\
\cal{B}@<<<\cal{A} 
\end{CD}
$$

进行以下实验：
1. $\cal{B}$ 获得参数 $\lambda$,执行 $i \leftarrow Gen(\lambda)$
2. $\cal{B}$将参数 $\lambda$ 给予 $\cal{A}$
3. $\cal{A}$执行 $x \leftarrow \cal{A}(\lambda)$，并将 $x$返回给 $\cal{A}$
4. $\cal{B}$将参数  $i$ 给予 $\cal{A}$
5. $\cal{A}$执行 $x' \leftarrow Gen(\lambda)$，并将 $x'$返回给 $\cal{A}$
6. 如果 $x \neq x' \land h_i(x) = h_{i}(x')$，则实验输出1，反之输出0

我们看到：
$Pr[B \ breaks  \ CR]=Pr[A \ breaks \ UOW]$

### UOW $\Rightarrow$ TCR
Proof：

$$
\begin{CD}
UOW@>>> TCR\\
@AAA@AAA\\
\cal{B}@<<<\cal{A} 
\end{CD}
$$

进行以下实验：
1. $\cal{B}$ 获得参数 $\lambda$,执行 $x \leftarrow \cal{B}(\lambda)$ 和 $i \leftarrow Gen(\lambda)$
2. $\cal{B}$将参数 $i$ 和 $x$ 给予 $\cal{A}$
3. $\cal{A}$执行 $x' \leftarrow \cal{A}(x,i)$，并将 $x'$返回给 $\cal{A}$
4. 如果 $x \neq x' \land h_i(x) = h_{i}(x')$，则实验输出1，反之输出0

我们看到：
$Pr[B \ breaks  \ UOW]=Pr[A \ breaks \ TCR]$

>A的视图中，随机选择的x和B发送的x可区分吗？

### TCR $\Rightarrow$ PIR  
a mild codnition: *H* is v-regular,i.e.,for every image y, $|h^{-1}| \geq v$    
Proof：

$$
\begin{CD}
TCR@>>> PIR\\
@AAA@AAA\\
\cal{B}@<<<\cal{A} 
\end{CD}
$$

进行以下实验：
1. $\cal{B}$ 获得参数 $\lambda$,执行  $i \leftarrow Gen(\lambda)$ 和 $x \leftarrow \lbrace 0,1 \rbrace ^*$,并计算 $y \leftarrow h_i(x)$
3. $\cal{B}$将参数 $i$ 和 $y$ 给予 $\cal{A}$
4. $\cal{A}$执行 $x' \leftarrow A(i, h_i(x))$,并将x'返回给 $\cal{B}$
5. 如果 $x \neq x' \land h_i(x) = h_{i}(x')$，则实验输出1，反之输出0

我们看到：
$Pr[B \ breaks  \ UOW]=Pr[A \ breaks \ TCR]$
