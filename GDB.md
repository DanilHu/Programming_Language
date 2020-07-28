1. 条件断点，使用`break number if expression`
2. 删除断点，使用`delete number`
3. 回退到上一行，使用`reverse-step`
4. 查看值的变化，使用`watch` & `record `
5. 查看汇编，使用`disassemble /m main # /m表示跟源码一起看，/r表示看到16进制`
6. 跳转到某一行执行，使用`j n`
7. 查看寄存器的值，使用`i registers`查看所有整数寄存器的值，`i all-registers`查看包括浮点寄存器的值，`i registers register`查看一个寄存器的值。(i是info的缩写)；出来的内容则是前面是16进制表示，后面是10进制，除了%rsp两个都是16进制
8. 查看指定地址Memory的值，使用`x/nfu address`
  > n代表从该地址开始往后多少个unit，`默认是1`<br>
  f代表format，与printf里面的一致，‘x’, ‘d’, ‘u’, ‘o’, ‘t’, ‘a’, ‘c’, ‘f’, ‘s’。`默认是x`<br>
  u代表每个unit是多少个字节的，b->Bytes, h->Halfwords (two bytes), w->Words (four bytes), g->Giant words (eight bytes)。默认是`4bytes`<br>
  若使用默认的nfu，则不需要"/"
9. 设置断点后，使用`c`直接到达下一个断点。`clear+linenum`可以清除某一行上的断点。
