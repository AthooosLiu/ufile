# 常见问题

## 内存消耗情况如何？

目前us3vmds测试保存超过100W文件索引时，内存在1.7g左右，其中包含了不少目录序列化的物化视图，理论实际值相对更少。平均每个索引的大小为1.7k左右，这个值确实相对比较高，这也是后续优化点之一。

## us3vmds启动后，发现通过hadoop命令看到的目录下文件与us3控制台上看到不一致，该怎么办？

有两个方法，第一种是直接暴力重启us3vmds，第二种是通过us3vmds的sync命令来进行强制同步。