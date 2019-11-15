### Tạo symbolic cho hdp, xử lý vấn đề bộ nhớ trong hadoop cluster

- Copy /usr/hdp -> /var/hdp
  - cp -r /usr/hdp /var/hdp
  - check lại xem đã ok chưa (xem size,xm folder ...)
- Đổi tên /usr/hdp -> /usr/hdp2
  - mv /usr/hdp /usr/hdp2
- tạo /usr/hdp là simbolic của /var/hdp
  - ln -s /var/hdp /usr/hdp    