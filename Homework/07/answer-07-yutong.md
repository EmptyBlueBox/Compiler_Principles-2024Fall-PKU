# 编译原理第七次作业

<center><div style='height:2mm;'></div><div style="font-size:10pt;">梁昱桐 2100013116</div></center>

<center><span style="font-size:9pt;line-height:9mm"><i>Peking University</i></span></center>

## Ex 4.7.1

为练习 4.2.1 的文法 S $\to$ SS+ $\mid$ SS* $\mid$ a 构造规范 LR 项集族和 LALR 项集族

提取左公因子和消除左递归后得到：

$$
S' \rightarrow S\\
S \rightarrow a B\\
B \rightarrow a B A B\\
B \rightarrow \varepsilon\\
A \rightarrow +\\
A \rightarrow *
$$

计算可得:

$$
FIRST(B) = \{a\}\\
FIRST(A) = \{+, *\}
$$

### 规范 LR 项集族

规范 LR 项集族：

1. $I_0$
   1. $S'\to \cdot S, \$$
   2. $S \to \cdot aB, \$$
2. $I_1$, from $I_0$
   1. $S' \to S \cdot, \$$
3. $I_2$, from $I_0$ by $a$
   1. $S \to a \cdot B, \$$
   2. $B \to \cdot aBA, \$$
   3. $B \to \cdot \varepsilon, \$$
4. $I_3$, from $I_2$
   1. $S \to aB \cdot, \$$
5. $I_4$, from $I_2$
   1. $B \to a \cdot BAB, \$$
   2. $B \to \cdot aBAB, +/*$
   3. $B \to \cdot \varepsilon, +/*$
6. $I_5$, from $I_4$ by $B$
   1. $B \to aB \cdot AB, \$$
   2. $A \to \cdot +, a/\$$
   3. $A \to \cdot *, a/\$$
7. $I_6$, from $I_4$ by $a$
   1. $B \to a \cdot BAB, +/*$
   2. $B \to \cdot aBAB, +/*$
   3. $B \to \cdot \varepsilon, +/*$
8. $I_7$, from $I_5$ by $A$
   1. $B \to aBA \cdot B, \$$
   2. $B \to \cdot aBAB, \$$
   3. $B \to \cdot \varepsilon, \$$
9. $I_8$, from $I_5$ by $+$
   1. $A \to + \cdot, a/\$$
10. $I_9$, from $I_5$ by $*$
    1. $A \to * \cdot, a/\$$
11. $I_{10}$, from $I_6$ by $B$
    1. $B \to aB \cdot AB, +/*$
    2. $A \to \cdot +, +/*/a$
    3. $A \to \cdot *, +/*/a$
12. $I_{11}$, from $I_6$ by $a$
    1. $B \to a \cdot BAB, +/*/a$
    2. $B \to \cdot aBAB, +/*$
    3. $B \to \cdot \varepsilon, +/*$
13. $I_{12}$, from $I_{7}$ by $B$
    1. $B \to aBAB \cdot, \$$
14. $I_{13}$, from $I_{10}$ by $A$
    1. $B \to aBA \cdot B, +/*$
    2. $B \to \cdot aBAB, +/*$
    3. $B \to \cdot \varepsilon, +/*$
15. $I_{14}$, from $I_{11}$ by $B$
    1. $B \to aB \cdot AB, +/*/a$
    2. $A \to \cdot +, +/*/a$
    3. $A \to \cdot *, +/*/a$
16. $I_{15}$, from $I_{14}$ by $B$
    1. $B \to aBAB \cdot, +/*$
17. $I_{16}$, from $I_{15}$ by $A$
    1. $B \to aBA \cdot B, +/*/a$
    2. $B \to \cdot aBAB, +/*/a$
    3. $B \to \cdot \varepsilon, +/*/a$
18. $I_{17}$, from $I_{15}$ by $+$
    1. $A \to + \cdot, +/*/a$
19. $I_{18}$, from $I_{15}$ by $*$
    1. $A \to * \cdot, +/*/a$
20. $I_{19}$, from $I_{17}$ by $B$
    1. $B \to aBAB \cdot, +/*/a$

### LALR 项集族

1. $I_0$
   1. $S'\to \cdot S, \$$
   2. $S \to \cdot aB, \$$
2. $I_1$, from $I_0$
   1. $S' \to S \cdot, \$$
3. $I_2$, from $I_0$
   1. $S \to a \cdot B, \$$
   2. $B \to \cdot aBA, \$$
   3. $B \to \cdot \varepsilon, \$$
4. $I_3$, from $I_2$
   1. $S \to aB \cdot, \$$
5. $I_4$, from $I_2$
   1. $B \to a \cdot BAB, +/*/a/\$$
   2. $B \to \cdot aBAB, +/*$
   3. $B \to \cdot \varepsilon, +/*$
6. $I_5$, from $I_4$ by $B$
   1. $B \to aB \cdot AB, +/*/a/\$$
   2. $A \to \cdot +, +/*/a/\$$
   3. $A \to \cdot *, +/*/a/\$$
7. $I_7$, from $I_6$ by $A$
   1. $B \to aBA \cdot B, +/*/a/\$$
   2. $B \to \cdot aBAB, +/*/a/\$$
   3. $B \to \cdot \varepsilon, +/*/a/\$$
8. $I_6$, from $I_5$ by $B$
   1. $B \to aBAB \cdot, +/*/a/\$$
9. $I_8$, from $I_5$ by $+$
   1. $A \to + \cdot, +/*/a/\$$
10. $I_9$, from $I_5$ by $*$
    1. $A \to * \cdot, +/*/a/\$$

## Ex 4.7.4

说明下面的文法是 LALR（1）的，但不是 SLR（1）的。

$$
S \to Aa \mid bAc \mid dc \mid bda \\
A \to d
$$

Answer:

提取左公因子和消除左递归后得到：

$$
S' \rightarrow S\\
S \rightarrow Aa \mid bB \mid dc\\
B \rightarrow Ac \mid da\\
A \rightarrow d
$$

### SLR（1）

写出所有集族, 然后考虑以下集族：

1. $I_4$
   1. $S \to d \cdot c$
   2. $S \to d \cdot$
2. $I_5$ from $I_4$ by $c$
   1. $S \to dc \cdot$

同时 $\text{FOLLOW}(A) = \{a,c\}$, 那么 $I_4$ 存在归约 $d$ 还是移进 $c$ 的移进-归约冲突, 所以该文法不是 SLR（1）的

### LALR（1）

此时与 SLR（1）对应的集族为：

1. $I_4$
   1. $S \to d \cdot c, \$$
   2. $S \to d \cdot, a$
2. $I_5$ from $I_4$ by $c$
   1. $S \to dc \cdot, \$$

此时 $d$ 不能被归约, 因此不存在移进-归约冲突, 所以该文法是 LALR（1）的

## Ex 4.7.5

说明下面的文法是 LR（1）的，但不是 LALR（1）的。

$$
S \to Aa \mid bAc \mid Bc \mid bBa
A \to d
B \to d
$$

Answer:

提取左公因子和消除左递归后得到：

$$
S' \rightarrow S\\
S \rightarrow Aa \mid bC \mid Bc\\
A \rightarrow d\\
B \rightarrow d\\
C \rightarrow Ac \mid Ba
$$

### LALR（1）

写出所有 LR（1）集族, 然后合并同心集族, 考虑以下 LALR（1）集族：

1. $I_5$
   1. $A \to d \cdot, a/c$
   2. $B \to d \cdot, a/c$

此时对于 $A$ 和 $B$ 来说 $d$ 都可以被规则 2 和规则 3 归约, 因此存在归约-归约冲突, 所以该文法不是 LALR（1）的

### LR（1）

写出所有 LR（1）集族, 不合并同心集族, 以下 LR（1）集族为与上文 LALR（1）集族对应的集族：

1. $I_5$
   1. $A \to d \cdot, a$
   2. $B \to d \cdot, c$
2. $I_6$
   1. $A \to d \cdot, c$
   2. $B \to d \cdot, a$

此时对于 $A$ 和 $B$ 来说 $d$ 要么被规则 2 归约, 要么被规则 3 归约, 因此不存在归约-归约冲突, 所以该文法是 LR（1）的
