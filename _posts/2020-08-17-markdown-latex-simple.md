---
layout: post
title: "latex公式快速查询"
date: 2020-08-17
category: Others
author: zhengjunan
published: true
latex: true
---

1.  To see how any formula was written in any question or answer, including this one, right-click on the expression it and choose "Show Math As > TeX Commands". (When you do this, the '$' will not display. Make sure you add these. See the next point.)

2.  **For <mark>inline formulas</mark>**, enclose the formula in `$...$`. For displayed formulas, use `$$...$$`.
    These render differently. For example, type `$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$` to show $ \sum*{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6} $ (which is inline mode) or type `$$\sum*{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$` to show : (which is display mode)

        $$
        \sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}
        $$

3.  For **<mark>Greek letters</mark>**, use `\alpha`, `\beta`, ... , `\omega`: $\alpha$, $\beta$, ... , $\omega$. For uppercase, use `\Gamma`, `\Delta`, …, `\Omega`: $\Gamma$, $\Delta$, ... , $\Omega$.

4.  For **<mark>superscripts and subscripts</mark>**, use `^` and `_`. For example, `x_i^2`: $x_i^2$ , `\log_2 x`: $\log_2 x$.

5.  **<mark>Groups</mark>**. Superscripts, subscripts, and other operations apply only to the next “group”. A “group” is either a single symbol, or any formula surrounded by curly braces `{`…`}`. If you do `10^10`, you will get a surprise: 1010. But `10^{10}` gives what you probably wanted: 1010. Use curly braces to delimit a formula to which a superscript or subscript applies: `x^5^6` is an error; `{x^y}^z` is ${x^y}^z$ , and `x^{y^z}` is $x^{y^z}$ . Observe the difference between `x_i^2` $x_i^2$ and `x_{i^2}` $x_{i^2}$ .

6.  **<mark>Parentheses</mark>** Ordinary symbols `()[]` make parentheses and brackets (2+3)[4+4]. Use `\{` and `\}` for curly braces {}.
    These do _not_ scale with the formula in between, so if you write `(\frac{\sqrt x}{y^3})` the parentheses will be too small: $\frac{\sqrt x}{y^3}$.
    Using `\left(`…`\right)` will make the sizes adjust automatically to the formula they enclose: `\left(\frac{\sqrt x}{y^3}\right)` is: $\left(\frac{\sqrt x}{y^3}\right)$.

- `\left` and`\right` apply to all the following sorts of parentheses:
- `(` and `)`: $(x)$
- `[` and `]`: $[x]$
- `\{` and `\}`: $\{ x \}$ $\lbrace x \rbrace$
- `|`: $\|$
- `\vert`: $\vert x \vert$
- `\Vert`: $\Vert x \Vert$,
- `\langle` and `\rangle`: $\langle x \rangle$
- `\lceil` and `\rceil`: $\lceil x \rceil$
- `\lfloor` and `\rfloor`: $\lfloor x \rfloor$
- `\middle` can be used to add additional dividers. There are also invisible parentheses, denoted by `.`: `\left.\frac12\right\rbrace` is $\left.\frac 12 \right \rbrace $.
- If manual size adjustments are required:`\Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr)` gives $\Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr)$.

7. **<mark>Sums and integrals</mark>** `\sum` and `\int`; the subscript is the lower limit and the superscript is the upper limit, so for example `\sum_1^n` $\sum_1^n$. Don't forget `{`…`}` if the limits are more than a single symbol.
   For example, `\sum_{i=0}^\infty i^2` is $\sum_{i=0}^\infty i^2$. Similarly, `\prod` $\prod$, `\int` $\int$, `\bigcup` $\bigcup$, `\bigcap` $\bigcap$, `\iint` $\iint$, `\iiint` $\iiint$, `\idotsint` $\idotsint$.

8. **<mark>Fractions</mark>** There are [three ways to make these](https://math.meta.stackexchange.com/q/12978/3111). `\frac ab` applies to the next two groups, and produces $\frac ab$; for more complicated numerators and denominators use `{`…`}`: `\frac{a+1}{b+1}` is $\frac{a+1}{b+1}$. If the numerator and denominator are complicated, you may prefer `\over`, which splits up the group that it is in: `{a+1\over b+1}` is ${a+1\over b+1}$. Using `\cfrac{a}{b}` command is useful for continued fractions $\cfrac{a}{b}$, more details for which [are given in this sub-article](https://math.meta.stackexchange.com/a/5058/3111).

9. **<mark>Fonts</mark>**

   - Use `\mathbb` or `\Bbb` for "blackboard bold": $\mathbb{CHNQRZ}$.
   - Use `\mathbf` for boldface: $\mathbf{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\mathit` for italics: $\mathit{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\pmb` for boldfaced italics: $\pmb{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\mathtt` for "typewriter" font: $\mathtt{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\mathrm` for roman font: $\mathrm{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\mathsf` for sans-serif font: $\mathsf{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$.
   - Use `\mathcal` for "calligraphic" letters: $\mathcal{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$
   - Use `\mathscr` for script letters: $\mathscr{ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz}$
   - Use `\mathfrak` for "Fraktur" (old German style) letters: $\mathfrak{ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz}$.

10. **<mark>Radical signs</mark>** Use `sqrt`, which adjusts to the size of its argument: `\sqrt{x^3}` $\sqrt{x^3}$; `\sqrt[3]{\frac xy}` $\sqrt[3]{\frac cy}$. For complicated expressions, consider using `{...}^{1/2}` instead.
11. **<mark>Radical signs</mark>** Use `sqrt`, which adjusts to the size of its argument: `\sqrt{x^3}` $\sqrt{x^3}$; `\sqrt[3]{\frac xy}` $\sqrt[3]{\frac cy}$. For complicated expressions, consider using `{...}^{1/2}` instead.

12. Some **<mark>special functions</mark>** such as "lim", "sin", "max", "ln", and so on are normally set in roman font instead of italic font. Use `\lim`, `\sin`, etc. to make these: `\sin x` $\sin x$, not `sin x` $sin x$. Use subscripts to attach a notation to `\lim`: `\lim_{x\to 0}`$\lim_{x\to 0}$

13. There are a very large number of **<mark>special symbols and notations</mark>**, too many to list here; see [this shorter listing](http://pic.plover.com/MISC/symbols.pdf), or [this exhaustive listing](https://www.ctan.org/tex-archive/info/symbols/comprehensive/symbols-a4.pdf). Some of the most common include:

    - `\lt \gt \le \leq \leqq \leqslant \ge \geq \geqq \geqslant \neq` $\lt \gt \le \leq \leqq \leqslant \ge \geq \geqq \geqslant \neq $. You can use `\not` to put a slash through almost anything: `\not\lt` $\not\lt$ but it often looks bad.
    - `\times \div \pm \mp` $\times \div \pm \mp$. `\cdot` is a centered dot: $x \cdot y$
    - `\cup \cap \setminus \subset \subseteq \subsetneq \supset \in \notin \emptyset \varnothing` $\cup \cap \setminus \subset \subseteq \subsetneq \supset \in \notin \emptyset \varnothing $
    - `{n+1 \choose 2k}` or `\binom{n+1}{2k}` ${n+1 \choose 2k} \binom{n+1}{2k}$
    - `\to \rightarrow \leftarrow \Rightarrow \Leftarrow \mapsto` $\to \rightarrow \leftarrow \Rightarrow \Leftarrow \mapsto$
    - `\land \lor \lnot \forall \exists \top \bot \vdash \vDash` $\land \lor \lnot \forall \exists \top \bot \vdash \vDash$
    - `\star \ast \oplus \circ \bullet` $\star \ast \oplus \circ \bullet$
    - `\approx \sim \simeq \cong \equiv \prec \lhd \therefore` $\approx \sim \simeq \cong \equiv \prec \lhd \therefore$
    - `\infty \aleph_0` $\infty \aleph_0$ `\nabla \partial` $\nabla \partial$ `\Im \Re` $\Im \Re$
    - For modular equivalence, use `\pmod` like this: `a\equiv b\pmod n` $a\equiv b\pmod n$.
    - `\ldots` is the dots in $a_1, a_2, \ldots, a_n$ `\cdots` is the dots in $a_1 + a_2 + \cdots + a_n$
    - Some Greek letters have variant forms: `\epsilon \varepsilon` $\epsilon \varepsilon$, `\phi \varphi` $\phi \varphi$, and others. Script lowercase l is `\ell` $\ell$.
    - [Detexify](http://detexify.kirelabs.org/classify.html) lets you draw a symbol on a web page and then lists the TEX symbols that seem to resemble it. These are not guaranteed to work in MathJax but are a good place to start. To check that a command is supported, note that MathJax.org maintains a [list of currently supported LATEX commands](http://docs.mathjax.org/en/latest/tex.html#supported-latex-commands), and one can also check Dr. Carol JVF Burns's page of [LATEX Commands Available in MathJax](http://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm).

14. **<mark>Spaces</mark>** MathJax usually decides for itself how to space formulas, using a complex set of rules. Putting extra literal spaces into formulas will not change the amount of space MathJax puts in: `a␣b` and `a␣␣␣␣b` are both $a␣b$. To add more space, use `\,` for a thin space $a\ b$; `\quad` and `\qquad` are large spaces: $a \quad b$, $a \qquad b$.

    - To set plain text, use `\text{…}`: $\{ x\in s \| \text{x is extra large}\}$. You can nest `$…$` inside of `\text{…}`, for example to access spaces.

15. **<mark>Accents and diacritical marks</mark>** Use `\hat` for a single symbol $\hat x$, `\widehat` for a larger formula $\widehat {xy}$. If you make it too wide, it will look silly. Similarly, there are `\bar` $\bar{x}$ and `\overline` $\overline{xyz}$, and `\vec` $\vec{x}$ and `\overrightarrow` $\overrightarrow{xy}$ and `\overleftrightarrow` $\overleftrightarrow{xyz}$. For dots, as in $\dot{x}$ $\ddot{x}$, use `\dot` and `\ddot`.

16. **<mark>Special characters</mark>** used for MathJax interpreting can be escaped using the `\` character: `\$` $ \$ $, `\{` $\{$, `\_` $\_$, etc. If you want `\` itself, you should use `\backslash` $\backslash$, because `\\` is for a new line.

### [转载文章](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
