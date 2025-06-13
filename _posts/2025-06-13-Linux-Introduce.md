---
layout: post
title: "Linux Introduce"
date: 2025-06-13 16:26:00 +0700
categories: [Linux]
tags: [Linux]
---

**\_\_\_**

Nguyễn Minh Nhựt

# GIỚI THIỆU

Bài viết về Linux OS hệ điều hành mã nguồn mở được sử dụng phổ biến
trong nhiều thiết bị (hầu như là ở khắp mọi nơi) từ máy tính cá nhân đến
các hệ thống trạm cao cấp phục vụ cho mục đích quân sự hoặc khám phá
khoa học

Bên cạnh Linux tùy vào domain đang nói đến mà còn có thể có nhiều OS
khác ví dụ như GPOS (Windows, Mac) , RTOS (Realtime application) dành
cho các thiết bị yêu cần timing chặt chẽ ví dụ như mục đích quốc phòng/
y tế/ vận hành các thiết bị có yêu cầu cao như công nghiệp, urgent,\...

## Định nghĩa về OS

- Hệ điều hành được hiểu về cơ bản là phần mềm của hệ thống, một hệ
  thống ví dụ như PC chỉ có thể khởi động lên vả chỉ có thể phát lên vài
  tiếng \*bip vì nó không tìm thấy được phần mềm (OS) cần boot.

- Mỗi khi có một action gì trong phần mềm chính (hệ điều hành) thì
  chương trình sẽ được thông dịch sang cho hardware của máy tính. Chính
  vì vậy, khi thiết kế phần mềm cần phải cung cấp các thông tin về
  nguyên lý làm việc của từng thiết bị có trên máy tính.

- Nếu bỏ qua các chi tiết thì OS được xem như là gốc rễ của các phần mềm
  chạy "on-top" của nó, OS sẽ được chạy liên tục để chuyển thông thông
  tin từ end-user đến máy tính, vấn đề về control.

- Chức năng cơ bản nhất của một OS, thường được biết đến là quản lý thư
  mục và file.

## UNIX distribution

> Chính xác thì UNIX là một hệ điều hành được phát triển bới bell LAB
> tách ra từ công ty AT&T (một nhà mạng nổi tiếng tại Mĩ). Là bố của các
> hệ điều hành và trong các hệ điều hành được phát triển thì Linux là
> một trong các bản phân phối miễn phí khác với MACOS và WINDOW

## Linux partition

Phần cứng: gồm tất cả các thiết bị có trên máy tính như memory, CPU, ổ
đĩa, ..

Linux kernel: là lõi của hệ điều hành, quản lý phần cứng và tương tác
với toàn bộ hệ thống.

User Space: dành cho các người dùng phổ trong truy cập. Được chia thành
2 thể loại user-space là CLI and GUI.

## Linux category

- Ubuntu là hđh dựa trên Debian do vậy sẽ sử dụng các Debian package để
  quản lý hệ thống.

- Fedora thì thay Debian bằng Red Hat Enterprise Linux (RHEL), thực chất
  là fedora được phân nhánh từ red hat.

- Linux Mint dựa trên ubuntu và sử dụng phần mềm của nó nên được coi là
  sử dụng pkg của Debian

- Arch linux, nhẹ và linh hoạt, được đóng góp 1000% từ cộng đồng, cái
  này thì sử dụng PACMAN của chính nó để control

- openSUSE, created by the openSUSE Project, Uses RPM package manager.
