Đối với những lập trình viên thì linux từ lâu đã là 1 người bạn. Mặc dù sự ra đời của Window và MacOs cùng với 1 số tính năng ưu việt hơn nhưng các hệ điều hành nhân linux như Ubuntu, CentOs vẫn được nhiều lập trình viên chọn sử dụng vì 1 số lý do sau:
+ Miễn phí 
+ Tính bảo mật cao
+ Hộ trợ môi trường tốt cho việc lập trình
+ Tránh chơi game ...

Hiện nay hầu hết các hệ thống server trên toàn thế giới cũng chọn các hệ thống linux làm hệ điều hành. Vì vậy người quản trị hệ thống phải thành thạo kĩ năng về  linux và bài toán phân quyền trong linux là vấn đề cần phải nắm vững. Việc hệ thống của bạn bảo mật đến mức độ nào phần nhiều phụ thuộc sự phân quyền hợp lý, chính xác của bạn. Mình đã thấy nhiều bạn vì không hiểu rõ kiến thức phân quyền đã vội vàng sử dụng command 'chmod 777 file_name', điều này thật sự nguy hiểm vì tất cả mọi tài khoản đều có full quyền sử dụng đối với file/folder đó kể cả quyền xóa :D. Mình hi vọng bài viết này sẽ giúp bạn hiểu rõ hơn về bài toán phân quyền file/folder trong hệ thống linux.
## 1. Phân quyền trong linux là gì ?
Với 1 file/folder trong linux sẽ có 3 quyền cơ bản:
+ R (read) - với file thì có thể xem được nó, với thư mục thì có thể show được các thành phần ở trong đó.
+ W (write) - với file thì có thể chỉnh sửa nội dung file, với thư mục thì có thể thêm bớt, xóa file ở trong đó.
+ X (execute) - có quyền thực thi với file, quyền truy cập với thư mục tức là thư mục muốn sử dụng lệnh cd thì phải có quyền này mới sử dụng được.


Với 1 file/folder trong linux sẽ có 3 đối tượng sử dụng: 
+ O (owner): là chủ sở hữu của file thư mục, khi mới tạo file mặc định là là account tạo file.
+ G (group): là 1 hoặc 1 nhóm account, khi mới tạo file mặc định là là account tạo file. 
+ U (user other) : là những account còn lại không thuộc 2 nhóm trên 
 
Để hiểu rõ hơn ta xét ví dụ sau: 
```
$ ls -al
drwxr-xr-x 2 nhatthanh123bk nhatthanh123bk 4096 Thg 1 22 17:19 .
drwxrwxr-x 4 nhatthanh123bk nhatthanh123bk 4096 Thg 1 22 17:10 ..
-rw-r--r-- 1 nhatthanh123bk nhatthanh123bk   34 Thg 1 21 17:16 text1.txt
-|rw-|r--|r--| 1 nhatthanh123bk nhatthanh123bk   43 Thg 1 21 17:39 text2.txt
   ^   ^   ^           ^              ^
   |   |   |           |              |  
   |_ _|_ _| _ _ _ _ _ |_ __ _ _ _ _ _| _ _ _ _ _ _ _ _ quyển của owner
       |_ _| _ _ _ _ _ |_ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ quyền của group
           |_ _ _ _ _ _| _ _ _ _ _ _ _| _ _ _ _ _ _ _ _  quyền của user other
                       |_ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ tên owner
                                      |_ _ _ _ _ _ _ _ _ tên group
```  
Từ ví dụ trên ta thấy được với file text2.txt:
+ owner của file này là nhatthanh123bk, owner có quyền: rw- tức là đọc và ghi.
+ group của file cũng là nhatthanh123bk, các account trong group này có quyền: r-- tức là đọc.
+ user other của file có quyền: r-- tức quyền đọc.

Trong hệ thống linux có 1 account sở hữu mọi quyền thực thi đối với file/folder đó user root.
Trong nhiều trường hợp ta phải tiến hành setting lại quyền của owner,group,user other với file/folder,để làm điều đó ta sẽ đến với mục tiếp theo.
## 2. Thiết lập quyền sử dụng file/folder như thế nào?
Trong hệ thống linux:
+ Quyền read file/folder "được cho": 4 điểm.
+ Quyền ghi file/folder "được cho" : 2 điểm.
+ Quyền thực thi hay truy cập file/folder "được cho": 1 điểm. 

Vì vậy giả sử  muốn setting phân quyền cho 1 file như sau:
+ owner gồm quyền : r+w+x
+ group gồm quyền : r+x
+ user other gồm quyền : r+x

Ta thấy:
+ owner có : 7 điểm.
+ group có : 5 điểm.
+ user other : 5 điểm.

Chính vì thế ta sẽ thực hiện lệnh sau để setting phân quyền cho file:
```
chmod 755 file_name
```

Ngoài cách trên ta còn có thể làm như sau:
+ command thêm quyền execute cho group:
    ```
    chmod g+x file_name
    ```
+ command xóa quyền write cho group:
    ```
    chmod g-x file_name
    ```
+ command thêm quyền write cho user other: 
    ```
    chmod a+x file_name
    ```
+ command thêm quyền execute cho group và user other:
    ```
    chmod ga+x file_name
    ```
Với o-owner, g - group, a - user other, r-read ,w-write, x-execute, add thêm quyền là '+', loại bỏ đi quyền là '-'.

Có nhiều cách để setting quyền cho 1 file/folder phải không nào, sau đây mình sẽ hướng dẫn cho các bạn cách để thay đổi owner và group của file/folder đó.



## 3. Thay đổi owner và group cho tập tin và thư mục.
### Thay đổi owner cho tập tin và thư mục.
Khi file/folder vừa mới tạo ra thì owner được mặc định là account tạo ra file/folder đó, ta hoàn toàn có thể đổi tên owner này bằng câu lệnh sau:
```
chown user file_name 
```
Ví dụ bạn muốn set lại owner cho text1.txt với owner mới là user1:
```
chown user1 text1.txt
```
### Thay đổi group cho tập tin và thư mục.
Trước hết ta cần phải biết được trong hệ thống của chúng ta có những group và account nào? cách tạo chúng ra sao? Những câu lệnh dưới đây sẽ giúp chúng ta điều đó:
- Command liệt kê ra danh sách các group có sẵn: 
    ```
    getent group | awk -F : '{print $1}'
    ```
- Command show tất cả các account có trong group:
    ```
    members group_name
    ```
- Command tạo 1 group mới:
    ```
    sudo groupadd group_name
    ```
- Command thêm 1 account vào group:
    ```
    usermod -a -G group_name user_name
    ```

Bây giờ muốn đổi từ group này qua group khác ta thực hiện câu lệnh sau:
```
chgrp name_file/name_folder name_group
```
## 4.Kết luận
Chỉ với những câu lệnh ở trên bạn hoàn toàn đã có thể giải quyết được bài toán phân quyền cho file/folder trong hệ thống linux rồi đó :D, thật đơn giản đúng không nào. Hi vọng bài viết sẽ giúp ích nhiều cho những bạn mới làm quen sử dụng các hệ thống linux. Mọi ý kiến đóng góp của bạn đọc xin được gửi về địa chỉ email sau: thanhtn@vietnamlab.vn. Xin cảm ơn các bạn đã đọc bài viết của mình,hẹn gặp lại :D
