| | | |
| -- | -- | -- |
| (pattern) | 匹配 pattern 并获取这一匹配。所获取的匹配可以从产生的 Matches 集合得到，在VBScript 中使用 SubMatches 集合，在JScript 中则使用 $0…$9 属性。要匹配圆括号字符，使用 '\(' 或 '\)'。 | 例子：用IMG_\(....\)匹配IMG_0123, IMG_3210，用\<img src=\"\/pics\/NAS/IMG_$1.JPG\"\>替换扩展匹配到的文件名，并且保留原本的文件名。 |