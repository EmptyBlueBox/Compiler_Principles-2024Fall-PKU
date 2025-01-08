# 编译原理作业 01

<center><div style='height:2mm;'></div><div style="font-size:10pt;">梁昱桐 2100013116</div></center>

<center><span style="font-size:9pt;line-height:9mm"><i>Peking University</i></span></center>

## 练习 3.3.2

试描述下列正则表达式定义的语言：

1. `a(a|b)*a`
2. `((ε|a)b*)*`
3. `(a|b)*a(a|b)(a|b)`
4. `a*ba*ba*ba*`
5. `(aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*`

Answer:

1. 用 `a` 开头，以 `a` 结尾, 中间有任意个 `a` 或 `b` 的 **长度大于等于 2** 串.
2. 用 `a` 和 `b` 组成的任意串.
   1. 这是因为外层的 `*` 可以允许其所作用的部分在匹配过程中被重新评估, 也即 `(ε|a)b*` 每次重复可以是不同的字符串.
3. 倒数第三个字符是 `a` 的由 `a` 和 `b` 组成的字符串.
4. 有且仅有 3 个 `b` 的由 `a` 和 `b` 组成的字符串.
5. 拥有偶数个 `a` 和偶数个 `b` 的由 `a` 和 `b` 组成的字符串
   1. 任意一个连续的 `a` 或连续的 `b` 之间的转换都可以被子 pattern `(ab|ba)(aa|bb)*(ab|ba)(aa|bb)*` 所描述.
   2. 之后只需要在前面添加任意个 `aa` 或 `bb` 即可描述一个拥有偶数个 `a` 和偶数个 `b` 的由 `a` 和 `b` 组成的字符串.

## 练习 3.3.3

试说明在一个长度为 `n` 的字符串中，分别有多少个：

1. 前缀
2. 后缀
3. 真前缀
4. 子串
5. 子序列

Answer:

1. 前缀：$n + 1$
2. 后缀：$n + 1$
3. 真前缀：$\max\{0, n - 1\}$ , 需要考虑 $n == 0$ 的情况
4. 子串：$\frac{n(n + 1)}{2} + 1$
5. 子序列：$2^n$

## 练习 3.3.5

试写出下列语言的正则定义：

1. 包含 5 个元音的所有小写字母串，这些串中的元音按顺序出现

    Answer:

    ```
    not_vowel -> [bcdfghjklmnpqrstvwxyz]
    ans -> (not_vowel)*a(a|not_vowel)*e(e|not_vowel)*i(i|not_vowel)*o(o|not_vowel)*u(u|not_vowel)*
    ```

2. 所有由按词典递增排列的小写字母组成的串

    Answer:

    ```
    ans -> a*b*c*d*e*f*g*h*i*j*k*l*m*n*o*p*q*r*s*t*u*v*w*x*y*z*
    ```

3. 注释，即 `/*` 和 `*/` 之间的串，且串中没有不在双引号 ("") 中的 `*/`

    Answer:

   <img src="./answer-01-yutong.assets/CleanShot 2024-11-14 at 12.49.28@2x.png" alt="CleanShot 2024-11-14 at 12.49.28@2x" style="zoom:30%;" />
   
4. 所有由偶数个 a 和奇数个 b 构成的串：

    Answer:

    ```
    (aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*b(aa|bb)*((ab|ba)(aa|bb)*(ab|ba)(aa|bb)*)*
    ```

    第一题第五问复制两遍，中间单走一个 b

5. 所有由 a 和 b 组成且不含子序列 abb 的串

    Answer:
    ```
    b*a*b?
    ```

    注意这里是子序列不是子串
