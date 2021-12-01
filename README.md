# Personal-Notes



### How to send files through scp?

```shell
scp -P 2100 jupyter/data-repo-sigmod22-et/ERT/az.txt wangke@101.6.96.180:~/
```



### how to send files through rsync?

```shell
rsync -r ../CLionProjects/nvmkv/ wangke@101.6.96.180:~/nvmkv/
rsync -azr -e "ssh -p 2100" ../CLionProjects/nvmkv/ wangke@101.6.96.180:~/nvmkv/ # need to specify a port
```

