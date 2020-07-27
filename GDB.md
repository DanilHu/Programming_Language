1. 条件断点，使用`break number if expression`
2. 删除断点，使用`delete number`
3. 回退到上一行，使用`reverse-step`
4. 查看值的变化，使用`watch` & `record `
5. 查看汇编，使用`disassemble /m main # /m表示跟源码一起看，/r表示看到16进制`
6. 跳转到某一行执行，使用`j n`
7. 查看寄存器的值，使用`i registers`查看所有整数寄存器的值，`i all-registers`查看包括浮点寄存器的值，`i registers $register`查看一个寄存器的值。(i是info的缩写)
