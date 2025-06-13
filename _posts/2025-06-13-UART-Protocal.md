**\_\_\_**

Nguyễn Minh Nhựt

# GIỚI THIỆU

UART, or universal asynchronous receiver-transmitter, là một trong những
giao thức truyền thông phố biến nhất giữa các thiết bị, ngoài ra còn là
một serial protocol hay cổng truyền thông nối tiếp (gửi từng bit một --
bit by bit trên một kênh -- single channel, còn cổng truyền thông song
song truyền đồng thời -- simultaneously thông qua nhiều kênh khác nhau).

Trong giao tiếp hai chiều, thì sử dụng 2 dây để truyền tải thông tin do
mỗi bên đều có 2 pin là TX-RX, do đó consider là có thể sử dụng ít hơn 2
dây nếu chỉ sử dụng một chiều (maybe)

Các đối tượng sử dụng UART thường là embedded sys, micro-controller,
computers trong layer là hardware device layer hay còn được gọi là
hardware protocal.

[=\> Được sử dụng nhiều không đồng nghĩa là lúc nào nó cũng tối
ưu]{.underline}

Asynchronous có nghĩa là không cần tới clock để sync các output bits từ
nơi gửi đến nơi nhận.

## UART Interface

> ![What is UART Communication? Block Diagram -
> ETechnoG](/assets/img/uart_connect_in_device.png){width="4.306059711286089in"
> height="2.474747375328084in"}

***Figure 1 Kết nối UART trong device***

> Cần lưu ý:

- Cấu hình về Baudrate, giống nhau ở các device muốn giao tiếp với nhau
  (đại diện cho số lượng bits muốn truyền đi trong một giây - speed)

- Baudrate phổ biến sử dụng từ 9600 -\> 1.500.000

- Chỉ được kết nối truyền thông giữa hai thiết bị duy nhất

> Như đã đề cập, UART không sử dụng clock từ Master để điều khiển như
> SPI vì vậy nó cần phải có một phương pháp để đồng bộ hóa các dữ liệu/
> message truyền nhận này.
>
> [Vậy nó sync như thế nào?]{.mark}

- **Transmitter** tạo ra **bitstream** dựa trên chính clock signal của
  nó.

- **Transmitter** tạo ra **bitstream** dựa trên chính clock signal của
  nó.

- **Receiver** cũng tự dùng **internal clock** của nó dể lấy mẫu data
  được gửi đến.

<!-- -->

- **Đó là vì sao mà cần phải cấu hình baudrate giống nhau**

<!-- -->

- Độ sai lệch trong khoảng dưới 10% khi configue baudrate.

## UART Frame

> Đương nhiên khứa nào cũng sẽ có frame UART cũng có nhưng mà sẽ ngắn
> hơn các frame khác ở dạng tiêu chuẩn (tại có thông tin là nó ra đời
> tiên mà nên cũng hiểu là nó phải là các basic nhất có thể - USART).
>
> ![](/assets/img/uart_frame.png){width="5.867522965879265in"
> height="0.6331408573928259in"}

***Figure 2 UART Data Frame***

> **Start bit**, thường hold ở mức cao khi không có giao tiếp gì, cho
> đến khi pull xuống low trong 1 clock cycle.
>
> **Data Frame**, thì cái này include luôn cái parity bit nếu data của
> mình trong khoảng 5-8 bits, còn nếu mà data tới tận 9 bits thì coi như
> không sài cái parity bit.
>
> **Parity bit** là bit check tính chẳn lẽ (even/odd), hoặc bất cứ gì
> trong quá trình truyền thì nó cũng report theo cái bit này từ receiver
> lên transmitter.

- Tính chẵn lẻ: PB=0 thì tổng các bit cao (logic 1) trong frame sẽ là số
  chẵn, và ngược lại.

- Match với rule trên thì OK/ Positive **còn ngược lại là Địt cụ lỗi
  luôn**.

> **Stop bit**, đẩy ngược lại về HIGH (logic 1) được xác định trong 1
> hoặc 2 chu kì bit.
>
> **Truyền thì truyền MSB bit trước nhé**
>
> ![](/assets/img/uart_frame_1.png){width="5.953159448818898in"
> height="0.8548118985126859in"}

***Figure 3 UART Root Frame***

> Thường thì nó chỉ giao tiếp với hai con nên các Frame này ít khi được
> nhắc đến do có Header cũng làm quần què gì đâu, vậy nên có config luôn
> cái ID Header rồi.

- H1 là 0xAB, H2 là 0xCD **(Unique)**

- CMD hay command thì có 1 list sẵn lệnh giao tiếp giữa hai con là gì tự
  chọn luôn.

- Data length thì có thể điều chỉnh ( dựa trên command đã chọn ).

- Trailer 1 là 0xE1 và Trailer 2 là 0xE2 **(Unique)**

- CRC check sum giữa bên nhận với bên gửi.

> [Baud rate = PCLK/((M + N/2048) × 2^OSR\ +\ 2 ^× DIV]{.mark}

## UART Terminology

- OSR, over sampler rate

- DIV, Baud Rate divider

- M (DIVM fractional baud rate M)

- N (DIVM fractional baud rate N)

## Use case

> You can use UART for many applications, such as:

- **Debugging**: Early detection of system bugs is important during
  development. Adding UART can help in this scenario by capturing
  messages from the system.

- Manufacturing **function-level tracing**: Logs are very important in
  manufacturing. They determine functionalities by alerting operators to
  what is happening on the manufacturing line.

- **Customer or client updates**: Software updates are highly important.
  Having complete, dynamic hardware with update-capable software is
  important to having a complete system.

- **Testing/verification**: Verifying products before they leave the
  manufacturing process helps deliver the best quality products possible
  to customers.

## Tips for working with protocol

> Khi lần đầu tiếp cận với một protocol về hardware đang sử dụng thì có
> vài điều cần thực hiện theo thứ tự sau.

1.  Kiểm tra các chân được attach để giao tiếp UART và các specific
    operation mode, frame format, data length, bit start/stop.

2.  Số lượng thanh ghi của giao thức UART (data, interrupt, status,
    control,...) và tính toán về baudrate tùy vào MCU.

## Formula

> ![](/assets/img/uart_formuler.png){width="6.5in" height="3.2597222222222224in"}

***Figure 4 Công thức tính UART của NXP 1768***

> Trong công thức trên thì có các biến cũng hơi confuse chút sẽ làm rõ
> như sau:

- **PCLK** là peripheral clock tần số xung cơ bản của các I/O, cổng vào
  ra vật lý (quản lý bới bare system).

- **MULVAL (Phần nguyên) và DIVADDVAL (Phần thập phân),** kết hợp với
  nhau tạo thành bộ chia nhỏ tần số (fractional deivider) xuống mức phù
  hợp với cấu hình baudrate của giao thức tương ứng.

![](/assets/img/uart_config_examble_stm.png){width="5.511811023622047in"
height="2.4279057305336833in"}

***Figure 5 Ví dụ***

> Với hai biến còn lại thì dường như là chỉ dùng để hiệu chỉnh lại chút
> cho chính xác với configs.

1.  Reference

> Có thể tham khảo lại cái
> [[https://www.byte-lab.com/explaining-uart-protocol/]{.underline}](https://www.byte-lab.com/explaining-uart-protocol/)
> nếu cần.
