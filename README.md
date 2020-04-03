# mine-shell


# 常用命令

## k8s
```
kubectl get pods  -o=go-template='{{range $m := .items}}{{$m.metadata.name}}{{"\t"}}{{range $n := $m.status.containerStatuses}}{{$n.image}}{{end}}{{"\t"}}{{$m.status.podIP}}{{"\t"}}{{"\t"}}{{$m.status.hostIP}}{{"\n"}}{{end}}' --context=dev | grep bbxc
```

## java
通过javabean生成所有set方法
```
grep -v '@' bean.data | grep -v '*'  | sed -e 's/^\s\+//g' -e '/^$/d'   | sed -e 's/\(\S\+\)\s\+\(\S\+\)\s\+\(\S\+\);/\3/' -e 's/^\([a-z]\)/result\.set\u\1/g' -e 's/$/(null);/g'
```

通过数据库生成所有set方法
```
sed -e 's/_\([a-z]\)/\u\1/g' -e 's/^\([a-z]\)/orderPay\.set\u\1/g' -e 's/$/(null);/g' column.data
```
