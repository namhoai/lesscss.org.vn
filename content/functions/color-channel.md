### hue

> Lấy giá trị kênh hue của đối tượng màu trong không gian màu HSL.

Tham số: `color` - đối tượng màu.

Trả về: `integer` `0-360`

Ví dụ: `hue(hsl(90, 100%, 50%))`

Kết quả: `90`


### saturation

> Lấy giá trị kênh saturation của đối tượng màu trong không gian màu HSL.

Tham số: `color` - đối tượng màu.

Trả về: `percentage` `0-100`

Ví dụ: `saturation(hsl(90, 100%, 50%))`

Kết quả: `100%`


### lightness

> Lấy giá trị kênh lightness của đối tượng màu trong không gian màu HSL.

Tham số: `color` - đối tượng màu.

Trả về: `percentage` `0-100`

Ví dụ: `lightness(hsl(90, 100%, 50%))`

Kết quả: `50%`


### hsvhue

> Lấy giá trị kênh hue của đối tượng màu trong không gian màu HSV.

Tham số: `color` - đối tượng màu.

Trả về: `integer` `0-360`

Ví dụ: `hsvhue(hsv(90, 100%, 50%))`

Kết quả: `90`


### hsvsaturation

> Lấy giá trị kênh saturation của đối tượng màu trong không gian màu HSV.

Tham số: `color` - đối tượng màu.

Trả về: `percentage` 0-100

Ví dụ: `hsvsaturation(hsv(90, 100%, 50%))`

Kết quả: `100%`


### hsvvalue

> Lấy giá trị kênh value của đối tượng màu trong không gian màu HSV.

Tham số: `color` - đối tượng màu.

Trả về: `percentage` 0-100

Ví dụ: `hsvvalue(hsv(90, 100%, 50%))`

Kết quả: `50%`


### red

> Lấy giá trị kênh red của đối tượng màu.

Tham số: `color` - đối tượng màu.


Ví dụ: `red(rgb(10, 20, 30))`

Kết quả: `10`


### green

> Lấy giá trị kênh green của đối tượng màu.

Tham số: `color` - đối tượng màu.

Trả về: `integer` 0-255

Ví dụ: `green(rgb(10, 20, 30))`

Kết quả: `20`


### blue

> Lấy giá trị kênh blue của đối tượng màu.

Tham số: `color` - đối tượng màu.

Trả về: `integer` 0-255

Ví dụ: `blue(rgb(10, 20, 30))`

Kết quả: `30`


### alpha

> Lấy giá trị kênh alpha của đối tượng màu.

Tham số: `color` - đối tượng màu.

Trả về: `float` `0-1`

Ví dụ: `alpha(rgba(10, 20, 30, 0.5))`

Kết quả: `0.5`


### luma

> Tính [luma](http://en.wikipedia.org/wiki/Luma_%28video%29) (độ sáng cảm quang) của đối tượng màu.

Uses 
 coefficients, as recommended in 
Sử dụng hệ số **SMPTE C / Rec. 709** theo như [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef). Phép tính này cũng được sử dụng trong hàm contrast.

Trước phiên bản v1.7.0, hàm tính luma không có bước hiệu chỉnh gamma. Từ phiên bản v1.7.0, hàm này được đổi tên thành `luminance`.

Tham số: `color` - đối tượng màu.

Trả về: `percentage` 0-100%

Ví dụ: `luma(rgb(100, 200, 30))`

Kết quả: `44%`


### luminance

> Tính giá trị luma khi bỏ qua bước hiệu chỉnh gamma (trước phiên bản v1.7.0, hàm này tên là `luma`)

Tham số: `color` - đối tượng màu.

Trả về: `percentage` 0-100%

Ví dụ: `luminance(rgb(100, 200, 30))`

Kết quả: `65%`
