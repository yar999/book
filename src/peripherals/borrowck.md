## 全局可变状态

不幸的是，硬件基本上只不过是可变的全局状态，这可能会让Rust开发人员来感到非常棘手。但是硬件本来就独立于我们编写的结构体代码，并且在现实世界中就是随时可以进行修改。

## 我们的规则应该是什么？

我们如何与这些外围设备可靠地交互？

1. 始终使用`volatile`方法读取或写入外围存储器，因为它随时可能发生变化
2. 在软件中，应该允许同时存在对这些外设的任意数量的只读访问
3. 如果某些软件需要对外设的读写访问权限，则它应该拥有该外设的唯一引用

## 借用检查器

这些规则中的最后两个听起来和借用检查器的工作机制非常类似！

想像一下我们是否可以转移这些外设的所有权，或者提供对这些外设的不变或可变的引用？

好吧，我们可以.我们需要每个外围设备都只有一个实例，以便Rust借用检查器可以正确处理。 幸运的是，在硬件中，任何给定的外设都只有一个实例，但是如何设计访问接口呢？