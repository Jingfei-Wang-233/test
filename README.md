- 这里记述一下本小倒霉蛋的经历
问题：
在github上简单创建了个公开的repo，想要将本地的内容push到这个repo上
却发现要输入github用户名和密码，而坑爹的是：这个密码它输不进去啊！！！！！

- 分析一下问题
过程是这个亚子的：
谷歌一下，大部分反馈都是要配置ssh，而在这个问题发生之前我已经超勇地配置了ssh
- assumption-1: ssh没完全配好？有哪一步没有做？
虽然已经配置了ssh keys， 用ssh -T git@github.com，显示成功了，但其实忘记把把私钥添加了
解决：
    用 ssh-add -l查看是否添加了私钥
    如果没有：ssh-add ~/.ssh/id_rsa 
        即
    ssh-add <directory to private SSH key>

结果：
    显示私钥已经添加了，但再次运行 git push -u origin main,结果依然要输入账号和密码
- 继续谷歌：发现了这个相关文档：https://gist.github.com/ddeveloperr/1859fd395e7cb5832c59
解决： 
    对照文档，将repo的URL改成了文档中对应的：git+ssh://git@github.com/我的用户名/repo名.git
    即 git remote set-url origin git+ssh://git@github.com/username/reponame.git
结果：
    push成功了！查看github的repo里有本地目录里的几个文件了！
    感动！

-再更新一下：
    试着clone了一下自己的priviate repo ,如果只是复制url，依然要输入账号密码，于是把url改成了ssh，又可以了
reference：
1. https://gist.github.com/ddeveloperr/1859fd395e7cb5832c59
2. https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent
3. https://www.jianshu.com/p/d29ef6aefee2
4. https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey

