摘自[[翻译\] 控制台（Console），终端（Terminal）和Shell之间的区别究竟是什么？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/405527391)好文



不止了解shell

1.Terminal(终端)

终端只负责接受键盘输入并显示文字输出，**并不对你的输入做任何处理，它只负责接收输入和显示输出，负责处理你输入信息的另有其人。**

比如我打开cmd (CommandPrompt,命令提示符)，输入 “111”，终端就会显示111

![1678458702359](shell.assets/1678458702359.png)

2.console(控制台)

控制台指的是计算机的操控台或者一个内置屏幕和键盘的机柜，但它本质上仍是一个终端。从（计算机）技术上讲，控制台是硬件设备，而终端则是其内部运行的软件程序。**而在软件世界中提到控制台和终端时，它们实际上是同义词。（例如IDE和编辑器中的内置终端，也叫控制台）**

3.shell(外壳，与之相对的是kenel，操作系统内核)

之前提到的终端，会接受用户的输入并将其发送给另一个程序，这个应用程序就是Shell。Shell 会接收你通过终端/控制台输入的命令并将其"翻译"成操作系统内核可以理解的语言，然后调用相应的应用程序，最后生成输出并将其传递回终端以显示给用户。

现在我们打开cmd，就会打开终端，然后终端会调用shell程序。

shell是解释器而非编译器，而且shell有很多类型：

bash是Unix shell的一种，目前是linux和mac OS的默认shell



脚本文件：

shell不仅能执行用户直接输入的命令,还能从文件中读取命令，这样的文件称为脚本。