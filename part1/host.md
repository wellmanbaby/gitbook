# JS的宿主对象和原生对象的区别
## 原生对象
ECMA-262 把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象”。与宿主无关，在javascript（远景浏览器）、nodejs（node平台）、jscript（ie浏览器）、typescript（微软平台）等等中均有这些对象。

“本地对象”包含哪些内容：Object、Function、Array、String、Boolean、Number、Date、RegExp、 Error、EvalError、RangeError、ReferenceError、SyntaxError、TypeError、 URIError。

由此可以看出，简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。在运行过程中动态创建的对象，需要new
## 内置对象
ECMA-262 把内置对象（built-in object）定义为“由 ECMAScript 实现提供的、独立于宿主环境的所有对象，在 ECMAScript 程序开始执行时出现”。这意味着开发者不必明确实例化内置对象，它已被实例化了。

同样是“独立于宿主环境”。根据定义我们似乎很难分清“内置对象”与“本地对象”的区别。而 ECMA-262 只定义了两个内置对象，即 Global 和 Math （它们也是本地对象，根据定义，每个内置对象都是本地对象）。如此就可以理解了。内置对象是本地对象的一种。
## 宿主对象
何为“宿主对象”？主要在这个“宿主”的概念上，ECMAScript中的“宿主”当然就是我们网页的运行环境，即“操作系统”和“浏览器”。

所有非本地对象都是宿主对象（host object），即由 ECMAScript 实现的宿主环境提供的对象。所有的BOM和DOM都是宿主对象。因为其对于不同的“宿主”环境所展示的内容不同。其实说白了就是，ECMAScript官方未定义的对象都属于宿主对象，因为其未定义的对象大多数是自己通过ECMAScript程序创建的对象。
## 它们之间的关系
本地对象与内置对象：原生包含内置，内置是原生的一个子集。

宿主对象：内置对象的Global和宿主提供的一个全局对象，

本地对象为array obj regexp等可以new实例化

内置对象为 Global Math 等不可以实例化的

宿主为宿主注入到全局的对象，如浏览器的window 等

宿主为浏览器自带的document,window 等
## 为什么扩展JS内置对象不是好的做法
因为你不知道哪一天浏览器或javascript本身就会实现这个方法，而且和你扩展的实现有不一致的表现。到时候你的javascript代码可能已经在无数个页面中执行了数年，而浏览器的实现导致所有使用扩展原型的代码都崩溃了。。。
## 有哪些内置对象和内置函数
太特么多了