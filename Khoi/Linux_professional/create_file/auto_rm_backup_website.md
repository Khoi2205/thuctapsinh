```
#!/bin/bash

read -p "Enter website domain: " website_domain
read -p "Enter database name: " db_name
read -p "Enter database username: " db_username
read -s -p "Enter database password: " db_password
echo
read -p "Nhập số ngày sao lưu tối đa(in days): " max_backup_age

# Xóa các bản sao lưu website cũ hơn thời gian lưu trữ tối đa
find "$backup_dir" -type d -name "$website_domain" -mtime +$max_backup_age -exec rm -rf {} \;
echo "Các bản sao lưu cũ của $website_domain đã bị xóa."


```