**\_\_\_**

Nguyễn Minh Nhựt

# GIỚI THIỆU

Bài viết về sự khác biệt giữa giao tiếp theo phương thức song song và
nối tiếp trong các truyền dẫn tín hiệu, được khám phá ra khi đang đọc
datasheet của TFT LCD ST7735 giao tiếp bằng các con MCU 8080 parallel
interface

[Sai lầm thường gặp]{.underline}:

X, Parallel là nhanh hơn Serial. ( cái này chỉ đúng với những năm về
trước thôi, giờ thì chưa chắc)

## Kiến trúc của giao tiếp song song và nối tiếp

Giao tiếp song song: Giao tiếp // được hiểu đơn giản là việc truyền
nhiều tín hiệu (dữ liệu) khác nhau thông qua nhiều line trong cùng một
thời điểm. Vậy có 2 tính chất cơ bản của việc truyền tín hiệu này là:
Nhiều line và đồng thời (các dữ liệu khác nhau).

\*hình ảnh minh họa

Giao tiếp nối tiếp: Trực tiếp hơn bằng cách chuyển từng bits một thông
qua có thể là bằng frame dữ liệu bit by bit method.

\*hình ảnh minh họa

## Sự khác nhau đặc trưng của hai cách kết nối

Đây là một bảng so sánh về sự khác nhau giữa hai giao thức, nhưng nhìn
chung vài khẳng định vẫn còn mơ hồ cần kiểm chứng

  ------------------------------------------------------------------------
  **Các khía cạnh**  **Serial              **Parallel Communication**
                     Communication**       
  ------------------ --------------------- -------------------------------
  **Speed truyền     Slower.               Faster.
  ngắn**                                   

  **Độ phức tạp**    Simple for long       Simple for short distances.
                     distances.            

  **Chi phí**        Cheaper.              Expensive.

  **Độ tin cậy       Reliable.             May suffer signal degradation
  truyền dài**                             sometimes.

  **Tính đồng bộ**   Complex at very high  Easier to synchronize at short
                     speeds.               distances.

  **Kết nối**        Requires fewer wires. Requires more wires.

  **Ứng dụng**       Keyboards, mice, and  The data bus.
                     sensors.              
  ------------------------------------------------------------------------

**List adjustment:**

### Speed 

> Tốc độ ngày nay giữa hai phương pháp truyền có sự chênh lệch rất lớn
> do có nhiều hơn 1 phương pháp truyền như xưa, cần đề cập về vấn đề:

- Truyền vi sai: MCU sides thì vẫn bit by bit với serial nhưng giờ dữ
  liệu không còn truyền trên 1 line nữa mà thay vào đó là 2 line đối
  xứng -\> hạn chế nhiễu, vấn đề mà UART vẫn gặp khi distance truyền \>
  40cm (thực nghiệm). CAN bus là một ví dụ, đặc tính của CAN cũng rõ là
  tốc độ rất cao và reliable.

- Trong khi đó Parallel lại mang quá nhiều dữ liệu khác nhau trên nhiều
  line, phải chia nhiều line gửi + data khác nhau + không có vi sai, nên
  truyền dài sẽ dể bị "hụt" dữ liệu tốc độ cũng thấp hơn 10 lần mỗi line
  (1 senior 20 năm nói) do đó speed giờ là yếu điểm của cấu trúc này.

- Concept parallel vẫn cho tốc độ nhanh khi áp dụng lên Serial bằng cách
  chia nhiều channel khác nhau, nhưng về cơ bản chúng là bit by bit
  communication.

### Cost

> Cost của các serial cao cấp như CAN hay flexray có thể có chi phí rất
> cao so với nhiều chuẩn Serial
>
> Xưa trong máy tính có nhiều kết nối dạng tép nhiều line dẫn trong đó
> -\> có thể nó la Parallel
>
> Giờ hầu hết các ổ đĩa đều được chuyển sang các cổng sata.
>
> ![](/assets/img/parallel_to_serial_port.png){width="4.225in" height="1.1625in"}
>
> Ví dụ về Parallel sang Serial
>
> ![](/assets/img/parallel_to_serial_port_1.png){width="1.74375in" height="1.28125in"}

## Interface

Interface là một từ cũng có thể sử dụng khi nói về vấn đề này chúng y
chang nhau.

### Liệt kê các Interface của hai giao thức 

  -----------------------------------------------------------------------
  Serial interface                   Parallel interface
  ---------------------------------- ------------------------------------
  I2C                                ISA

  SPI                                ATA

  USB                                SCSI

  RS-232                             IEEE 488

  CAN                                PCI

  Ethernet                           

  SATA                               

  1-Wire                             
  -----------------------------------------------------------------------

## Tham khảo thêm

https://www.geeksforgeeks.org/serial-vs-parallel-communication-in-microprocessor/
