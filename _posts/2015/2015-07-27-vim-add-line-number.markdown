---
layout: post
title: 用VIM给文件添加行号
tags: Vim
blog: true
---

面试时被问及，果断不会，枉我还自称中级VIM用户。答案却很简单：

    %s/^/\=line('.')/

用每行的行号去替换行首的空字符串，即可获得结果。解决问题的关键在于使用`\=`可以获得之后函数的结果进行替换。

上面的命令会在每行添加对应行号数字，但是行号一般还包含至少一个空格，改进如下：

    %s/^/\=line('.').' '/

添加前：

    def foo():
        print 'hello world'

    if __name__ == '__main__':
        foo()

添加后：

    1 def foo():
    2     print 'hello world'
    3 
    4 if __name__ == '__main__':
    5     foo()


-----------------------

Ref:

<http://vim.wikia.com/wiki/Insert_line_numbers>
