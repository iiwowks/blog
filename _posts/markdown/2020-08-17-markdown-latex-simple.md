---
layout:        post
title:         "latex公式快速查询"
date:          2020-08-17
category:      Markdown
author:        iiwowks
published:     true
latex:         true
---

1. To see how any formula was written in any question or answer, including this one, right-click on the expression it and choose "Show Math As > TeX Commands". (When you do this, the '$' will not display. Make sure you add these. See the next point.)

2. **For inline formulas, enclose the formula in `$...$`. For displayed formulas, use `$$...$$`.**
    These render differently. For example, type
    `$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$`
    to show ∑*n**i*=0*i*2=(*n*2+*n*)(2*n*+1)6 (which is inline mode) or type
    `$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$`
    to show*n*∑*i*=0*i*2=(*n*2+*n*)(2*n*+1)6(which is display mode).

3. For **Greek letters**, use `\alpha`, `\beta`, …, `\omega`: *α*,*β*,…*ω*. For uppercase, use `\Gamma`, `\Delta`, …, `\Omega`: Γ,Δ,…,Ω.

4. For **superscripts and subscripts**, use `^` and `_`. For example, `x_i^2`: *x*2*i*, `\log_2 x`: log2*x*.

5. **Groups**. Superscripts, subscripts, and other operations apply only to the next “group”. A “group” is either a single symbol, or any formula surrounded by curly braces `{`…`}`. If you do `10^10`, you will get a surprise: 1010. But `10^{10}` gives what you probably wanted: 1010. Use curly braces to delimit a formula to which a superscript or subscript applies: `x^5^6` is an error; `{x^y}^z` is *x**y**z*, and `x^{y^z}` is *x**y**z*. Observe the difference between `x_i^2` *x*2*i* and `x_{i^2}` *x**i*2.

6. **Parentheses** Ordinary symbols `()[]` make parentheses and brackets (2+3)[4+4]. Use `\{` and `\}` for curly braces {}.

    These do *not* scale with the formula in between, so if you write `(\frac{\sqrt x}{y^3})` the parentheses will be too small: (√*x**y*3). Using `\left(`…`\right)` will make the sizes adjust automatically to the formula they enclose: `\left(\frac{\sqrt x}{y^3}\right)` is (√*x**y*3).

    `\left` and`\right` apply to all the following sorts of parentheses: `(` and `)` (*x*), `[` and `]` [*x*], `\{` and `\}` {*x*}, `|` |*x*|, `\vert` |*x*|, `\Vert` ‖*x*‖, `\langle` and `\rangle` ⟨*x*⟩, `\lceil` and `\rceil` ⌈*x*⌉, and `\lfloor` and `\rfloor` ⌊*x*⌋. `\middle` can be used to add additional dividers. There are also invisible parentheses, denoted by `.`: `\left.\frac12\right\rbrace` is 12}.

    If manual size adjustments are required: `\Biggl(\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\Biggr)` gives (((((*x*))))).

7. **Sums and integrals** `\sum` and `\int`; the subscript is the lower limit and the superscript is the upper limit, so for example `\sum_1^n` ∑*n*1. Don't forget `{`…`}` if the limits are more than a single symbol. For example, `\sum_{i=0}^\infty i^2` is ∑∞*i*=0*i*2. Similarly, `\prod` ∏, `\int` ∫, `\bigcup` ⋃, `\bigcap` ⋂, `\iint` ∬, `\iiint` ∭, `\idotsint` ∫⋯∫.

8. **Fractions** There are [three ways to make these](https://math.meta.stackexchange.com/q/12978/3111). `\frac ab` applies to the next two groups, and produces *a**b*; for more complicated numerators and denominators use `{`…`}`: `\frac{a+1}{b+1}` is *a*+1*b*+1. If the numerator and denominator are complicated, you may prefer `\over`, which splits up the group that it is in: `{a+1\over b+1}` is *a*+1*b*+1. Using `\cfrac{a}{b}` command is useful for continued fractions *a**b*, more details for which [are given in this sub-article](https://math.meta.stackexchange.com/a/5058/3111).

9. **Fonts**

    - Use `\mathbb` or `\Bbb` for "blackboard bold": CHNQRZ.
    - Use `\mathbf` for boldface: **A****B****C****D****E****F****G****H****I****J****K****L****M****N****O****P****Q****R****S****T****U****V****W****X****Y****Z** **a****b****c****d****e****f****g****h****i****j****k****l****m****n****o****p****q****r****s****t****u****v****w****x****y****z**.
    - Use `\mathit` for italics: ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz.
    - Use `\pmb` for boldfaced italics: *A**B**C**D**E**F**G**H**I**J**K**L**M**N**O**P**Q**R**S**T**U**V**W**X**Y**Z**A**B**C**D**E**F**G**H**I**J**K**L**M**N**O**P**Q**R**S**T**U**V**W**X**Y**Z* *a**b**c**d**e**f**g**h**i**j**k**l**m**n**o**p**q**r**s**t**u**v**w**x**y**z**a**b**c**d**e**f**g**h**i**j**k**l**m**n**o**p**q**r**s**t**u**v**w**x**y**z*.
    - Use `\mathtt` for "typewriter" font: ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz.
    - Use `\mathrm` for roman font: ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz.
    - Use `\mathsf` for sans-serif font: ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz.
    - Use `\mathcal` for "calligraphic" letters: ABCDEFGHIJKLMNOPQRSTUVWXYZ
    - Use `\mathscr` for script letters: ABCDEFGHIJKLMNOPQRSTUVWXYZ
    - Use `\mathfrak` for "Fraktur" (old German style) letters: ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz.

10. **Radical signs** Use `sqrt`, which adjusts to the size of its argument: `\sqrt{x^3}` √*x*3; `\sqrt[3]{\frac xy}` 3√*x**y*. For complicated expressions, consider using `{...}^{1/2}` instead.

11. Some **special functions** such as "lim", "sin", "max", "ln", and so on are normally set in roman font instead of italic font. Use `\lim`, `\sin`, etc. to make these: `\sin x` sin*x*, not `sin x` *s**i**n**x*. Use subscripts to attach a notation to `\lim`: `\lim_{x\to 0}`lim*x*→0

12. There are a very large number of **special symbols and notations**, too many to list here; see [this shorter listing](http://pic.plover.com/MISC/symbols.pdf), or [this exhaustive listing](https://www.ctan.org/tex-archive/info/symbols/comprehensive/symbols-a4.pdf). Some of the most common include:

    - `\lt \gt \le \leq \leqq \leqslant \ge \geq \geqq \geqslant \neq` <>≤≤≦⩽≥≥≧⩾≠. You can use `\not` to put a slash through almost anything: `\not\lt` ≮ but it often looks bad.
    - `\times \div \pm \mp` ×÷±∓. `\cdot` is a centered dot: *x*⋅*y*
    - `\cup \cap \setminus \subset \subseteq \subsetneq \supset \in \notin \emptyset \varnothing` ∪∩∖⊂⊆⊊⊃∈∉∅*∅*
    - `{n+1 \choose 2k}` or `\binom{n+1}{2k}` (*n*+12*k*)
    - `\to \rightarrow \leftarrow \Rightarrow \Leftarrow \mapsto` →→←⇒⇐↦
    - `\land \lor \lnot \forall \exists \top \bot \vdash \vDash` ∧∨¬∀∃⊤⊥⊢⊨
    - `\star \ast \oplus \circ \bullet` ⋆∗⊕∘∙
    - `\approx \sim \simeq \cong \equiv \prec \lhd \therefore` ≈∼≃≅≡≺⊲∴
    - `\infty \aleph_0` ∞ℵ0 `\nabla \partial` ∇∂ `\Im \Re` ℑℜ
    - For modular equivalence, use `\pmod` like this: `a\equiv b\pmod n` *a*≡*b*(mod*n*).
    - `\ldots` is the dots in *a*1,*a*2,…,*a**n* `\cdots` is the dots in *a*1+*a*2+⋯+*a**n*
    - Some Greek letters have variant forms: `\epsilon \varepsilon` *ϵ**ε*, `\phi \varphi` *ϕ**φ*, and others. Script lowercase l is `\ell` *ℓ*.

    [Detexify](http://detexify.kirelabs.org/classify.html) lets you draw a symbol on a web page and then lists the *T**E**X* symbols that seem to resemble it. These are not guaranteed to work in MathJax but are a good place to start. To check that a command is supported, note that MathJax.org maintains a [list of currently supported *L**A**T**E**X* commands](http://docs.mathjax.org/en/latest/tex.html#supported-latex-commands), and one can also check Dr. Carol JVF Burns's page of [*T**E**X* Commands Available in MathJax](http://www.onemathematicalcat.org/MathJaxDocumentation/TeXSyntax.htm).

13. **Spaces** MathJax usually decides for itself how to space formulas, using a complex set of rules. Putting extra literal spaces into formulas will not change the amount of space MathJax puts in: `a␣b` and `a␣␣␣␣b` are both *a**b*. To add more space, use `\,` for a thin space *a**b*; `\;` for a wider space *a**b*. `\quad` and `\qquad` are large spaces: *a**b*, *a**b*.

    To set plain text, use `\text{…}`: {*x*∈*s*∣*x* is extra large}. You can nest `$…$` inside of `\text{…}`, for example to access spaces.

14. **Accents and diacritical marks** Use `\hat` for a single symbol ˆ*x*, `\widehat` for a larger formula ^*x**y*. If you make it too wide, it will look silly. Similarly, there are `\bar` ˉ*x* and `\overline` ¯*x**y**z*, and `\vec` →*x* and `\overrightarrow` →*x**y* and `\overleftrightarrow` ↔*x**y*. For dots, as in *d**d**x**x*˙*x*=˙*x*2+*x*¨*x*, use `\dot` and `\ddot`.

15. Special characters used for MathJax interpreting can be escaped using the `\` character: `\$` $, `\{` {, `\_` _, etc. If you want `\` itself, you should use `\backslash` ∖, because `\\` is for a new line.