1. 对当前目录初始化

```
￼$ git init

```

2.如果当前目录下有几个文件想要纳入版本控制,需要先用 git add 命令告诉 Git 开始对 这些文件进行跟踪,然后提交

```
$ git add *.c
$ git add README
$ git commit -m 'initial project version'

```

3.从现有仓库克隆

```
$ git clone git://github.com/schacon/grit.git

```

如果希望在克隆 的时候,自己定义要新建的项目目录名称,可以在上面的命令最后指定

```
￼$ git clone git://github.com/schacon/grit.git mygrit
```

