1. \` \`和$()的作用是一样的，都是命令的替换；\`expr\`进行计算的时候，相当于是一条命令，要将命令的结果幅值给变量就必须使用\` \`或者$()将表达式括起来
2. Shell中变量的说明
  > $$: Shell本身的PID（ProcessID<br>
  $!: Shell最后运行的后台Process的PID<br> 
  $?: 最后运行的命令的结束代码（返回值）<br> 
  $-: 使用Set命令设定的Flag一览<br> 
  $*: 所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。<br> 
  $@: 所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。 <br>
  $#: 添加到Shell的参数个数 <br>
  $0: Shell本身的文件名 <br>
  $1～$n: 添加到Shell的各参数值。$1是第1参数、$2是第2参数…。