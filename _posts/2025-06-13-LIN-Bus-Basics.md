---
layout: post
title: "LIN Bus Basics"
date: 2025-06-13 16:26:00 +0700
categories: [Protocol]
tags: [LIN, protocol, automotive]
---

**\_\_\_**

Nguyễn Minh Nhựt

# GIỚI THIỆU

Trong Series Network Protocol phổ biến gồm 3 loại Network chính như sau:
CAN, LIN, Flexray là các protocol hiện có trong các lĩnh vực Automotive
và Industrial. Các chuẩn truyền thông này có độ tin cậy cao, tín hiệu
truyền theo dạng vi sai và có tốc độ truyền tải cao nên được áp dụng phổ
biến. Các truyền thông này theo phương pháp broadcasting message frame
đến các node trong mạng, diagnostic/ error handle/ start stop bit đều
có. Trong nội dung này sẽ giới thiệu về LIN bus.

## Khái niệm và specs của protocol

Là một mạng truyền thông dạng broadcasting serial network bao gồm 16
nodes trong đó gồm 1 primary node (master node) và các secondary node
(slave node) còn lại (upto 15 note).

Hỗ trợ tốc độ truyền thông 19.2 Kbit/second, trong khi đó chỉ hỗ trợ
truyền thông tối đa là 40m. Nâng cấp lên thì Bandwidth là 20Kbit/second.

**[Pros khi sử dụng LIN:]{.underline}**

- Tiết kiệm kinh phí phát triển

- Khả năng truyền tải tốt hơn, hay cụ thể là về mặt chống nhiễu tốt và
  đảm bảo với mức điện áp 12/24 Vdc thay vì 5 Vdc như CAN bus.

- Trong xe có những thành phần điều khiển không quan trọng lắm, cho nên
  không cần dùng CAN để điều khiển, LIN lại có đặc tính là cũng tương tự
  với CAN và có thể là phần kết nối phụ hỗ trợ điều khiển các thành phần
  đó.

- Chỉ có duy nhất 1 master node.

- Chỉ sử dụng 6 bits ID thay vì 11/ 29 bits như CAN.

> ![](/assets/img/lin_topology.png){width="3.937007874015748in"
> height="1.990797244094488in"}

*Figure 1: LIN và đồng bọn của nó*

> ![](/assets/img/lin_topology_in_car.png){width="3.937007874015748in"
> height="2.1468471128608924in"}

*Figure 2: Một vài cái sử dụng LIN*

## LIN Connection

![](/assets/img/lin_connection.png){width="6.299212598425197in"
height="2.683895450568679in"}

*Figure 3: Cấu trúc kết nối của một giao thức LIN*

Có thể thấy trong hình 3, LIN chỉ dùng duy nhất 1 dây để truyền dữ liệu
khác hoàn toàn với CAN là sử dụng 2 dây, cũng chính vì lý do này mà nó
phải truyền ở mức điện áp 12V để đảm bảo chất lượng tín hiệu.

Sẵn đó ta có luôn là nó sẽ có DUY NHẤT 1 Master và gồm nhiều SLAVE, còn
với CAN là giao tiếp ngang hàng.

Dữ liệu truyền được 2 chiều (bidirectional) trong BUS.

> ![](/assets/img/lin_connection_inside.png){width="6.299212598425197in"
> height="2.940978783902012in"}

*Figure 4 Cấu hình bên trong driver*

Ngoài ra, nó còn sử dụng 1 RES khoảng 1 Kom nối song song với RES 30 Kom
tại VBAT , để hạn chế dòng tiêu thụ (current draw). 30 Kom thì dùng để
giữa cho LIN bus ở điện áp mức cao.

## LIN Topology

Primary node thường là node chính (có thể gọi là master-node)
broadcasting message cho các node khác(node slave ngang hàng) trong
mạng.

Tất cả message đều được khởi tạo bởi node chính, các node phụ chỉ có
chức năng trả lời thông tin và có tối đa là 1 node tương đương với một
mã header gửi ra duy nhất. =\> còn không thì sẽ make collision message.

## Notes for LIN

- Đảm bảo về mặt độ trễ.

- Multicast reception - Nhận thông tin đa chiều và đồng thời với đồng bộ
  thời gian **không cần phải có dao động thạch anh.**

- Có nhiều thứ trên CAN như checksum, error detection, fault detection,
  phân cấp mạng/ network

- Điện áp vận hành là 12V

**[Các message được concern trong LIN]{.underline}**

- Đồng bộ hóa break

- Đồng bộ hóa byte

- Byte ID byte (Identifier byte)

- Data bytes

- Checksum byte

## LIN Frame types

Unconditional-frame (vô điều kiện): Identifier ID range from 00 to 3b.
All nodes that received the frame will execute information for
application. - default frame - cần chú ý rằng LIN master cần phải truyền
data để phản hồi cho header cụ thể.

Event-trigger frame: frame được dùng thông báo các trigger với sự kiện
bên ngoài môi trường. Việc enable frame này giúp cho LIN tăng tính thích
nghi/ nhạy cảm và ví dụ thường dùng để theo dõi door knobs (tay nắm cửa
trên xe ô tô)

nguyên lý hoạt động: master request data từ nhiều slave -\> slave
response nếu thông tin của nó được update, với protected id (PID) trong
byte data đầu tiên -\> nếu có nhiều slave response cùng một lúc thì nó
sẽ có hiện tượng là collision -\> master chuyển sang uncondition frame
tạm thời để request lần lượt từng còn slave trả lời -\> Lưu lý là cái
hiện tượng collision sẽ không được xem là lỗi LIN từ bất cứ node nào

Sporadic frame

Frame này cho phép linh động trong cách mà slave phản hồi (dynamic way)
nếu mà có collision thì nó sẽ auto response theo ưu tiên về ID (thấp
nhất) sau đó sẽ gửi ID còn lại, nếu 1 trong 2 có data update thì nó sẽ
work như bình thường, còn lại thì silent.

## Tham khảo thêm
