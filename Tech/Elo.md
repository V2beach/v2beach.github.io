<!-- ex_nolevel -->
# Elo Rating System
https://en.wikipedia.org/wiki/Elo_rating_system

The Elo rating system is a method for calculating the relative skill levels of players in zero-sum games such as chess or esports. It is named after its creator Arpad Elo, a Hungarian-American physics professor. (Educated in public primary and secondary schools, he earned his BS (22歲) and MS (25歲) degrees, **in Physics**, from the University of Chicago.)

西洋棋的elo rating在[這裡](https://ratings.fide.com/top_lists.phtml)，我的[dota](https://www.dotabuff.com/players/443839701/matches)和[chess](https://www.chess.com/member/dopedashenone)在這裡。

Pairwise comparisons form the basis of the Elo rating methodology.

https://github.com/V2beach/books/blob/main/1978-elo-theratingofchessplayerspastandpresent.pdf

![pairwise comparison](/assets/Pairwise+Comparison+Matrix+Manual+Spreadsheet+Method+Calculator+Example.png)

Elo's central assumption was that the chess performance of each player in each game is a normally distributed random variable. Although a player might perform significantly better or worse from one game to the next, Elo assumed that the mean value of the performances of any given player changes only slowly over time. Elo thought of a player's true skill as the mean of that player's performance random variable.

A further assumption is necessary because chess performance in the above sense is still not measurable. One cannot look at a sequence of moves and derive a number to represent that player's skill. Performance can only be inferred from wins, draws, and losses. Therefore, a player who wins a game is assumed to have performed at a higher level than the opponent for that game. Conversely, a losing player is assumed to have performed at a lower level. If the game ends in a draw, the two players are assumed to have performed at nearly the same level.

[實踐中存在很多問題。](https://en.wikipedia.org/wiki/Elo_rating_system#Practical_issues)
## Mathematical details
如果玩家A的rating是RA，玩家B的當前分數是RB，玩家A預測分數的公式（using the [logistic curve](https://en.wikipedia.org/wiki/Logistic_curve) with [base 10](https://en.wikipedia.org/wiki/Common_logarithm)）是  
{%math%}E_{\mathrm{A}}=\frac{1}{1+10^{\left(R_{\mathrm{B}}-R_{\mathrm{A}}\right) / 400}} .{%endmath%}  
相似地，B的預期分數是  
{%math%}E_{\mathrm{B}}=\frac{1}{1+10^{\left(R_{\mathrm{A}}-R_{\mathrm{B}}\right) / 400}} .{%endmath%}  
也可以表示為  
{%math%}E_A=\frac{Q_A}{Q_A+Q_B}{%endmath%}  
和  
{%math%}E_B=\frac{Q_B}{Q_A+Q_B},{%endmath%}  
其中{%math%}Q_A=10^{R_A/400}{%endmath%}{%math%}Q_B=10^{R_B/400}{%endmath%}。這個logistic函數的曲線如下，

![player's expected score function graph](/assets/Screenshot 2024-11-04 at 22.57.34.png)

其實就是用分差把預期分數約束到0到1之間，其中勝利是1，失敗是0。

假設玩家A（當前分數{%math%}R_A{%endmath%}）的預期分數是{%math%}E_A{%endmath%}但是實際得分是{%math%}S_A{%endmath%}，玩家更新分數的公式是
{%math%}R_{\mathrm{A}}^{\prime}=R_{\mathrm{A}}+K \cdot\left(S_{\mathrm{A}}-E_{\mathrm{A}}\right).{%endmath%}

K-factor set at K=16  for masters and K=32 for weaker players.

Moreover, online judge sites are also using Elo rating system or its derivatives. For example, Topcoder is using a modified version based on normal distribution, while Codeforces is using another version based on logistic distribution.

Formal derivation for win/loss games  
The above expressions can be now formally derived by exploiting the link between the Elo rating and the stochastic gradient update in the logistic regression.有的用隨機梯度更新分數

## Logistic/Sigmoid
<p>A <b>logistic function</b> or <b>logistic curve</b> is a common S-shaped curve (<a href="https://en.wikipedia.org/wiki/Sigmoid_function" title="Sigmoid function">sigmoid curve</a>) with the equation.</p>  

{%math%}f(x)=\frac{L}{1+e^{-k\left(x-x_0\right)}}{%endmath%}

where
- L is the carrying capacity, the supremum of the values of the function;
- k is the logistic growth rate, the steepness of the curve; and
- x0 is the x value of the function's midpoint.
The logistic function has domain the real numbers, the limit as x→−∞ is 0, and the limit as x→+∞ is L.

<img src="/assets/Logistic-curve.svg.png" width="50%" height="50%" alt="Standard logistic function where L=1,k=1,x0=0.">

>sup(X)是取上限函数，inf(X) 是取下限函数。 sup是supremum的简写，意思是：上确界，最小上界。 inf是infimum的简写，意思是：下确界，最大下界。
<img src="/assets/Minimum-maximum-infimum-and-supremum-of-example-functions.ppm.png" width="50%" height="50%">

A ***sigmoid function*** refers specifically to a function whose graph follows the logistic function. It is defined by the formula:

{%math%}\sigma(x)=\frac{1}{1+e^{-x}}=\frac{e^x}{1+e^x}=1-\sigma(-x) .{%endmath%}

<img src="https://blog.v2beach.cn/pics/cs231n/sigmoid.png" width="50%" height="50%" alt="Some sigmoid functions compared. In the drawing all functions are normalized in such a way that their slope at the origin is 1.">

The logistic function was introduced in a series of three papers by Pierre François **Verhulst** between 1838 and 1847, who devised it as **a model of population growth by adjusting the exponential growth model**。

Exponential Growth：

<style>
    .legend-color{
        display: inline-block;
        min-width: 1.25em;
        height: 1.25em;
        line-height: 1.25;
        margin: 1px 0;
        text-align: center;
        border: 1px solid black
    }
</style>

<img src="/assets/Exponential.svg.png" width="50%" height="50%" alt="The graph illustrates how exponential growth (green) surpasses both linear (red) and cubic (blue) growth."/>

<div class="legend"><span class="legend-color mw-no-invert" style="background-color:red; color:black;">&nbsp;</span>&nbsp;Linear growth</div>
<div class="legend"><span class="legend-color mw-no-invert" style="background-color:blue; color:white;">&nbsp;</span>&nbsp;<a href="https://en.wikipedia.org/wiki/Polynomial" title="Polynomial">Cubic growth</a></div>
<div class="legend"><span class="legend-color mw-no-invert" style="background-color:green; color:white;">&nbsp;</span>&nbsp;Exponential growth</div>

這logistic函數發明初衷是用於優化人口增長函數，在統計學和機器學習的應用只是它茫茫多應用的其中之一而已。  
所有圖像長得像logsitic函數的都是sigmoid函數(S-shaped curve)。

Logistic functions are used in several roles in statistics. For example, they are the cumulative distribution function of the logistic family of distributions, and they are, a bit simplified, used to model the chance a chess player has to beat their opponent in the Elo rating system. More specific examples now follow.

## Logistic regression
Logistic functions are used in logistic regression to model how the probability p of an event may be affected by one or more explanatory variables: an example would be to have the model

{%math%}p = f(a + bx),{%endmath%}

where x is the explanatory variable, a and b are model parameters to be fitted, and f is the standard logistic function.

Logistic regression and other **log-linear models** are also commonly used in machine learning. A generalisation of the logistic function to multiple inputs is the softmax activation function, used in multinomial logistic regression.

## Log-linear
先複習一下，線性回歸是{%math%}y_i(x)=\beta_0+\beta_1x_i{%endmath%}，

![graph](/assets/1*F8xLapWs4stL93NEO5NPeQ.webp)

把數據{%math%}(x_i, y_i){%endmath%}代入之後，用最小平方法(Least Square)計算loss function目標/損失函數，
{%math%}{Loss}\left({\beta}_0, {\beta}_1\right)=\sum_{i=1}^n\left(y_i-\hat{y}_i\right)^2=\sum_{i=1}^n\left(y_i-\left({\beta}_0+{\beta}_1 x_i\right)\right)^2{%endmath%}
之後更新beta修正函數擬合數據。

而log-linear就是把a+bx結果代入logistic或者其他sigmoid函數，好處是比如對分類任務來說，这个Sigmoid Function可以将线性的值，映射到\[0-1\]范围中。如果映射结果小于0.5，则认为是负的样本，如果是大于0.5，则认为是正的样本。

## 採用logistic分布和gaussian/normal分布的區別？
A workable rating system, fully developed from basic theory, includes certain principal components:
1. Rating scale
2. Performance distribution function
3. Percentage expectancy function
4. Performance rating formula
5. Continuous rating formula
6. Appropriate numerical coefficients and ancillary formulae
—— 8.12 [The Rating of Chessplayers, Past & Present, Second Edition, Arpad E. Elo](https://gwern.net/doc/statistics/order/comparison/1978-elo-theratingofchessplayerspastandpresent.pdf)

區別就是預期分數（player's expected score）的計算公式，上面用的logistic function(base10)其實就是logistic distribution的CDF，可以發現如下圖所示跟normal distribution的CDF很像。

- In probability theory and statistics, the logistic distribution is a continuous probability distribution.
- **Its cumulative distribution function is the logistic function, which appears in logistic regression and feedforward neural networks.**
- It resembles the normal distribution in shape but has heavier tails (higher kurtosis).

logistic distribution其實就是尾部更長的normal distribution了。

<table class="infobox infobox-table ib-prob-dist"><tbody><tr><td colspan="4">Logistic distribution</td><td colspan="4">Normal distribution</td></tr><tr><td colspan="4" class="infobox-image">
<div class="ib-prob-dist-image">Probability density function</div><span typeof="mw:File"><a href="/wiki/File:Logisticpdfunction.svg" class="mw-file-description" title="Standard logistic PDF"><img alt="Standard logistic PDF" src="/assets/Logisticpdfunction.svg.png" decoding="async" width="320" height="256" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/6/66/Logisticpdfunction.svg/480px-Logisticpdfunction.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/6/66/Logisticpdfunction.svg/640px-Logisticpdfunction.svg.png 2x" data-file-width="450" data-file-height="360"></a></span></td><td colspan="4" class="infobox-image"><div class="ib-prob-dist-image">Probability density function</div><span class="skin-invert-image" typeof="mw:File"><a href="/wiki/File:Normal_Distribution_PDF.svg" class="mw-file-description"><img src="/assets/Normal_Distribution_PDF.svg.png" decoding="async" width="400" height="256" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/7/74/Normal_Distribution_PDF.svg/600px-Normal_Distribution_PDF.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/7/74/Normal_Distribution_PDF.svg/800px-Normal_Distribution_PDF.svg.png 2x" data-file-width="720" data-file-height="460"></a></span><div class="infobox-caption">The red curve is the <i>standard normal distribution</i>.</div></td></tr><tr><td colspan="4" class="infobox-image">
<div class="ib-prob-dist-image">Cumulative distribution function</div><span typeof="mw:File"><a href="/wiki/File:Logistic_cdf.svg" class="mw-file-description" title="Standard logistic CDF"><img alt="Standard logistic CDF" src="/assets/Logistic_cdf.svg.png" decoding="async" width="320" height="256" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Logistic_cdf.svg/480px-Logistic_cdf.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Logistic_cdf.svg/640px-Logistic_cdf.svg.png 2x" data-file-width="450" data-file-height="360"></a></span></td><td colspan="4" class="infobox-image">
<div class="ib-prob-dist-image">Cumulative distribution function</div><span class="skin-invert-image" typeof="mw:File"><a href="/wiki/File:Normal_Distribution_CDF.svg" class="mw-file-description"><img src="/assets/Normal_Distribution_CDF.svg.png" decoding="async" width="400" height="256" class="mw-file-element" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Normal_Distribution_CDF.svg/600px-Normal_Distribution_CDF.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Normal_Distribution_CDF.svg/800px-Normal_Distribution_CDF.svg.png 2x" data-file-width="720" data-file-height="460"></a></span></td></tr><tr><th scope="row" class="infobox-label">Notation</th><td colspan="3">LogisticDistribution(μ,s)</td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle {\mathcal {N}}(\mu ,\sigma ^{2})}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mrow class="MJX-TeXAtom-ORD">
          <mrow class="MJX-TeXAtom-ORD">
            <mi class="MJX-tex-caligraphic" mathvariant="script">N</mi>
          </mrow>
        </mrow>
        <mo stretchy="false">(</mo>
        <mi>μ<!-- μ --></mi>
        <mo>,</mo>
        <msup>
          <mi>σ<!-- σ --></mi>
          <mrow class="MJX-TeXAtom-ORD">
            <mn>2</mn>
          </mrow>
        </msup>
        <mo stretchy="false">)</mo>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle {\mathcal {N}}(\mu ,\sigma ^{2})}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/863304aaa42a945f2f07d79facc3d2eebc845ce7" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; margin-left: -0.062ex; width:8.966ex; height:3.176ex;" alt="{\displaystyle {\mathcal {N}}(\mu ,\sigma ^{2})}"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Statistical_parameter" title="Statistical parameter">Parameters</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu ,}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
        <mo>,</mo>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu ,}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/1e7e1ef161a49a22b500d63307460ad92eeb6a16" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:2.049ex; height:2.176ex;" alt="{\displaystyle \mu ,}"></span> <a href="/wiki/Location_parameter" title="Location parameter">location</a> (<a href="/wiki/Real_number" title="Real number">real</a>)<br><span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle s>0,}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>s</mi>
        <mo>&gt;</mo>
        <mn>0</mn>
        <mo>,</mo>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle s&gt;0,}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/c383e7faf9b1add044f091319507fccc0f8a310f" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.671ex; width:5.998ex; height:2.509ex;" alt="{\displaystyle s>0,}"></span> <a href="/wiki/Scale_parameter" title="Scale parameter">scale</a> (real)</td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu \in \mathbb {R} }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
        <mo>∈<!-- ∈ --></mo>
        <mrow class="MJX-TeXAtom-ORD">
          <mi mathvariant="double-struck">R</mi>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu \in \mathbb {R} }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/a9a48f0e84328dc53dec2ad301bb321c00dcf422" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:5.92ex; height:2.676ex;" alt="{\displaystyle \mu \in \mathbb {R} }"></span> = <a href="/wiki/Mean" title="Mean">mean</a> (<a href="/wiki/Location_parameter" title="Location parameter">location</a>)<br><span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \sigma ^{2}\in \mathbb {R} _{>0}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <msup>
          <mi>σ<!-- σ --></mi>
          <mrow class="MJX-TeXAtom-ORD">
            <mn>2</mn>
          </mrow>
        </msup>
        <mo>∈<!-- ∈ --></mo>
        <msub>
          <mrow class="MJX-TeXAtom-ORD">
            <mi mathvariant="double-struck">R</mi>
          </mrow>
          <mrow class="MJX-TeXAtom-ORD">
            <mo>&gt;</mo>
            <mn>0</mn>
          </mrow>
        </msub>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \sigma ^{2}\in \mathbb {R} _{&gt;0}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/5b81059aaa2db87802908711c7527c0e1d65fc06" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.671ex; width:9.236ex; height:3.009ex;" alt="{\displaystyle \sigma ^{2}\in \mathbb {R} _{>0}}"></span> = <a href="/wiki/Variance" title="Variance">variance</a> (squared <a href="/wiki/Scale_parameter" title="Scale parameter">scale</a>)</td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Support_(mathematics)" title="Support (mathematics)">Support</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle x\in (-\infty ,\infty )}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>x</mi>
        <mo>∈<!-- ∈ --></mo>
        <mo stretchy="false">(</mo>
        <mo>−<!-- − --></mo>
        <mi mathvariant="normal">∞<!-- ∞ --></mi>
        <mo>,</mo>
        <mi mathvariant="normal">∞<!-- ∞ --></mi>
        <mo stretchy="false">)</mo>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle x\in (-\infty ,\infty )}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/d7aea9be5e96822459afc5c7d9f911a586290dc5" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:13.469ex; height:2.843ex;" alt="{\displaystyle x\in (-\infty ,\infty )}"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle x\in \mathbb {R} }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>x</mi>
        <mo>∈<!-- ∈ --></mo>
        <mrow class="MJX-TeXAtom-ORD">
          <mi mathvariant="double-struck">R</mi>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle x\in \mathbb {R} }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/a9c6d458566aec47a7259762034790c8981aefab" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.338ex; width:5.848ex; height:2.176ex;" alt="{\displaystyle x\in \mathbb {R} }"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Probability_density_function" title="Probability density function">PDF</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle {\frac {e^{-(x-\mu )/s}}{s\left(1+e^{-(x-\mu )/s}\right)^{2}}}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <msup>
              <mi>e</mi>
              <mrow class="MJX-TeXAtom-ORD">
                <mo>−<!-- − --></mo>
                <mo stretchy="false">(</mo>
                <mi>x</mi>
                <mo>−<!-- − --></mo>
                <mi>μ<!-- μ --></mi>
                <mo stretchy="false">)</mo>
                <mrow class="MJX-TeXAtom-ORD">
                  <mo>/</mo>
                </mrow>
                <mi>s</mi>
              </mrow>
            </msup>
            <mrow>
              <mi>s</mi>
              <msup>
                <mrow>
                  <mo>(</mo>
                  <mrow>
                    <mn>1</mn>
                    <mo>+</mo>
                    <msup>
                      <mi>e</mi>
                      <mrow class="MJX-TeXAtom-ORD">
                        <mo>−<!-- − --></mo>
                        <mo stretchy="false">(</mo>
                        <mi>x</mi>
                        <mo>−<!-- − --></mo>
                        <mi>μ<!-- μ --></mi>
                        <mo stretchy="false">)</mo>
                        <mrow class="MJX-TeXAtom-ORD">
                          <mo>/</mo>
                        </mrow>
                        <mi>s</mi>
                      </mrow>
                    </msup>
                  </mrow>
                  <mo>)</mo>
                </mrow>
                <mrow class="MJX-TeXAtom-ORD">
                  <mn>2</mn>
                </mrow>
              </msup>
            </mrow>
          </mfrac>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle {\frac {e^{-(x-\mu )/s}}{s\left(1+e^{-(x-\mu )/s}\right)^{2}}}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9d42088b22c0c7577eb7a68d827061870368d054" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -3.505ex; width:17.79ex; height:7.343ex;" alt="{\displaystyle {\frac {e^{-(x-\mu )/s}}{s\left(1+e^{-(x-\mu )/s}\right)^{2}}}}"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle {\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <mn>1</mn>
            <msqrt>
              <mn>2</mn>
              <mi>π<!-- π --></mi>
              <msup>
                <mi>σ<!-- σ --></mi>
                <mrow class="MJX-TeXAtom-ORD">
                  <mn>2</mn>
                </mrow>
              </msup>
            </msqrt>
          </mfrac>
        </mrow>
        <msup>
          <mi>e</mi>
          <mrow class="MJX-TeXAtom-ORD">
            <mo>−<!-- − --></mo>
            <mrow class="MJX-TeXAtom-ORD">
              <mfrac>
                <mrow>
                  <mo stretchy="false">(</mo>
                  <mi>x</mi>
                  <mo>−<!-- − --></mo>
                  <mi>μ<!-- μ --></mi>
                  <msup>
                    <mo stretchy="false">)</mo>
                    <mrow class="MJX-TeXAtom-ORD">
                      <mn>2</mn>
                    </mrow>
                  </msup>
                </mrow>
                <mrow>
                  <mn>2</mn>
                  <msup>
                    <mi>σ<!-- σ --></mi>
                    <mrow class="MJX-TeXAtom-ORD">
                      <mn>2</mn>
                    </mrow>
                  </msup>
                </mrow>
              </mfrac>
            </mrow>
          </mrow>
        </msup>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle {\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/2ce7e315b02666699e0cd8ea5fb1a3e0c287cd9d" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -2.838ex; width:15.527ex; height:7.176ex;" alt="{\displaystyle {\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}}"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Cumulative_distribution_function" title="Cumulative distribution function">CDF</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle {\frac {1}{1+e^{-(x-\mu )/s}}}={\frac {1+\tanh {\frac {x-\mu }{2s}}}{2}}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <mn>1</mn>
            <mrow>
              <mn>1</mn>
              <mo>+</mo>
              <msup>
                <mi>e</mi>
                <mrow class="MJX-TeXAtom-ORD">
                  <mo>−<!-- − --></mo>
                  <mo stretchy="false">(</mo>
                  <mi>x</mi>
                  <mo>−<!-- − --></mo>
                  <mi>μ<!-- μ --></mi>
                  <mo stretchy="false">)</mo>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mo>/</mo>
                  </mrow>
                  <mi>s</mi>
                </mrow>
              </msup>
            </mrow>
          </mfrac>
        </mrow>
        <mo>=</mo>
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <mrow>
              <mn>1</mn>
              <mo>+</mo>
              <mi>tanh</mi>
              <mo>⁡<!-- ⁡ --></mo>
              <mrow class="MJX-TeXAtom-ORD">
                <mfrac>
                  <mrow>
                    <mi>x</mi>
                    <mo>−<!-- − --></mo>
                    <mi>μ<!-- μ --></mi>
                  </mrow>
                  <mrow>
                    <mn>2</mn>
                    <mi>s</mi>
                  </mrow>
                </mfrac>
              </mrow>
            </mrow>
            <mn>2</mn>
          </mfrac>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle {\frac {1}{1+e^{-(x-\mu )/s}}}={\frac {1+\tanh {\frac {x-\mu }{2s}}}{2}}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/841f3507b4810bd25d4211115d9d1720edfa96eb" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -2.338ex; width:30.538ex; height:7.176ex;" alt="{\displaystyle {\frac {1}{1+e^{-(x-\mu )/s}}}={\frac {1+\tanh {\frac {x-\mu }{2s}}}{2}}}"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \Phi \left({\frac {x-\mu }{\sigma }}\right)={\frac {1}{2}}\left[1+\operatorname {erf} \left({\frac {x-\mu }{\sigma {\sqrt {2}}}}\right)\right]}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi mathvariant="normal">Φ<!-- Φ --></mi>
        <mrow>
          <mo>(</mo>
          <mrow class="MJX-TeXAtom-ORD">
            <mfrac>
              <mrow>
                <mi>x</mi>
                <mo>−<!-- − --></mo>
                <mi>μ<!-- μ --></mi>
              </mrow>
              <mi>σ<!-- σ --></mi>
            </mfrac>
          </mrow>
          <mo>)</mo>
        </mrow>
        <mo>=</mo>
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <mn>1</mn>
            <mn>2</mn>
          </mfrac>
        </mrow>
        <mrow>
          <mo>[</mo>
          <mrow>
            <mn>1</mn>
            <mo>+</mo>
            <mi>erf</mi>
            <mo>⁡<!-- ⁡ --></mo>
            <mrow>
              <mo>(</mo>
              <mrow class="MJX-TeXAtom-ORD">
                <mfrac>
                  <mrow>
                    <mi>x</mi>
                    <mo>−<!-- − --></mo>
                    <mi>μ<!-- μ --></mi>
                  </mrow>
                  <mrow>
                    <mi>σ<!-- σ --></mi>
                    <mrow class="MJX-TeXAtom-ORD">
                      <msqrt>
                        <mn>2</mn>
                      </msqrt>
                    </mrow>
                  </mrow>
                </mfrac>
              </mrow>
              <mo>)</mo>
            </mrow>
          </mrow>
          <mo>]</mo>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \Phi \left({\frac {x-\mu }{\sigma }}\right)={\frac {1}{2}}\left[1+\operatorname {erf} \left({\frac {x-\mu }{\sigma {\sqrt {2}}}}\right)\right]}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/c0fed43e25966344745178c406f04b15d0fa3783" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -2.838ex; width:36.321ex; height:6.509ex;" alt="{\displaystyle \Phi \left({\frac {x-\mu }{\sigma }}\right)={\frac {1}{2}}\left[1+\operatorname {erf} \left({\frac {x-\mu }{\sigma {\sqrt {2}}}}\right)\right]}"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Quantile_function" title="Quantile function">Quantile</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu +s\log \left({\frac {p}{1-p}}\right)}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
        <mo>+</mo>
        <mi>s</mi>
        <mi>log</mi>
        <mo>⁡<!-- ⁡ --></mo>
        <mrow>
          <mo>(</mo>
          <mrow class="MJX-TeXAtom-ORD">
            <mfrac>
              <mi>p</mi>
              <mrow>
                <mn>1</mn>
                <mo>−<!-- − --></mo>
                <mi>p</mi>
              </mrow>
            </mfrac>
          </mrow>
          <mo>)</mo>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu +s\log \left({\frac {p}{1-p}}\right)}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/30fdc436e07663fa4f425651b2d506f86c740dc2" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -2.505ex; width:18.121ex; height:6.176ex;" alt="{\displaystyle \mu +s\log \left({\frac {p}{1-p}}\right)}"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu +\sigma {\sqrt {2}}\operatorname {erf} ^{-1}(2p-1)}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
        <mo>+</mo>
        <mi>σ<!-- σ --></mi>
        <mrow class="MJX-TeXAtom-ORD">
          <msqrt>
            <mn>2</mn>
          </msqrt>
        </mrow>
        <msup>
          <mi>erf</mi>
          <mrow class="MJX-TeXAtom-ORD">
            <mo>−<!-- − --></mo>
            <mn>1</mn>
          </mrow>
        </msup>
        <mo>⁡<!-- ⁡ --></mo>
        <mo stretchy="false">(</mo>
        <mn>2</mn>
        <mi>p</mi>
        <mo>−<!-- − --></mo>
        <mn>1</mn>
        <mo stretchy="false">)</mo>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu +\sigma {\sqrt {2}}\operatorname {erf} ^{-1}(2p-1)}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/510cf4025ba141645f21c7f06866867648d5bc21" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:22.19ex; height:3.176ex;" alt="{\displaystyle \mu +\sigma {\sqrt {2}}\operatorname {erf} ^{-1}(2p-1)}"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Expected_value" title="Expected value">Mean</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Median" title="Median">Median</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Mode_(statistics)" title="Mode (statistics)">Mode</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \mu }">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mi>μ<!-- μ --></mi>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \mu }</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9fd47b2a39f7a7856952afec1f1db72c67af6161" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.838ex; width:1.402ex; height:2.176ex;" alt="{\displaystyle \mu }"></span></td></tr><tr><th scope="row" class="infobox-label"><a href="/wiki/Variance" title="Variance">Variance</a></th><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle {\frac {s^{2}\pi ^{2}}{3}}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <mrow class="MJX-TeXAtom-ORD">
          <mfrac>
            <mrow>
              <msup>
                <mi>s</mi>
                <mrow class="MJX-TeXAtom-ORD">
                  <mn>2</mn>
                </mrow>
              </msup>
              <msup>
                <mi>π<!-- π --></mi>
                <mrow class="MJX-TeXAtom-ORD">
                  <mn>2</mn>
                </mrow>
              </msup>
            </mrow>
            <mn>3</mn>
          </mfrac>
        </mrow>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle {\frac {s^{2}\pi ^{2}}{3}}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/f9e1141f49e6711939a3757111a9dc5576990db0" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -1.838ex; width:5.369ex; height:5.676ex;" alt="{\displaystyle {\frac {s^{2}\pi ^{2}}{3}}}"></span></td><td colspan="3" class="infobox-data">
<span class="mwe-math-element"><span class="mwe-math-mathml-inline mwe-math-mathml-a11y" style="display: none;"><math xmlns="http://www.w3.org/1998/Math/MathML" alttext="{\displaystyle \sigma ^{2}}">
  <semantics>
    <mrow class="MJX-TeXAtom-ORD">
      <mstyle displaystyle="true" scriptlevel="0">
        <msup>
          <mi>σ<!-- σ --></mi>
          <mrow class="MJX-TeXAtom-ORD">
            <mn>2</mn>
          </mrow>
        </msup>
      </mstyle>
    </mrow>
    <annotation encoding="application/x-tex">{\displaystyle \sigma ^{2}}</annotation>
  </semantics>
</math></span><img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/53a5c55e536acf250c1d3e0f754be5692b843ef5" class="mwe-math-fallback-image-inline mw-invert skin-invert" aria-hidden="true" style="vertical-align: -0.338ex; width:2.385ex; height:2.676ex;" alt="{\displaystyle \sigma ^{2}}"></span></td></tr></tbody></table>

# Probability theory basics機率基礎
https://www.youtube.com/watch?v=GwSEguqJj6U&list=PLtvno3VRDR_jMAJcNY1n4pnP5kXtPOmVk  
台大電機 Prof. 葉丙成 機率與統計 2013，這個講得超好。

**為什麼我們要研究機率？**  
**因為我們對這世界了解太少，這世界的運作有很多仍是未知的。——prof.benson**

術語：
- Experiment實驗(procedures實驗步驟、model機率模型、observations結果觀察，三個部分任何一個改變，都會變為新的實驗)，
- Outcome結果，
- Sample Space樣本空間，若是S={o1,...,on}n個outcome的集合
- Event事件（實驗結果的敘述，因此是Outcome的集合，或者是Sample Space的子集），
- Event Space事件空間，則為\{\{o1},...,{on},{o1,o2},{o1,o3},...,{on-1,on},{o1,o2,o3},...,{o1,o2,...,on},{}}一共2^n個事件元素的集合
- Probability機率（是個函數，P(Event)，Probability is a function of Event(Set)，Domain定義域就是Event Space，Range值域是[0,1]） 
- Set Theory（因為Probability is a function of Set，所以要了解Set）術語：
    - Element, Set, Subset, Universal Set全集, Empty Set, Intersection交集, Union并集/聯集, Complement補集, Difference差集(X - Y), Disjoint不相交(X, Y disjoint if X∩Y=∅), Mutually Exclusive互斥（兩個set是disjoint，一堆集合兩兩不相交就是互斥）
    - De Morgan's Law: 
    <img src="/assets/1280px-Demorganlaws.svg.png" width="50%" height="50%">

>為什麼事件空間是2^n？一次實驗裡兩個結果，三個結果怎麼可能同時發生？  
剛開始這個疑問就是沒搞清結果和事件的區別，一個事件可能包含多個結果。（37分鐘有例子）

## Axioms /ˈaksɪəm/
從[這部影片](https://www.youtube.com/watch?v=ee-k1VBdzNU&list=PLtvno3VRDR_jMAJcNY1n4pnP5kXtPOmVk&index=2)第一次了解一個理論的公理，中國大陸的教學真差。
近代數學常從數條公理推導出整套理論，線性代數有8(9?)條公理([9 axioms of linear algebra/real vector spaces](https://www.math.ucla.edu/~tao/resource/general/121.1.00s/vector_axioms.html)):
- Additive axioms.  For every x,y,z in X, we have
    - x+y = y+x.
    - (x+y)+z = x+(y+z).
    - 0+x = x+0 = x.
    - (-x) + x = x + (-x) = 0.
- Multiplicative axioms.  For every x in X and real numbers c,d, we have
    - 0x = 0
    - 1x = x
    - (cd)x = c(dx)
- Distributive axioms.  For every x,y in X and real numbers c,d, we have
    - c(x+y) = cx + cy.
    - (c+d)x = cx +dx.
整套理論只基於幾條公理的好處是，對於一個新問題只需要確定滿足這些公理（其實沒有定義“+”要怎麼做，是general的，套別的case其實不一定滿足），就能適用其他所有定理。 
公理不用證明，axioms是理性直覺覺得是對的東西。只從這幾條廢話推導出所有定理確實牛逼。

Axioms of Probability(機率三公理):
- Axiom 1: For any event A, {% math %}P(A) \geq 0{% endmath %}
- Axiom 2: Probability of the sample space S is {% math %}P(S)=1{% endmath %}
- Axiom 3: If A1,A2,A3,⋯ are disjoint events, then {% math %}P(A_1 \cup A_2 \cup A_3 \cdots)=P(A_1)+P(A_2)+P(A_3)+\cdots{% endmath %}

axiom3的disjoint即互斥。

## 性質(定理)
- P(A) = P(A-B) + P(A∩B)  
- P(A∪B) = P(A) + P(B) - P(A∩B)  
- 切麵包定理：若 {% math %}C_1, C_2, \cdots, C_n{% endmath %}互斥，且{% math %}C_1 \cup C_2 \cup \cdots \cup C_n = S{% endmath %}，則对任何事件 A：{% math %}P(A) = P(A \cap C_1) + P(A \cap C_2) + \cdots + (A \cap C_n){% endmath %}
- 若A⊂B則P(A)≤P(B)
- Boole's inequality/Union Bound布爾不等式：對任何事件A1, A2, ..., An，{% math %}\mathbb{P}\left(\bigcup_i A_i\right)\leq \sum_i\mathbb P(A_i){% endmath %}
- Bonferroni's inequality

## conditional probability條件機率(貝氏定理)
P ( X | Y ), Y是觀察到的已發生的事件，X是關心的未發生的事件。

![原本實驗的樣本空間若是S即P(S)=1，新的樣本空間就變成了Y即P(Y|Y)=1，這個豎線｜讀作“given”比如P(X|Y)讀作P of X given Y](/assets/Screenshot 2024-10-31 at 13.53.26.png)

**tex公式裡∪是\\cup，∩是\\cap，一個杯子一個帽子很形象很有趣。**

{%math%}P(X|Y) = \frac{P(X\cap Y)}{P(Y)}{%endmath%}

P ( X | Y )可以理解成只是樣本空間S變成了Y而已。  

**若事件C1, C2 . . . Cn互斥且S = C1 ∪ C2 ∪ . . . . . ∪ Cn，則對任意事件A，**
- Law of Total Probability(切麵包)，{%math%}\begin{array}{l} P(A) =\sum\limits_{i=1}^{n} P(C_i)P(A| C_i)\end{array}{%endmath%}。Ex：阿宅 vs. 可愛店員：店員對阿宅笑否，受店的生意影響很大。已知滿座機率，可愛店員對阿宅笑的機率？
- Bayes' Rule, {% math %} P(C_j|A)=\frac{P(A|C_j)P(C_j)}{\sum\limits_{i=1}^{n} P(A | C_i) P(C_i)}{% endmath %}，之前算的都是P of A given C，貝葉斯是解決計算P of C given A。Ex：一日，老闆見可愛店員笑，請問在此情況下，當日生意滿座之機率為何？  
![proof](/assets/Screenshot 2024-10-31 at 15.00.44.png)

## Independence(獨立性)
若滿足P(A∩B)=P(A)P(B)則A、B兩事件為獨立事件。  
跟互斥對比：A∩B=∅不可能事件即P(A∩B)=0。

可以理解成兩個實驗的樣本空間沒有交集？

Prof. Benson立刻就講到了[更好的定義](https://www.youtube.com/watch?v=GQvEk8Rsyd4&list=PLtvno3VRDR_jMAJcNY1n4pnP5kXtPOmVk&index=3&t=222s)，若滿足P(A|B) = P(A)則A、B兩事件為獨立事件。

根據上面的理解“P ( X | Y )可以理解成只是樣本空間S變成了Y而已”，即Y的樣本空間跟X完全沒有關係，比如X的樣本空間是{o1, o2, ..., on}，Y的樣本空間是{p1, p2, ..., pn}，事件Y可能是{p1, p2, p3}，完全不影響這個世界裡事件X發生與否，這裡的Y實際上是{p1, p2, p3, o1, o2, ..., on}。

非獨立事件的conditional probability是這樣的：假如實驗是投一個6面骰子一次，樣本空間是{1,2,3,4,5,6}，X事件是扔出{1,5,6}，Y事件是扔出大數{4,5,6}，那X｜Y的樣本空間就變成了{4,5,6}即X只可能是扔出了大數中的某個數，o1∩Y=∅，X就變成{5,6}，P(X｜Y)則=P({5,6})/P({4,5,6})=2/3。

## Graph Scheme
[實驗分解。](https://www.youtube.com/watch?v=GQvEk8Rsyd4&list=PLtvno3VRDR_jMAJcNY1n4pnP5kXtPOmVk&index=3&t=1307s)

## counting method
為什麼機率需要算排列組合，需要counting？  
因為**古典機率常假設每個outcome發生機率相同，**所以計算某個事件的機率，等同於計算這個事件包含多少個outcome，像[上面](#probability-theory-basics機率基礎)計算事件空間那樣，機率（事件）=outcome數/事件空間元素數。所以機率問題等於counting問題。

counting前的判斷：
- distinguishable? 可區分？
- w/wo replacement? 有放回？
- order matters or not? 關心順序嗎？**if order matters then Permutation (排列問題) else Combination (組合問題)**

### Permutation(order matters)
- w/o replacement
![若有n異物，從中依序取出K物，共有多少種結果？](/assets/Screenshot 2024-10-31 at 16.28.23.png)
- w/ replacement
![若有n異物，從中選取一物，選完後放回。依序選取k次，共有多少種結果？](/assets/Screenshot 2024-10-31 at 16.31.09.png)

### Combination(order doesn't matter)

除以k!就是因為order doesn't matter，要把order的排列除掉，也就是k個items的所有排列方式k!種（比如3個items有6種排列方式=3!）。

數學裡叫n choose k，n取k。

{%math%}C(n, k) = \binom{n}{k} = C_n^k = \frac{n!}{k!(n-k)!}{%endmath%}

![二項式定理裡的係數就是這個所以C(n, k)也叫binomial coefficient](/assets/Screenshot 2024-10-31 at 18.38.19.png)

### Multinomial

![跟二項式係數類似](/assets/Screenshot 2024-10-31 at 18.47.16.png)

## Random Variable隨機變數
就是把outcome數字化的方式，讓推導更數學、更簡明。

![本質是一個mapping，是個函數，定義域是樣本空間值域是實數。](/assets/Screenshot 2024-10-31 at 19.21.49.png)

- Discrete R.V. (離散隨機變數)
- Continuous R.V. (連續隨機變數)
![隨機變數](/assets/Screenshot 2024-10-31 at 20.55.38.png)

**隨機變數的函數**也是隨機變數，因為outcome的函數的函數也是outcome的函數。

## CDF (Cumulative Distribution Function)
累計分佈函數{%math%}F_X(x) = P(X \le x){%endmath%}。

![最有用的用途：計算X落在某範圍內的機率](/assets/Screenshot 2024-10-31 at 21.40.43.png)

![](/assets/Screenshot 2024-10-31 at 21.53.48.png)

![discrete r.v.函數曲線是階梯式的，所以X的區間有沒有等於包不包含邊界區別很大](/assets/Screenshot 2024-10-31 at 22.21.28.png)

![continuous r.v. P(x)=0](/assets/Screenshot 2024-10-31 at 22.42.03.png)

![性質](/assets/Screenshot 2024-10-31 at 22.48.48.png)

## PMF (Probability Mass Function)
![一旦知道discrete r.v.的PMF，就完全掌握](/assets/Screenshot 2024-10-31 at 22.57.17.png)

![對一個discrete random variable來說PMF和CDF可以互相推得](/assets/Screenshot 2024-10-31 at 23.16.30.png)

![](/assets/Screenshot 2024-10-31 at 23.58.51.png)

兩個函數一個是X=x(PMF)，一個是X<=x(CDF)就是這個區別。  
分布是把很多相似實驗總結成規律。
## Discrete Probability Distributions

### Bernoulli Distribution
![](/assets/Screenshot 2024-11-01 at 18.50.27.png)

只care成功失敗，一次實驗，非1即0。

![](/assets/Screenshot 2024-11-01 at 21.15.44.png)

![](/assets/Screenshot 2024-11-01 at 21.19.18.png)

### Binomial Distribution
二項分布。

![](/assets/Screenshot 2024-11-01 at 21.22.22.png)

![](/assets/Screenshot 2024-11-01 at 21.27.03.png)

![](/assets/Screenshot 2024-11-01 at 21.28.59.png)

![](/assets/Screenshot 2024-11-01 at 21.31.08.png)

n=1時退化成白努力分布。

### Uniform Distribution
均勻分布。

![](/assets/Screenshot 2024-11-01 at 21.32.42.png)

![](/assets/Screenshot 2024-11-01 at 22.45.12.png)

![](/assets/Screenshot 2024-11-01 at 22.47.04.png)

### Geometric Distribution
几何分布。

{%math%}P_X(x){%endmath%}等比級數，即幾何級數

{%math%}S_n=\frac{a_1\left(1-r^n\right)}{1-r}, r \neq 1{%endmath%}

![](/assets/Screenshot 2024-11-01 at 22.54.08.png)

![](/assets/Screenshot 2024-11-01 at 22.59.08.png)

![](/assets/Screenshot 2024-11-01 at 23.17.12.png)

![](/assets/Screenshot 2024-11-01 at 23.21.49.png)

### Pascal Distribution

k=1就退化成Geometric分布。

![](/assets/Screenshot 2024-11-01 at 23.25.45.png)

![](/assets/Screenshot 2024-11-01 at 23.34.44.png)

![](/assets/Screenshot 2024-11-01 at 23.44.20.png)

![](/assets/Screenshot 2024-11-01 at 23.48.35.png)

### Poisson Distribution
![](/assets/Screenshot 2024-11-01 at 23.51.42.png)

![](/assets/Screenshot 2024-11-02 at 00.12.09.png)

![](/assets/Screenshot 2024-11-02 at 00.18.37.png)

![](/assets/Screenshot 2024-11-02 at 00.19.01.png)

## Probability Density Function
PDF就是CDF的微分！

積分constant不用擔心，可以通過-無窮=0等邊界條件唯一確定。

![](/assets/Screenshot 2024-11-02 at 14.42.37.png)

![why mass和density，這張圖一目了然，continuous不能有PMF，就是顧名思義“質量”和“密度”的關係](/assets/Screenshot 2024-11-02 at 15.12.29.png)

![](/assets/Screenshot 2024-11-02 at 15.18.20.png)

![](/assets/Screenshot 2024-11-02 at 15.23.02.png)

![](/assets/Screenshot 2024-11-02 at 15.26.34.png)

![](/assets/Screenshot 2024-11-02 at 15.28.21.png)

![](/assets/Screenshot 2024-11-02 at 15.28.56.png)

![](/assets/Screenshot 2024-11-02 at 15.29.17.png)

![](/assets/Screenshot 2024-11-02 at 15.31.32.png) ![](/assets/Screenshot 2024-11-02 at 15.33.07.png)

### Uniform Distribution
![](/assets/Screenshot 2024-11-02 at 15.41.03.png)

![](/assets/Screenshot 2024-11-02 at 15.43.14.png)

### Exponential Distribution
![](/assets/Screenshot 2024-11-02 at 15.48.27.png)

![](/assets/Screenshot 2024-11-02 at 15.50.39.png)

### Gamma / Erlang Distribution
![](/assets/Screenshot 2024-11-02 at 15.58.38.png)

![](/assets/Screenshot 2024-11-02 at 15.59.04.png)

![](/assets/Screenshot 2024-11-02 at 15.59.35.png)

## Normal Distribution
終於來到elo的重點。

![](/assets/Screenshot 2024-11-02 at 16.01.02.png)

![](/assets/Screenshot 2024-11-02 at 16.02.15.png)

![](/assets/Screenshot 2024-11-02 at 16.03.52.png)

![](/assets/Screenshot 2024-11-02 at 16.05.08.png)

比如gaussian，為什麼單獨對standard normal建表？因為：。。。

https://en.wikipedia.org/wiki/Normal_distribution

<svg xmlns:xlink="http://www.w3.org/1999/xlink" xmlns="http://www.w3.org/2000/svg" width="24.077ex" height="7.176ex" style="vertical-align: -2.838ex;" viewBox="0 -1867.7 10366.4 3089.6" role="img" focusable="false" aria-labelledby="MathJax-SVG-1-Title">
<title id="MathJax-SVG-1-Title">{\displaystyle f(x)={\frac {1}{\sqrt {2\pi \sigma ^{2}}}}e^{-{\frac {(x-\mu )^{2}}{2\sigma ^{2}}}}\,.}</title>
<defs aria-hidden="true">
<path stroke-width="1" id="E1-MJMATHI-66" d="M118 -162Q120 -162 124 -164T135 -167T147 -168Q160 -168 171 -155T187 -126Q197 -99 221 27T267 267T289 382V385H242Q195 385 192 387Q188 390 188 397L195 425Q197 430 203 430T250 431Q298 431 298 432Q298 434 307 482T319 540Q356 705 465 705Q502 703 526 683T550 630Q550 594 529 578T487 561Q443 561 443 603Q443 622 454 636T478 657L487 662Q471 668 457 668Q445 668 434 658T419 630Q412 601 403 552T387 469T380 433Q380 431 435 431Q480 431 487 430T498 424Q499 420 496 407T491 391Q489 386 482 386T428 385H372L349 263Q301 15 282 -47Q255 -132 212 -173Q175 -205 139 -205Q107 -205 81 -186T55 -132Q55 -95 76 -78T118 -61Q162 -61 162 -103Q162 -122 151 -136T127 -157L118 -162Z"/>
<path stroke-width="1" id="E1-MJMAIN-28" d="M94 250Q94 319 104 381T127 488T164 576T202 643T244 695T277 729T302 750H315H319Q333 750 333 741Q333 738 316 720T275 667T226 581T184 443T167 250T184 58T225 -81T274 -167T316 -220T333 -241Q333 -250 318 -250H315H302L274 -226Q180 -141 137 -14T94 250Z"/>
<path stroke-width="1" id="E1-MJMATHI-78" d="M52 289Q59 331 106 386T222 442Q257 442 286 424T329 379Q371 442 430 442Q467 442 494 420T522 361Q522 332 508 314T481 292T458 288Q439 288 427 299T415 328Q415 374 465 391Q454 404 425 404Q412 404 406 402Q368 386 350 336Q290 115 290 78Q290 50 306 38T341 26Q378 26 414 59T463 140Q466 150 469 151T485 153H489Q504 153 504 145Q504 144 502 134Q486 77 440 33T333 -11Q263 -11 227 52Q186 -10 133 -10H127Q78 -10 57 16T35 71Q35 103 54 123T99 143Q142 143 142 101Q142 81 130 66T107 46T94 41L91 40Q91 39 97 36T113 29T132 26Q168 26 194 71Q203 87 217 139T245 247T261 313Q266 340 266 352Q266 380 251 392T217 404Q177 404 142 372T93 290Q91 281 88 280T72 278H58Q52 284 52 289Z"/>
<path stroke-width="1" id="E1-MJMAIN-29" d="M60 749L64 750Q69 750 74 750H86L114 726Q208 641 251 514T294 250Q294 182 284 119T261 12T224 -76T186 -143T145 -194T113 -227T90 -246Q87 -249 86 -250H74Q66 -250 63 -250T58 -247T55 -238Q56 -237 66 -225Q221 -64 221 250T66 725Q56 737 55 738Q55 746 60 749Z"/>
<path stroke-width="1" id="E1-MJMAIN-3D" d="M56 347Q56 360 70 367H707Q722 359 722 347Q722 336 708 328L390 327H72Q56 332 56 347ZM56 153Q56 168 72 173H708Q722 163 722 153Q722 140 707 133H70Q56 140 56 153Z"/>
<path stroke-width="1" id="E1-MJMAIN-31" d="M213 578L200 573Q186 568 160 563T102 556H83V602H102Q149 604 189 617T245 641T273 663Q275 666 285 666Q294 666 302 660V361L303 61Q310 54 315 52T339 48T401 46H427V0H416Q395 3 257 3Q121 3 100 0H88V46H114Q136 46 152 46T177 47T193 50T201 52T207 57T213 61V578Z"/>
<path stroke-width="1" id="E1-MJMAIN-32" d="M109 429Q82 429 66 447T50 491Q50 562 103 614T235 666Q326 666 387 610T449 465Q449 422 429 383T381 315T301 241Q265 210 201 149L142 93L218 92Q375 92 385 97Q392 99 409 186V189H449V186Q448 183 436 95T421 3V0H50V19V31Q50 38 56 46T86 81Q115 113 136 137Q145 147 170 174T204 211T233 244T261 278T284 308T305 340T320 369T333 401T340 431T343 464Q343 527 309 573T212 619Q179 619 154 602T119 569T109 550Q109 549 114 549Q132 549 151 535T170 489Q170 464 154 447T109 429Z"/>
<path stroke-width="1" id="E1-MJMATHI-3C0" d="M132 -11Q98 -11 98 22V33L111 61Q186 219 220 334L228 358H196Q158 358 142 355T103 336Q92 329 81 318T62 297T53 285Q51 284 38 284Q19 284 19 294Q19 300 38 329T93 391T164 429Q171 431 389 431Q549 431 553 430Q573 423 573 402Q573 371 541 360Q535 358 472 358H408L405 341Q393 269 393 222Q393 170 402 129T421 65T431 37Q431 20 417 5T381 -10Q370 -10 363 -7T347 17T331 77Q330 86 330 121Q330 170 339 226T357 318T367 358H269L268 354Q268 351 249 275T206 114T175 17Q164 -11 132 -11Z"/>
<path stroke-width="1" id="E1-MJMATHI-3C3" d="M184 -11Q116 -11 74 34T31 147Q31 247 104 333T274 430Q275 431 414 431H552Q553 430 555 429T559 427T562 425T565 422T567 420T569 416T570 412T571 407T572 401Q572 357 507 357Q500 357 490 357T476 358H416L421 348Q439 310 439 263Q439 153 359 71T184 -11ZM361 278Q361 358 276 358Q152 358 115 184Q114 180 114 178Q106 141 106 117Q106 67 131 47T188 26Q242 26 287 73Q316 103 334 153T356 233T361 278Z"/>
<path stroke-width="1" id="E1-MJMAIN-221A" d="M95 178Q89 178 81 186T72 200T103 230T169 280T207 309Q209 311 212 311H213Q219 311 227 294T281 177Q300 134 312 108L397 -77Q398 -77 501 136T707 565T814 786Q820 800 834 800Q841 800 846 794T853 782V776L620 293L385 -193Q381 -200 366 -200Q357 -200 354 -197Q352 -195 256 15L160 225L144 214Q129 202 113 190T95 178Z"/>
<path stroke-width="1" id="E1-MJMATHI-65" d="M39 168Q39 225 58 272T107 350T174 402T244 433T307 442H310Q355 442 388 420T421 355Q421 265 310 237Q261 224 176 223Q139 223 138 221Q138 219 132 186T125 128Q125 81 146 54T209 26T302 45T394 111Q403 121 406 121Q410 121 419 112T429 98T420 82T390 55T344 24T281 -1T205 -11Q126 -11 83 42T39 168ZM373 353Q367 405 305 405Q272 405 244 391T199 357T170 316T154 280T149 261Q149 260 169 260Q282 260 327 284T373 353Z"/>
<path stroke-width="1" id="E1-MJMAIN-2212" d="M84 237T84 250T98 270H679Q694 262 694 250T679 230H98Q84 237 84 250Z"/>
<path stroke-width="1" id="E1-MJMATHI-3BC" d="M58 -216Q44 -216 34 -208T23 -186Q23 -176 96 116T173 414Q186 442 219 442Q231 441 239 435T249 423T251 413Q251 401 220 279T187 142Q185 131 185 107V99Q185 26 252 26Q261 26 270 27T287 31T302 38T315 45T327 55T338 65T348 77T356 88T365 100L372 110L408 253Q444 395 448 404Q461 431 491 431Q504 431 512 424T523 412T525 402L449 84Q448 79 448 68Q448 43 455 35T476 26Q485 27 496 35Q517 55 537 131Q543 151 547 152Q549 153 557 153H561Q580 153 580 144Q580 138 575 117T555 63T523 13Q510 0 491 -8Q483 -10 467 -10Q446 -10 429 -4T402 11T385 29T376 44T374 51L368 45Q362 39 350 30T324 12T288 -4T246 -11Q199 -11 153 12L129 -85Q108 -167 104 -180T92 -202Q76 -216 58 -216Z"/>
<path stroke-width="1" id="E1-MJMAIN-2E" d="M78 60Q78 84 95 102T138 120Q162 120 180 104T199 61Q199 36 182 18T139 0T96 17T78 60Z"/>
</defs>
<g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)" aria-hidden="true">
 <use xlink:href="#E1-MJMATHI-66" x="0" y="0"/>
 <use xlink:href="#E1-MJMAIN-28" x="550" y="0"/>
 <use xlink:href="#E1-MJMATHI-78" x="940" y="0"/>
 <use xlink:href="#E1-MJMAIN-29" x="1512" y="0"/>
 <use xlink:href="#E1-MJMAIN-3D" x="2179" y="0"/>
<g transform="translate(3236,0)">
<g transform="translate(120,0)">
<rect stroke="none" width="3054" height="60" x="0" y="220"/>
 <use xlink:href="#E1-MJMAIN-31" x="1276" y="676"/>
<g transform="translate(60,-961)">
 <use xlink:href="#E1-MJMAIN-221A" x="0" y="80"/>
<rect stroke="none" width="2100" height="60" x="833" y="821"/>
<g transform="translate(833,0)">
 <use xlink:href="#E1-MJMAIN-32" x="0" y="0"/>
 <use xlink:href="#E1-MJMATHI-3C0" x="500" y="0"/>
<g transform="translate(1074,0)">
 <use xlink:href="#E1-MJMATHI-3C3" x="0" y="0"/>
 <use transform="scale(0.707)" xlink:href="#E1-MJMAIN-32" x="810" y="408"/>
</g>
</g>
</g>
</g>
</g>
<g transform="translate(6530,0)">
 <use xlink:href="#E1-MJMATHI-65" x="0" y="0"/>
<g transform="translate(466,681)">
 <use transform="scale(0.707)" xlink:href="#E1-MJMAIN-2212" x="0" y="0"/>
<g transform="translate(550,0)">
<g transform="translate(120,0)">
<rect stroke="none" width="2033" height="60" x="0" y="146"/>
<g transform="translate(60,515)">
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-28" x="0" y="0"/>
 <use transform="scale(0.574)" xlink:href="#E1-MJMATHI-78" x="389" y="0"/>
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-2212" x="962" y="0"/>
 <use transform="scale(0.574)" xlink:href="#E1-MJMATHI-3BC" x="1740" y="0"/>
<g transform="translate(1345,0)">
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-29" x="0" y="0"/>
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-32" x="389" y="364"/>
</g>
</g>
<g transform="translate(536,-567)">
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-32" x="0" y="0"/>
<g transform="translate(287,0)">
 <use transform="scale(0.574)" xlink:href="#E1-MJMATHI-3C3" x="0" y="0"/>
 <use transform="scale(0.574)" xlink:href="#E1-MJMAIN-32" x="572" y="288"/>
</g>
</g>
</g>
</g>
</g>
</g>
 <use xlink:href="#E1-MJMAIN-2E" x="10087" y="0"/>
</g>
</svg>

## Central Limit Theorem(中央極限定理)

![convolution](/assets/Screenshot 2024-11-03 at 13.46.25.png)


![uniform分布的獨立事件convolution完變成了gaussian](/assets/Screenshot 2024-11-03 at 15.39.14.png)

![exponential分布的獨立事件convolution完變成了gaussian](/assets/Screenshot 2024-11-03 at 15.40.21.png)

![laplacian分布也是一樣，可以知道continuous r.v.都是一樣](/assets/Screenshot 2024-11-03 at 15.43.13.png)

![多個discrete隨機變數之和也是](/assets/Screenshot 2024-11-03 at 15.44.05.png)

![不只uniform，geometric也是一樣](/assets/Screenshot 2024-11-03 at 15.44.49.png)


![](/assets/Screenshot 2024-11-03 at 15.52.56.png)

### 應用

![牛逼](/assets/Screenshot 2024-11-03 at 15.55.30.png)

![牛逼](/assets/Screenshot 2024-11-03 at 16.16.35.png)

為什麼mean是probability，variance是probability(1- probability)，因為Bernoulli的X非1即0，所以expectation是1\*probability + 0\*(1- probability)，{%math%}Var(X)=E(X^2)-E(X)^2 = probability - probability^2{%endmath%}。

## 失憶性

![條件機率的概率分佈計算方式](/assets/IMG_0608.jpg)

![0.8^(x-1)*0.2還是geometric distribution](/assets/Screenshot 2024-11-04 at 00.25.03.png)

![機率很重要的common sense](/assets/Screenshot 2024-11-04 at 00.26.13.png)

# dota mmr
https://dota2.fandom.com/wiki/Matchmaking  
https://dota2.fandom.com/wiki/Matchmaking_Rating

Valve has stated that matchmaking tries to fulfil several criteria:
- The teams are balanced. (Each team has a 50% chance to win. It's based on Elo rating.)
- The discrepancy in skill between the most and least skilled player in the match is minimized.
- The highest skill Radiant player should be close to the same skill as the highest skill Dire player.
- The discrepancy between experience (measured by the number of games played) between the least experienced player and the most experienced player is minimized.
- Each team contains about the same number of parties.
- Five-player parties can only be matched against other five-player parties.
- Players' language preferences contains a common language.
- Wait times shouldn't be too long.

## elo hell
Elo hell (also known as MMR hell) is a video gaming term used in MOBAs and other multiplayer online games with competitive modes. It refers to portions of the matchmaking ranking spectrum where individual matches are of poor quality, and are often determined by factors **such as poor team coordination** which are perceived to be **outside the individual player's control.** This ostensibly makes it difficult for skilled players to "climb" up the matchmaking ranking (and out of Elo hell), due to the difficulty of consistently winning games under these conditions. Its existence in various games has been debated, and **some game developers have called it an illusion caused by cognitive bias.**

在北街咖啡斷網的瞬間記起小時候爸帶回家一台筆記本電腦，那時上網還通通都是有線和sim卡，而那台筆記本是插無線網卡上網。在老家屬院那間客廳的衣櫥上用插著一根錄音筆一樣的無線網卡的筆記本電腦玩賽爾號（打普尼？），那真是堪比幾年後我用小手機看網路小說到天亮，爸第二天在我確定他沒有翻我手機的情況下能精準說出我瀏覽了哪些網頁一樣的震撼體驗。這一幕幕歷歷在目。