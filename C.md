1. 主函数main可以接收外部参数。利用main函数的形参——int argc, char* argv[]
  - argc 代表传递的参数
  - argv是一个指针数组，每一个元素指向命令行的一个字符串(以空格结尾)，argv[0]指的是运行的函数本身，后面才是传递给运行函数的参数
2. C语言移位操作中
  - 移动的位数一定不能超过自己本身的大小，否则相当于无移位
  - 有符号数进行移位的时候，会对符号位进行扩展
  - 无符号数移位的时候只会补0，所以大部分情况下，别对未知的有符号数进行移位操作
3. 对C语言自增、自减操作的理解
  左值就是结果能够标识一个准确位置的值。
  ```C
  int a = 0;
  ++a; // 这个表达式，先使得a+1，然后返回一份值为1的拷贝，这份拷贝没有具体的位置，因此无法作为左值
  a++; // 这个表达式，先返回一份值为0的a的拷贝，然后再使得a+1，因此也无法作为左值。
  // 注意对于指针变量也是同样的理解
  ```
