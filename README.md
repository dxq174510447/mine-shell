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

通过excel文件头生成ddl
```
cat head.data | sed -s 's/\s\+/\n/g' | sed -s 's/^[^\-]\+\-\([a-z]\+\)$/\1 varchar(200),/g'
```

通过word生成javabean
```
1.      TESTNO  检测报告编码    非空
2.      JYLSH   检验流水号      非空，唯一索引


cat head.data | sed -e 's/^\(\S\+\)\s\+\(\S\+\)\s\+\(.\+\)$/@ApiModelProperty(value = "\3")\nprivate String \L\2;/g'

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

## jq
https://github.com/stedolan/jq/wiki/Cookbook

```shell
cat bean.json | jq ".result.records[]|.name,.id"

cat bean.json | jq -r '.result.records[]| "\(.name),\(.id)"'
```


## ab
```shell

ab -H 'Content-Type: application/json'  -H 'ctl-bbxc-terminal: 3' -H 'ctl-appid: wxb69b26693b196da7' -H 'ctl-user-id: 20191223150227qtqxxsrbdiepwk2sevxnvx' -H 'ctl-login-type: customer' -H 'ctl-open-id: oKvzl5aaEZEeohjxtncEoCq4-Wuo'  -T 'application/json' -t 300 -p sec.txt -n 100 -c 100 http://localhost:8433/api/bbxc/order/outer/wx/order/pay

```

## go

### 通过查询结果生成struct 


### 通过查询结果生成struct的赋值语句


### 通过查询结构生存带orm标签的struct


