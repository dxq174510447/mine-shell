# mine-shell


# 常用命令

## k8s
```
kubectl get pods  -o=go-template='{{range $m := .items}}{{$m.metadata.name}}{{"\t"}}{{range $n := $m.status.containerStatuses}}{{$n.image}}{{end}}{{"\t"}}{{$m.status.podIP}}{{"\t"}}{{"\t"}}{{$m.status.hostIP}}{{"\n"}}{{end}}' --context=dev | grep bbxc
```

## java
通过javabean生成所有set方法
```
grep -v '@' bean.data | grep -v '*' | grep -v '//'  | sed -e 's/^\s\+//g' -e '/^$/d' -e 's/\s*=.\+/;/'   | sed -e 's/\(\S\+\)\s\+\(\S\+\)\s\+\(\S\+\);/\3/' -e 's/^\([a-z]\)/info\.set\u\1/g' -e 's/$/(null);/g'
```

通过数据库生成所有set方法
```
sed -e 's/_\([a-z]\)/\u\1/g' -e 's/^\([a-z]\)/orderPay\.set\u\1/g' -e 's/$/(null);/g' column.data
```

#### 通过进程查找消耗资源的线程
```shell
ps -mp 55052 -o %cpu,%mem,time,tid  
echo 'ibase=10;obase=16;55053'  | bc   ## D70D->d70d  
jstack 55052 > 22.txt ##从文件里面查找d70d

## 反向查找 从22.txt 查找对应线程的nid 16禁制
echo "ibase=16;D831"| bc   ## 转换10进制 55345
ps -mp 55052 -o %cpu,%mem,time,tid  ##在去里面查找
```
