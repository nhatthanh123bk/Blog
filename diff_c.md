# diff command

### 1. so sánh 2 file theo từng dòng
```
diff --recursive text1.txt text2.txt 
```
```
diff --recursive forlder2 folder1
```
```
diff -y file1 file2
```
### 2. so sánh 2 folder
- So sánh 2 folder và chỉ liệt kê ra những file có nội dung khác nhau, những file tên giống nhau nhưng nội dung khác nhau, những file chỉ có ở folder này nhưng không có tại folder kia.
```
diff --brief --recursive dir1/ dir2/

```