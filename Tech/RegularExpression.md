| 式子 | 法子 | 例子 |
| -- | -- | -- |
| (pattern) | 匹配 pattern 并获取这一匹配。所获取的匹配可以从产生的 Matches 集合得到，在VBScript 中使用 SubMatches 集合，在JScript 中则使用 $0…$9 属性。要匹配圆括号字符，使用 '\(' 或 '\)'。 | 用IMG\_\(....\)匹配IMG\_0123, IMG\_3210，用`<img src="/pics/NAS/IMG_$1.JPG">`替换扩展匹配到的文件名，并且保留原本的文件名。 |

正則可視化，fun tools.


| [lookaround](https://www.regular-expressions.info/lookaround.html) | lookahead |  解釋 | lookbehind | 解釋 |
| -- | -- | -- | -- | -- |
| negative | q(?!u) | 匹配後面沒有u的q(matches a “q” not followed by a “u”) | (?<!a)b | 匹配前面沒有a的b(matches a “b” that is not preceded by an “a”) |
| positive | q(?=u) | 匹配後面有u的q | (?<=a)b | 匹配前面有a的b |