# c_hook
c/c++函数运行时修改.Text段代码，可以实现在线热更，目前主要还是屏蔽某些函数执行，修改代码段直接RETURN或者用简单的新函数替换，修复一些紧急的BUG（老的业务函数内可能逻辑执行比较复杂，所以一般是直接RETURN而不是重写代码，这么做是有损的，会导致某些逻辑运行不正常，得结合场景使用）
#### 1:拿到函数地址后，简单的可以直接修改.Text段，直接return
#### 2:拿到函数地址后，也可以用新的.SO的函数替换执行文件中的函数，新的函数可以有一定的发挥空间，但很有限
#### 3:例如收到协议的地方直接屏蔽掉协议的处理
###问题
#### 1:修改.Text段的代码长度有限制，只能修改自己的，不能越界把别的函数的代码影响了
#### 2:多线程目前不好解决，其他现场可以正在运行要替换的函数，指令可能执行了一般，直接修改会导致其他线程执行错误，只能在逻辑层确保其他线程都不运行原函数后，在修改原函数
