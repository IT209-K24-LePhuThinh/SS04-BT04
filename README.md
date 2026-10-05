# BT04 - Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Commit nhầm file credentials.txt

```powershell
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git init
Initialized empty Git repository in D:/Work/Rikkei/devops/BT/SS04/SS04-BT04/.git/
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git config --local user.name "lethinh"
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git config --local user.email "lephuthinh387@gmail.com"
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git add README.md credentials.txt
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git commit -m "up"
[main (root-commit) 7d3c1b5] up
 2 files changed, 6 insertions(+)
 create mode 100644 README.md
 create mode 100644 credentials.txt
```

## 2. Tạo tệp .gitignore

```text
# Thông tin bí mật
credentials.txt

# File rác của hệ điều hành
Thumbs.db
Desktop.ini
```

## 3. Gỡ file khỏi cache theo dõi của Git

Dùng `git rm --cached` để Git ngừng theo dõi file nhưng file vẫn còn nguyên trên đĩa cứng.

```powershell
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git rm --cached credentials.txt
rm 'credentials.txt'

PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    credentials.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
```

## 4. Sửa lại commit gần nhất bằng --amend

```powershell
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git add .gitignore
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git commit --amend -m "docs: thêm README.md và cấu hình .gitignore"
[main 3e5a8c1] docs: thêm README.md và cấu hình .gitignore
 Date: Mon Oct 5 20:41:03 2026 +0700
 2 files changed, 5 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
```

## 5. Kiểm tra trạng thái file

```powershell
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git status
On branch main
nothing to commit, working tree clean

PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> Test-Path credentials.txt
True
```

`credentials.txt` không còn nằm trong danh sách theo dõi của Git (không ở dạng Staged hay Modified) nhưng vẫn tồn tại trên đĩa cứng.

## 6. Kiểm tra lịch sử commit gần nhất

```powershell
PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git log -n 1
commit 3e5a8c1a1f4d2e7b9c0d3a5f8e2b6c4d1a7f9e03
Author: lethinh <lephuthinh387@gmail.com>
Date:   Mon Oct 5 20:41:03 2026 +0700

    docs: thêm README.md và cấu hình .gitignore

PS D:\Work\Rikkei\devops\BT\SS04\SS04-BT04> git ls-files
.gitignore
README.md
```
