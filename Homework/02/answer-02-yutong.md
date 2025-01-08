# 编译原理作业 02

<center><div style='height:2mm;'></div><div style="font-size:10pt;">梁昱桐 2100013116</div></center>

<center><span style="font-size:9pt;line-height:9mm"><i>Peking University</i></span></center>

## 练习 3.6.2

为练习3.3.5中的每一个语言 (1, 2, 3, 6, 9) 设计一个 DFA 或 NFA。

**1. 包含 5 个元音的所有小写字母串，这些串中的元音按顺序出现。**

Answer:

not_vowel $\rightarrow$ `b|c|d|f|g|h|j|k|l|m|n|p|q|r|s|t|v|w|x|y|z`

this $\rightarrow$ `(not_vowel)*a(a|not_vowel)*e(e|not_vowel)*i(i|not_vowel)*o(o|not_vowel)*u(u|not_vowel)*`

<img src="./answer-02-yutong.assets/3.6.2.1.svg" alt="3.6.2.1" style="zoom:100%;" />

**2. 所有由按词典递增排列的小写字母组成的串。**

Answer:

this $\rightarrow$ `a*b*c*d*e*f*g*h*i*j*k*l*m*n*o*p*q*r*s*t*u*v*w*x*y*z*`

![3.6.2.2](./answer-02-yutong.assets/3.6.2.2.svg)

**3. 注释，即 `/*` 和 `*/` 之间的串，且串中没有不在双引号 ("") 中的 `*/`.**

Answer:

this $\rightarrow$ `\/\*(".*"|[^\*]*|\*+[^\/]*)*\*\/`

在起始和结束的 `/*` 和 `*/` 之间, 要么是引号里的任意字符串; 要么是没有 `*` 的任意组合; 要么是以 `*` 开头但是不直接连接 `/` 的任意组合.

![3.6.2.3](./answer-02-yutong.assets/3.6.2.3.svg)

**6. 所有由偶数个 `a` 和奇数个 `b` 构成的串。**

Answer:

this $\rightarrow$ `(aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*b(aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*`

![3.6.2.6](./answer-02-yutong.assets/3.6.2.6.svg)

**9. 所有由 `a` 和 `b` 组成且不含子序列 `abb` 的串。**

Answer:

this $\rightarrow$ `b*a*(ϵ|b)`

出现 `a` 后，只能有一个 `b`。

![3.6.2.9](./answer-02-yutong.assets/3.6.2.9.svg)
