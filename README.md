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
```git clone <url>```</br>
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
```$ git branch 
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
# một số vần đề về commit 
### sửa lại nội dung commit 
```git commit --amend```
### đổi tên user hoặc email khi commit --> của HEAD 
```git commit --amend -m "nội dung commit message" --author="user.name <user.email>"```
### Xóa 1 file ra khỏi commit 
```git rm --cached <tên file>```

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

### Với trường hợp đã public commit 
+ giống như reset nhưng revert thay đổi cả mes commit
```git revert <id_commit>```
### Gộp một vài commit thành 1 commit duy nhất
```git rebase -i <commit_end>```
