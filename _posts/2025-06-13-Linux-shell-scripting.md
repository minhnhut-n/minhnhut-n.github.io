---
layout: post
title: "Linux Shell Scripting"
date: 2025-06-13 16:26:00 +0700
categories: [Linux]
tags: [Linux, script, bash, shel scripting]
---
**\_\_\_**

Nguyễn Minh Nhựt

# GIỚI THIỆU

Shellscript là cách để một hệ thống đơn giản hóa trình tự thực hiện,
dùng trong các problem về tự động hóa trong lập trình và hệ thống máy
tính. Người dùng (end-user) có thể không tương tác nhiều với các file
.sh (trong linux), .bash(windows),\... nhưng các dev thường sử dụng
trong các hệ thống nhúng hoặc đơn giản chỉ là tool để tự động làm chuổi
công việc nào đó trên máy tính/ hệ thống nhúng.

Được dùng khi không tiện sử dụng các ngôn ngữ code khác để giải quyết
vấn đề và suy cho cùng nó chỉ là một ngôn ngữ. Khác với các language
khác phải dùng thư viện để truy cập các system call, Shell không cần
biên dịch vì là ngôn ngữ thông dịch (interpreted language).

Complied language -\> src code -\> compiler -\> machine code -\> tệp
chương trình -\> machine run in loop.

Sau quá trình này chỉ cần "tệp chương trình". (Văn bản đã biên dịch)

Interpreted language -\> src code -\> interpreter -\> machine run in
loop. (Live translate)

Cần toàn bộ quá trình khi chạy (cần người phiên dịch)

![](/assets/img/interpreter_compiler.png){width="4.3702504374453195in"
height="2.6769050743657044in"}
https://ruslanspivak.com/lsbasi-part1/

## Các syntax cho script

\# Sharp -\> Cho command

! Bang -\> Có nhiều các sử dụng (!n) xem lịch sử lệnh thứ n, (!!) Thực
hiện lệnh gần nhất, (!string) lệnh gần nhất bắt đầu bằng string. Dùng
cho toán tử phủ định khi đứng riêng lẽ mang nghĩa not. Để tham chiếu giá
trị đặc biệt

=\> Kết hợp lại (#!/bin/bash) chỉ đến trình thông dịch dùng để thông
dịch code trong file.

\$ tham chiếu biến (\$HOME, \$USER)

'command' hoặc \$(command): Thực thi lệnh và lấy kết quả

\>\>, \> chuyển hướng đầu ra (nối thêm/ ghi đè)

\< chuyển hướng đầu vào

& background process

; ngăn cách nhiều lệnh trên cùng một dòng (chấm phẩy)

&& và \|\|: toán tử AND và OR

\\ để thoát kí tự đặc biệt

\*,?,\[ \] là các wildcard để tìm kiếm và lọc file

## Note for script

Script rất khắc khe về khoảng cách trong code khác với code thông
thường, mọi thứ trong script phải được viết liền nhau không có khoảng
trắng, ví dụ như

- Lệnh gán: VAR=1000 hoặc VAR='string

Trong script không có các dấu chấm phẩy để phân biệt giữa các line code,
xuống hàng là một cách để ngăn cách giữa các code line. Thay vào đó nó
có xu hướng sử dụng các từ ngữ làm mô tả cho thực hiện, cái này follow
theo interpreter. Ví dụ như câu điều kiện

+-----------------------------------------------------------------------+
| #Ask a variable value from input                                      |
|                                                                       |
| read -p 'Enter the name: ' NAME                                       |
|                                                                       |
| if \[\[ "\${UID}" -ne "\${VAR}" }}                                    |
|                                                                       |
| then                                                                  |
|                                                                       |
| Command 1                                                             |
|                                                                       |
| Command 2                                                             |
|                                                                       |
| exit 1                                                                |
|                                                                       |
| else                                                                  |
|                                                                       |
| Command 1                                                             |
|                                                                       |
| Command 2                                                             |
|                                                                       |
| exit 0                                                                |
|                                                                       |
| fi                                                                    |
+=======================================================================+
{% raw %}
Qua ví dụ trên trong câu điều kiện {{ được thay cho ( và sau dấu \[\[ có
thêm 1 khoảng trắng và kế thúc cũng vậy, và then thay cho dấu { để bắt
đầu một vòng if.
{% endraw %}
Sử dụng "fi" để kết thúc một câu điều kiện, và else thì không cần phải
có then theo sau, cứ code như python là đủ.

Lệnh thoát exit(value) dùng cho việc thoát nếu cần với giá trị 0 là
okey, còn nếu là non-zero thì nó là false. Mỗi trường hợp exit non-zero
tức là false thường có một giá trị riêng thể hiện thông điệp của nó, vậy
nên mình có thể check thông điệp tương ứng.

Ngoài ra trong shell spt thì dấu " và dấu ' cũng có sự khác biệt. Dấu
nháy " cho phép nội dung trong đó bị thay đổi có thể ví dụ như việc giải
tham chiếu bên trong "\${VAR}", ngược lại dấu nháy đơn '\${VAR}' thì sẽ
hiển thị chính xác nội dung trong đó không thể thay đổi gì.
