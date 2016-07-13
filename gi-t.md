列显已有的标签

```
$ git tag

```

如果你只对 1.4.2 系列的版本感兴趣,可以运行下面的命令

```
$ git tag -l 'v1.4.2.*' v1.4.2.1
v1.4.2.2
v1.4.2.3
v1.4.2.4

```

新建标签

```
$ git tag -a v1.4 -m 'my version 1.4'

```

而 -m 选项则指定了对应的标签说明,Git 会将此说明一同保存在标签对象中。如果在此 选项后没有给出具体的说明内容,Git 会启动文本编辑软件供你输入。

可以使用 git show 命令查看相应标签的版本信息,并连同显示打标签时的提交对象。

```
$ git show v1.4
tag v1.4
Tagger: Scott Chacon <schacon@gee-mail.com>
Date: Mon Feb 9 14:45:11 2009 -0800

my version 1.4
commit 15027957951b64cf874c3557a0f3547bd83b3ff6
Merge: 4a447f7... a6b4c97...
Author: Scott Chacon <schacon@gee-mail.com>
Date: Sun Feb 8 19:02:46 2009 -0800

    Merge branch 'experiment'

```

分享标签

```
$ git push origin v1.5
Counting objects: 50, done.
Compressing objects: 100% (38/38), done. Writing objects: 100% (44/44), 4.56 KiB, done. Total 44 (delta 18), reused 8 (delta 1)
To git@github.com:schacon/simplegit.git
* [new tag] v1.5 -> v1.5
```

