---
layout: post
title: "Khác nhau giữa string và wstring"
categories: [technical]
tags: [string, wstring, char, wchar, language]
---

**Sự khác nhau giữa string và wstring (UNICODE and ANSI)**

- Vấn đề này được khám phá từ đâu?

Trong lúc viết tool code để đọc nội dung của multiple file trong một thư
mục do đó cần phải dùng đến thư viện windows.h thay vì filesystem vì
không hỗ trợ cho chuẩn c++98.

- Trong nội dung này bàn luận về std::string và std::wstring

<u>Author mention:</u> Questions 402283 trên Stackoverflow

**1.  Bối cảnh:**

Trên thế giới có nhiều loại ngôn ngữ khác nhau, do vậy có nhiều chuẩn
được thiết đặt như ASCII (Unicode8 - UTF8), Unicode 16/32,...Trong bảng
mã ASCII hầu hết là các kí tự latinh và một vài kí tự phổ biến, đặc biệt
là mô tả các ngôn ngữ như tiếng anh.

Chính vì tiếng anh là ngôn ngữ thống nhất toàn cầu nên hệ thống máy tính
cũng sử dụng nó

- Tối ưu bộ nhớ 8bit so với 16 hay 32 bit như UNICODE

- Dể nắm bắt và debug cho các developer global

Từ đó hai kiểu dữ liệu **string** và **wstring** được ra đời, cái này
mình cũng chỉ mới biết khi làm tool để check các tệp trên Windows. Do
string là tập hợp các char lại với nhau nên cũng biết rằng có hai kiểu
dữ liệu **char** và **wchar**.

**2.  Sự khác nhau về mặt kĩ thuật**

Kiểu dữ liệu char có kích thước là 1 byte, trong khi đó wchar có kích
thước là 4 bytes trên Windows x64 và 2 bytes trong Linux.

Thông tin xem rõ hơn trên <u>stackoverflow.com/questions/402283</u>
