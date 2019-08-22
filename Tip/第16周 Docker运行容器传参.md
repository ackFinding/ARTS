### Docker运行容器传参
运行容器指令
```shell
docker run <image-name> <command> arg1 arg2
```
使用shell 格式的 ENTRYPOINT传参
shell 格式的 ENTRYPOINT 是由 "/bin/sh -c" 启动的，而它是可以解析变量的。另一方面 CMD 或 docker run <image> 的输入第一个元素存成了 $0，其他剩余元素存为 $@, 所以 shell 格式的 ENTRYPOINT 可以这么写
```shell
## shell 中 $0 表示命令本身，$@ 为所有参数
ENTRYPOINT echo hello $0 $@
```
如果不写```$0```，第一个参数将被丢失，```docker run <image>``` 后第一个输入通常是一个命令，所以是 ```$0```, 而 ENTRYPOINT 又希望它是一个普通参数，因此```$0 $@ ```要同时写上。

关于Dockerfile，可参考：[Dockerfile 参考 - Docker中文文档 - PracticeMP 的博客](https://www.practicemp.com/2018/10/docker-dockerfile-reference.html#)
