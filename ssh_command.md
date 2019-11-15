# Command ssh
## 1. ssh đến máy remote thông qua máy trung gian chỉ 1 câu lệnh  
- Tham số -t để có thể thực hiện nhiều câu lệnh ssh với nhau:
```
ssh -p 10022 -t thanhtn@157.7.146.124 ssh root@10.121.31.84
```
## 2. Thực hiện ssh và command trên máy remote chỉ bằng 1 câu lệnh.
```
ssh -p 10022 -t thanhtn@157.7.146.124 ssh -l root 10.121.31.84 ""ls""
```

```
ssh -l hdfs 10.121.31.84 "hive -e 'show databases'"
```
```
ssh -p 10022 -t thanhtn@157.7.146.124 ssh -l hdfs 10.121.31.84 "'hive -f test.sql'"
```
- Để hive ẩn đi Warn và infor thì thêm --silent=true
```
ssh -t -p 10022 thanhtn@157.7.146.124 ssh -l hdfs 10.121.31.84 "'hive --showHeader=false --outputformat=tsv2 --silent=true -f test.sql'
```
```
ssh -t -p 10022 thanhtn@157.7.146.124 ssh -l hdfs 10.121.31.84 "'hive --showHeader=false --outputformat=tsv2 --silent=true -f test.sql'" | sed '/NULL/d' | sed '/SLF4J/d'
```
```
ssh -t -p 10022 thanhtn@157.7.146.124 ssh -l hdfs 10.121.31.84 "'hive --showHeader=false --outputformat=tsv2 --silent=true -f test.sql'" | sed '/NULL/d' | sed '/SLF4J/d' | sed '1d'|sed '1d'|sed -n '/#/q;p'
```