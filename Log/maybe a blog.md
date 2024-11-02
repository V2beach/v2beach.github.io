1. brew install lua
https://stackoverflow.com/questions/61899041/macos-permission-denied-apply2files-usr-local-lib-node-modules-expo-cli-n  
lua -v  
Lua 5.4.7  Copyright (C) 1994-2024 Lua.org, PUC-Rio  
2. /dump select(4, GetBuildInfo())
30403  
Beginning Lua with World of Warcraft Addons也是玩的巫妖王，版本是30100，有趣。  
3. write the toc
`## Interface: 30403`
`## Dependencies: xxx`
`## SavedVariables: xxx`
`xxx.lua`
`localization files...`
4. write the lua
core function
5. xml?

lua寫魔獸插件的思路從代碼裡扒出來？

[vscode配置nodejs](https://code.visualstudio.com/docs/nodejs/nodejs-tutorial)

[Node.js 有三大類的模組](https://ithelp.ithome.com.tw/articles/10184564)

Core Modules (原生模組)
- 可以被編譯成二進制位元存取，也可以單刀直入做一些本地自動化功能操作。有幾個重要的(以下連結，可以進入，知道其使用方法)：
- [http](https://nodejs.org/api/http.html)：它包含可以用來建立http server 的一些類別, 方法, 及事件。
- [url](https://nodejs.org/api/url.html)：它包含可以解析url的一些方法。
- [querystring](https://nodejs.org/api/querystring.html)：它包含可以處理由client端傳來querystring的一些方法。
- [path](https://nodejs.org/api/path.html)：它包含可以處理一些檔案或資料夾路徑的方法。
- [fs](https://nodejs.org/api/fs.html)：它包含檔案的存取／操作的一些類別，方法及事件。
- [util](https://nodejs.org/api/util.html)：它包含一些可供程序者使用的效能函式。
[Local Modules (自建模組)](https://ithelp.ithome.com.tw/articles/10185008)
- 自建模組，也可以包裝成npm，供Node.js 社群使用。
- 在Node.js裡，一個javascript檔案，就是一個模組！所以，在建立模組時，應該根據其功能，寫成一個Javascript的檔案。
- 最後需要[module.exports = var](https://ithelp.ithome.com.tw/articles/10185083)，就是宣告物件(台灣國語的對象object)是一個module，可以讓任何程式使用require()方法調用這個模組，使用裡面的物件，方法及變數…。
Third Party Modules (第三方模組)

JavaScript 除了 Node.js，还有其他运行环境，比如：

1. 浏览器：JavaScript 在浏览器中运行，常用于前端开发。
2. Deno：一个现代的 JavaScript 和 TypeScript 运行时，提供了更强的安全性和模块支持。
3. Electron：用于构建跨平台桌面应用的框架，结合了 Node.js 和浏览器环境。
4. React Native：用于开发移动应用的框架，使用 JavaScript 和 React。

不同编程语言有各自的运行环境，以下是一些常见语言及其运行环境：

C
- 编译器：C 代码通常通过编译器（如 GCC、Clang、MSVC）编译成机器代码，然后在操作系统上运行。
- 嵌入式环境：C 也广泛用于嵌入式系统，通常与特定硬件和工具链一起使用。
Java
- Java 虚拟机 (JVM)：Java 代码首先编译成字节码，然后在 JVM 中运行。JVM 使 Java 程序具有跨平台性。
- 应用服务器：如 Apache Tomcat、GlassFish 等，支持运行 Java Web 应用。
Python
- Python 解释器：Python 代码通过解释器（如 CPython、PyPy）直接执行。
- 虚拟环境：通常使用虚拟环境（如 venv、virtualenv）来管理项目的依赖和环境。
每种语言的运行环境设计都与其特性和使用场景密切相关。

JavaScript 的模块（module）可以类比于其他语言中的以下概念：

C：
- 头文件 (Header Files)：C 中的头文件通常用于定义函数和结构体，可以看作是模块的一种形式，用于组织和共享代码。
- 源文件 (Source Files)：通过源文件，可以将相关的函数和数据结构封装在一起，类似于模块的功能。
Java：
- 包 (Package)：Java 中的包用于组织类，类似于模块用于组织相关的功能和代码。
- 类 (Class)：模块可以包含多个类和函数，这些类和函数可以相互协作，类似于模块中的功能。
Python：
- 模块 (Module)：在 Python 中，模块本身是一个文件，可以包含函数、类和变量，直接对应于 JavaScript 的模块概念。
- 包 (Package)：Python 的包是多个模块的集合，类似于 JavaScript 中的命名空间或整体模块。
总的来说，JavaScript 的模块概念与其他语言的组织和封装机制相似，主要用于促进代码的复用和结构化。