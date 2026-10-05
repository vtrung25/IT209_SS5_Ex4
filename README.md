# Bài 4 — Gitflow Hotfix

## Luồng nhánh

`main` giữ phiên bản production `v1.0.0`; `develop` chứa công việc đang triển khai. Khi cần vá lỗi lộ dữ liệu, tạo `hotfix/v1.0.1` từ `main`, sửa lỗi, merge vào `main`, gắn tag `v1.0.1`, rồi merge ngược hotfix vào `develop`.

```text
main:     o-------------------M (tag v1.0.1)
           \                 /
hotfix:     H---------------/
             \             \
develop:     D---------------N
```

## Các lệnh chính

```bash
git switch main
git switch -c hotfix/v1.0.1
# sửa lỗi bảo mật và commit
git switch main
git merge --no-ff hotfix/v1.0.1
git tag -a v1.0.1 -m "Release Hotfix 1.0.1"
git switch develop
git merge --no-ff hotfix/v1.0.1
git branch -d hotfix/v1.0.1
```

## Kiểm tra

```bash
git branch -a
git tag
git log --graph --oneline --decorate --all
```

Tag `v1.0.1` trỏ vào merge commit trên `main`. Nhánh `develop` nhận cùng commit sửa lỗi qua merge thứ hai để tránh lỗi quay lại trong bản phát hành tiếp theo.
