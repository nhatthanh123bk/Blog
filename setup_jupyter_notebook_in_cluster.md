## Hướng dẫn cài đặt jupyter notebook để code pyspark trên cluster.

### 1. Các bước cài đặt.
    - Cài đặt jupyter notebook trên máy remote 
    - Cài đặt jupyter notebook trên máy server.
    - Forward port để chạy jupyter notebook từ máy server về máy remote của mình -> done!!!  
    - Setup Pyspark sử dụng jupyter notebook 
### 2. Chi tiết cài đặt.
    1. Đầu tiên cài đặt jupyter notebook trên máy remote.
        + sudo apt-get update
        + sudo apt-get install jupyter-notebook
    2. cài đặt jupyter notebook trên máy server.
        + Cài đặt virtualenv và tạo 1 virtualenv:
            pip install virtualenv
            virtualenv -p python2.7 env
        
        + Vào virtualenv, cài đặt jupyter.
            source env/bin/activate
            pip install jupyter

        + Config jupyter.
            Sử dụng lệnh sau để tạo file config nếu chưa có hoặc tìm được dẫn file nếu đã có rồi.
                jupyter notebook --generate-config
            Tìm đến dòng 
                ## The IP address the notebook server will listen on.
                c.NotebookApp.ip = 'localhost'
                để sửa localhost thành hosts của máy server vd: 'vnlab-master3.com' 
        
        + Config để có thể code pyspark cluster với jupyter notebook.
            Thêm 2 dòng sau vào ~/.bashrc
                export PYSPARK_DRIVER_PYTHON=jupyter
                export PYSPARK_DRIVER_PYTHON_OPTS='notebook'  

        + Chạy jupyter notebook trên server:
            jupyter notebook
            Chú ý đến port và dãy ký tự phía sau token sẽ là mật khẩu để đăng nhập ở bước sau.
        
        + Forward port về máy remote.
            vd:
            ssh -p 10022 thanhtn@157.7.146.124 -L 8888:10.121.31.84:8888
        + Truy cập trên máy remote.
            localhost:8888 password đăng nhập chính là token ở trên

    Done !!!       




