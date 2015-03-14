Các phép toán màu sắc thường nhận tham số có cùng đơn vị với màu đối chiếu, và phần trăm với giá trị tuyệt đối, vì vậy tăng 10% của 10% giá trị sẽ là 20% chứ không phải 11%, và các giá trị được giới hạn trong phạm vi cho phép. Với những phép toán trả về giá trị, bên cạnh giá trị màu hex quen thuộc, Less sử dụng các định dạng phù hợp giúp bạn dễ dàng hiểu chức năng của từng phép toán.

### saturate

> Tăng giá trị saturation trong không gian màu HSL lên một lượng xác định

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `saturate(hsl(90, 80%, 50%), 20%)`

Kết quả: `#80ff00 // hsl(90, 100%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80ff00:#000000/text:80ff00)

### desaturate

> Giảm giá trị saturation trong không gian màu HSL đi một lượng xác định

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `desaturate(hsl(90, 80%, 50%), 20%)`

Kết quả: `#80cc33 // hsl(90, 60%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80cc33:#000000/text:80cc33)

### lighten

> Tăng giá trị lightness trong không gian màu HSL lên một lượng nhất định.

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `lighten(hsl(90, 80%, 50%), 20%)`

Kết quả: `#b3f075 // hsl(90, 80%, 70%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#b3f075:#000000/text:b3f075)

### darken

> Giảm giá trị lightness trong không gian màu HSL đi một lượng nhất định.

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `darken(hsl(90, 80%, 50%), 20%)`

Kết quả: `#4d8a0f // hsl(90, 80%, 30%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#4d8a0f:#000000/text:4d8a0f)

### fadein

> Giảm độ trong suốt (tăng độ đục) của màu, làm nó thêm đục.

Không có tác dụng trên màu đục. Dùng `fadeout` để fade theo hướng ngược lại.

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `fadein(hsla(90, 90%, 50%, 0.5), 10%)`

Kết quả: `rgba(128, 242, 13, 0.6) // hsla(90, 90%, 50%, 0.6)`


### fadeout

> Tăng độ trong suốt (giảm độ đục) của màu, làm nó thêm trong suốt.
Dùng `fadein` để fade theo hướng ngược lại.

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `fadeout(hsla(90, 90%, 50%, 0.5), 10%)`

Kết quả: `rgba(128, 242, 13, 0.4) // hsla(90, 90%, 50%, 0.4)`


### fade

> Chỉnh độ trong suốt của một màu đến một độ nhất định. Có thể áp dụng với màu đã sẵn trong suốt và cả màu đục.

Tham số:
* `color`: Đối tượng màu.
* `amount`: Phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `fade(hsl(90, 90%, 50%), 10%)`

Kết quả: `rgba(128, 242, 13, 0.1) //hsla(90, 90%, 50%, 0.1)`


### spin

> Quay góc hue đi một góc.

Bạn có thể sử dụng một số bất kỳ, less sẽ xử lý và trả về số đo góc tương đương. Ví dụ: 360 và 720 sẽ cho ra cùng một kết quả. Lưu ý rằng màu được truyền qua hàm chuyển đổi RGB, và hàm này không giữ giá trị hue của các màu xám (vì hue không có ý nghĩa gì khi không có saturation), vì vậy hãy đảm bảo rằng bạn sử dụng các function đúng cách để giữ lại hue, đừng làm như ví dụ sau:

```less
@c: saturate(spin(#aaaaaa, 10), 10%);
```

Thay vào đó, hãy làm như thế này:

```less
@c: spin(saturate(#aaaaaa, 10%), 10);
```

Giá trị màu trả về luôn là RGB, vì vậy dùng `spin` vào một màu xám sẽ là vô nghĩa.

Tham số:
* `color`: Đối tượng màu.
* `angle`: Góc quay.

Trả về: `color`

Ví dụ:

```less
spin(hsl(10, 90%, 50%), 30)
spin(hsl(10, 90%, 50%), -30)
```

Kết quả:

```css
#f2a60d // hsl(40, 90%, 50%)
#f20d59 // hsl(340, 90%, 50%)
```

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f2a60d:#000000/text:f2a60d)

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f20d59:#000000/text:f20d59)

### mix

> Trộn hai màu vào nhau theo tỷ lệ biến (bao gồm cả độ đục).

Tham số:
* `color1`: Đối tượng màu.
* `color2`: Đối tượng màu.
* `weight`: không bắt buộc, phần trăm (điểm cân bằng giữa hai màu), mặc định là 50%, defaults to 50%.

Trả về: `color`

Ví dụ:

```less
mix(#ff0000, #0000ff, 50%)
mix(rgba(100,0,0,1.0), rgba(0,100,0,0.5), 50%)
```

Kết quả:

```css
#800080
rgba(75, 25, 0, 0.75)
```

![Color 1](holder.js/100x40/#ff0000:#ffffff/text:ff0000) + ![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff) ➜ ![Color 3](holder.js/100x40/#800080:#ffffff/text:800080)

### greyscale

> Loại bỏ tất cả saturation khỏi màu trong không gian màu HSL; tương đương với `desaturate(@color, 100%)`.

Do hue không tác động lên saturation nên phép ánh xạ màu có thể mờ hoặc lộn xộn; [`luma`](#color-channel-luma) có thể đem lại kết quả tốt hơn vì nó trích xuất theo độ sáng cảm quan thay vì độ sáng tuyến tính, ví dụ `greyscale('#0000ff')` sẽ trả về kết quả giống với `greyscale('#00ff00')`, mặc dù hai màu này khác nhau khá nhiều về độ sáng đối với mắt người.

Tham số: `color`: Đối tượng màu.

Trả về: `color`

Ví dụ: `greyscale(hsl(90, 90%, 50%))`

Kết quả: `#808080 // hsl(90, 0%, 50%)`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#808080:#000000/text:808080)

Lưu ý rằng màu xám được tạo ra trông sẽ tối hơn màu xanh gốc, dù giá trị lightness là như nhau.

So sánh việc sử dụng `luma` (cách dùng sẽ khác nhau vì `luma` trả về một giá trị đơn, không phải một màu):

```less
@c: luma(hsl(90, 90%, 50%));
color: rgb(@c, @c, @c);
```

Kết quả: `#cacaca`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#cacaca:#000000/text:cacaca)

Trong trường hợp này, giá trị lightness của màu xám trông sẽ giống với màu xanh, mặc dù giá trị của nó lớn hơn.

### contrast

> Chọn màu có độ tương phản cao hơn trong hai màu.so vỚi màu đối chiếu.

Hàm này khá hữu ích khi bạn cần đảm bảo rằng màu chữ đủ nổi bật và dễ đọc so với màu nền, tuân theo chuẩn khả năng truy nhập. Hàm này hoạt động giống như [hàm contrast trong framework Compass của ngôn ngữ SASS](http://compass-style.org/reference/compass/utilities/color/contrast/). Theo [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef), các màu được so sánh dựa trên [luma đã hiệu chính gamma](#color-channel-luma) chứ không dựa trên lightness.

Các tham số sáng và tối có thể đảo cho nhau trong thứ tự tham số truyền vào - Less sẽ tính giá trị luma của các màu và chọn ra trong hai màu một màu sáng một màu tối một cách tự động, cũng có nghĩa là bạn không thể sử dụng hàm này để chọn ra màu có mức tương phản *thấp nhất* bằng cách đảo thứ tự tham số.

Tham số:
* `color`: Màu đối chiếu
* `dark`: không bắt buộc - Màu tối (mặc định là màu đen).
* `light`: không bắt buộc - Màu sáng (mặc định là màu trắng).
* `threshold`: không bắt buộc - Phần trăm (trong khoảng 0-100%) xác định điểm chuyển đổi giữa "tối" và "sáng" (mặc định là 43%, giống với SASS). Tham số này được sử dụng để chuyển dịch độ tương phản nghiêng về một bên, chẳng hạn như khi bạn muốn quyết định tương phản so với nền xám 50% nên là chữ đen hay chữ trắng. Thông thường,, giá trị này với bảng màu sáng sẽ thấp hơn, và sẽ cao hơn ở bảng màu tối.

Trả về: `color`

Ví dụ:

```less
p {
    a: contrast(#bbbbbb);
    b: contrast(#222222, #101010);
    c: contrast(#222222, #101010, #dddddd);
    d: contrast(hsl(90, 100%, 50%), #000000, #ffffff, 30%);
    e: contrast(hsl(90, 100%, 50%), #000000, #ffffff, 80%);
}
```

Kết quả:

```
p {
    a: #000000 // black
    b: #ffffff // white
    c: #dddddd
    d: #000000 // black
    e: #ffffff // white
}
```
Những ví dụ dưới đây sử dụng các màu từ phép tính bên trên làm màu nền và màu chữ; bạn có thể thấy rằng kết quả không bao giờ là nền trắng chữ trắng hay nền đen chữ đen, dù rằng bạn có thể sử dụng giá trị threshold để cho ra một kết quả có độ tương phản thấp hơn, như ở ví dụ cuối cùng:

![Color 1](holder.js/100x40/#bbbbbb:#000000/text:000000)
![Color 1](holder.js/100x40/#222222:#ffffff/text:ffffff)
![Color 1](holder.js/100x40/#222222:#dddddd/text:dddddd)
![Color 1](holder.js/100x40/#80ff00:#000000/text:000000)
![Color 1](holder.js/100x40/#80ff00:#ffffff/text:ffffff)
