### eval  
```
eval "return redis.call('set',KEYS[1],ARGV[1],ARGV[2],ARGV[3],ARGV[4])" 1 a aaaa EX 60 NX
```
