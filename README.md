#                                         Một Số Thao Tác Với Git

# Một Số Lệnh Cơ Bản
![mô hình](https://github.com/trantronghienit/workingGit/blob/master/git_status_sequence.png)
### tạo file ghi chú 
``` echo "# ShellADB" >> README.md ``` 
### Khởi Tạo Git Local
``` git init ```
### Xóa git ra khỏi dự án
```rm -rf .git```
### Đem file cho git theo dõi
```
// thêm tất cả các file vào cho git quản lý
git add .
// thêm 1 file vào cho git quản lý
git add tenfile
```
### Commit sau khi đã thay đổi
```git commit -m "first commit"```
### kiểm tra log đã commit trên hệ thống dưới local và cả trên server
```git log```
### kiểm tra log đã commit trên hệ thống dưới local và cả trên server
```git log```
### CLONE (kéo dự án từ server)
```git clone <remote_repo>```</br>
```git clone <remote_repo> <ten_folder_local>```
```git clone -b <branch> <remote_repo>```
### PULL (cập nhật lại nội dung từ server đối với dự án đã kéo về) 
```git pull```

# Làm Việc với git từ xa 
### Liệt kê hết tất cả các máy chủ từ xa của dự án
```$ git remote -v
origin  https://github.com/trantronghienit/workingGit (fetch)
origin  https://github.com/trantronghienit/workingGit (push)
```
### Thêm Các Kho Chứa Từ Xa
+ Lưu ý là kho test đã đc tạo trên git và thao tác này chỉ giúp ta thêm server điều khiển dưới local thôi </br>
```cú pháp: git remote add [shortname] [url]```</br>
```git remote add hien https://github.com/trantronghienit/test.git``` </br>
or </br>
```git remote add origin https://github.com/trantronghienit/test.git``` </br>
### Đẩy Lên Máy Chủ Trung Tâm
```git push origin master```</br>
or </br>
+ với trường hợp bạn chưa đăng nhập tài khoản của mình vào hệ thống git khi đẩy lên bạn cần đăng nhập </br>
```git push -u origin master```</br>

### Xóa Và Đổi Tên Từ Xa
```cú pháp đổi tên: git remote rename <currentname> <newname>```

```cú pháp đổi tên: git remote rm <tencanxoa>```

# Branch(Nhánh Trong git)
nhánh thì cũ giống như repository cũng có 2 loại là branch local và branch remote </br>
### Tạo Nhánh
```git branch namebranch```
### Kiểm tra nhánh
```$ git branch -a
  issue1
* master     // có dấu sao là đang ở nhánh hiện tại
```

### chuyển nhánh
```git checkout <tên branch cần chuyển>```
### xóa nhánh
```git branch -d <tên branch cần xóa>```
### Xoá một branch remote lưu ở local
```git branch -d -r <remote_name>/<branch_name>```
### Xoá một branch ở phía remote
git push <remote_name> --delete <branch_name> </br>
vd: </br>
```git push origin --delete <branch_name>```</br>
+ Chú ý:
Phải checkout ra branch cùng tên với branch trên remote thì mới xóa được. Tức là khi ta đang ở branch develop thì ta không thể xóa branch master trên remote.
### Push một branch ở local lên server (giống như push data)
+ 2 branch cùng tên
```git push <remote_name> <branch_name>```</br>
vd: push branch test lên branch test trên remote </br>
```git push origin test```
+ 2 branch khác tên
```git push <remote_name> <local_branch>:<remote_branch>```</br>
VD: push branch master lên remote với tên là develop</br>
```git push origin master:develop```</br>

------------------------------------------
# git reset
### Chỉ đưa HEAD về như cũ
+ nghĩa là khi ta lỡ commit nhưng giờ muốn bỏ commit đó đi</br>
```git reset --soft HEAD~<index>``` or ```git reset --soft HEAD~<id_commit>``` </br>
+ index : chỉ mục commit ví dụ có 3 commit và giờ ta muốn quay về chỉ mục thứ nhất ```git reset --soft HEAD~1``` </br>

### Đưa HEAD và index về như cũ
+ nghĩa là cũng giống như trên nhưng nó gỡ bỏ sự theo dõi trong index</br>
```git reset HEAD~<index>``` or ```git reset HEAD~<id_commit>``` </br>

### Đưa cả index, working tree về 1 commit trước đó 
+ khi sử dụng câu lệnh này có thể ảnh hưởng đến nội dung file thay đổi trước đó và xóa cả file trc đó
```git reset --hard HEAD~<index>``` or ```git reset --hard HEAD~<id_commit>``` </br>

***===> mặc định 3 loại trên nếu không có index và id_commit thì nó sẽ quay về commit gần nhất***</br>
***===> lưu ý 3 câu lệnh trên có thể xem log của chúng đc bằng lệnh***</br>
```git reflog```</br>
===> vì tính chất của 3 loại lệnh trên chỉ là di chuyển về 

### git reset single file ?
+ đối với file chưa được add và chưa commit và muốn file đó quay về lúc commit hiện thời 
```git checkout -- [path file]     vd: git checkout -- lever\1/index.txt```

+ còn lỡ chúng ta muốn reset 1 file nào đó nhưng file đó đã đc add và commit rồi thì sao giải pháp
```
checkout đến working commit muốn trở về và đường dẫn đến file đó 
git checkout <commit hash> -- <path file> 
vd: git checkout c5f567 -- file1/to/restore file2/to/restore
// sau khi đánh lênh trên thì mặc nhiên nội dung file sẽ quay lại mốc commit chúng ta đã checkout nhưng vấn đề là khi chuyển nhánh qua nhánh hiện tại thì nó lại quay về như cũ
```

# một số vần đề về commit 
### sửa lại nội dung commit 
```git commit --amend```
### đổi tên user hoặc email khi commit --> của HEAD 
```git commit --amend -m "nội dung commit message" --author="user.name <user.email>"```
### Xóa 1 file ra khỏi commit 
```git rm --cached <tên file>```
### Với trường hợp đã public commit 
+ giống như reset nhưng revert thay đổi cả mes commit
```git revert <id_commit>```
### Gộp một vài commit thành 1 commit duy nhất
```git rebase -i <commit_end>```

# Git fetch
### Công dụng: Lấy source mới nhất trên server về đè lên source hiện tại trên máy local
```git fetch <Tên nhánh>```</br>
# Git pull
### Công dụng: Lấy source mới nhất trên server về và tiến hành trộn
```git pull <Tên nhánh>```</br>

# Git Tag
### Công dụng: Gắn nhãn (tagging) Người ta khuyên nên tạo nhãn (tags) khi phát hành phần mềm. Đây là khái niệm được biết đến, đã từng có trên SVN. Bạn tạo tag mới tên là 1.0.0 bằng cách
```git tag 1.0.0 1b2e1d63ff```</br>

+ Chuỗi 1b2e1d63ff là 10 ký tự đầu tiên của mã commit (commit id) mà bạn muốn tham chiếu đến bằng nhãn của bạn. Bạn có thể lấy mã commit với lệnh

# Kiểm Tra và Thay Đổi Thông Tin Git:
### Kiểm Tra Thông Tin
```
git config --list ---> liệt kê tất cả các thông tin
git config user.email  ----> hiện thông tin email hiện hành
git config user.name
```

### Thay Đổi Thông Tin
```
git config --global user.email [your email address here]
git config --global user.name [your name address here]
```
# Vấn Đề Merge Và Rebase
## So Sánh Giữa Merge và rebase
```
|===============|==============================================================================|
|               |                         F---G---H  develop                                   |
|  Ban đầu      |                        /                                                     |
|               |               A---B---C---D---E   master                                     |
|===============|==============================================================================|
|               |                 Rebase                  |             Merge                  |
|===============|=========================================|====================================|
| Branch        |                 develop                 |             master                 |
|     hiện tại  |                                         |                                    |
|---------------|-----------------------------------------|------------------------------------|
|    Câu lệnh   |           git rebase master             |       git merge develop            |
|               |       hoặc                              |                                    |
|               |           git rebase master develop     |                                    |
|---------------|-----------------------------------------|------------------------------------|
|               |                   F'---G'---H'  develop |           F---G---H  develop       |
| Sơ đồ kết quả |                  /                      |          /         \               |
|               | A---B---C---D---E   master              | A---B---C---D---E---I   master     |
|---------------|-----------------------------------------|------------------------------------|
|   Nguyên lý   | - Lưu các commit F, G, H (các commit của| - Tạo một commit mới (I) áp dụng   |
|               |   develop tính tới cha chung gần nhất)  |   tất cả các thay đổi của các      |
|               | - Reset develop về commit C             |   commit trên develop tính đến     |
|               | - Áp dụng các commit của master đến     |   cha chung gần nhất.              |
|               |   cha chung gần nhất C                  |   Cụ thể ở đây là tất cả các       |
|               | - Tạo các commit mới F', G', H' theo    |   commit F, G, H                   |
|               |   sự thay đổi của các commit F, G, H    |                                    |
|---------------|-----------------------------------------|------------------------------------|
|    Đặc điểm   | - Các commit của rebase-branch sẽ là    | - Lịch sử commit không bị thay đổi |
|               |   các commit mới nhất                   |                                    |
|               | - Lịch sử commit sẽ bị thay đổi         |                                    |
|               |                                         |                                    |
|               |                                         |                                    |
|===============|=========================================|====================================|
```
