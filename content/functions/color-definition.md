### rgb

> Tạo đối tượng màu từ các giá trị red, green và blue (RGB).

Giá trị màu chuẩn theo định dạng HTML/CSS cũng có thể được dùng tạo màu, ví dụ `#ff0000`.

Tham số:
* `red`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).
* `green`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).
* `blue`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `rgb(90, 129, 32)`

Kết quả: `#5a8120`


### rgba

> Tạo đối tượng màu trong suốt từ các giá trị red, green, blue và alpha (RGBA).

Tham số:
* `red`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).
* `green`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).
* `blue`: Số nguyên (trong khoảng 0-255) hoặc phần trăm (trong khoảng 0-100%).
* `alpha`: Số thập phân (trong khoảng 0-1) hoặc phần trăm (trong khoảng 0-100%).

Trả về: `color`

Ví dụ: `rgba(90, 129, 32, 0.5)`

Kết quả: `rgba(90, 129, 32, 0.5)`


### argb

> Định dạng màu theo dạng `#AARRGGBB` (**KHÔNG PHẢI** `#RRGGBBAA`!).

Định dạng này được sử dụng trong Internet Explorer, và trong .NET, Android.

Tham số: `color`, đối tượng màu.

Trả về: `string`

Ví dụ: `argb(rgba(90, 23, 148, 0.5));`

Kết quả: `#805a1794`


### hsl

> Tạo đối tượng màu từ các giá trị hue, saturation và lightness (HSL).

Tham số:
* `hue`: Số nguyên (trong khoảng 0-360, tương ứng với số đo góc).
* `saturation`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `lightness`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).

Trả về: `color`

Ví dụ: `hsl(90, 100%, 50%)`

Kết quả: `#80ff00`

Hàm này đặc biệt hữu dụng khi bạn muốn tạo màu dựa trên các kênh của một màu khacs, ví dụ: `@new: hsl(hue(@old), 45%, 90%);`

`@new` sẽ có giả trị hue giống với `@old`, nhưng khác giá trị saturation và lightness.


### hsla

> Tạo đối tượng màu trong suốt từ các giá trị hue, saturation, lightness và alpha (HSLA).

Tham số:
* `hue`: Số nguyên (trong khoảng 0-360, tương ứng với số đo góc).
* `saturation`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `lightness`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `alpha`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).

Trả về: `color`

Ví dụ: `hsl(90, 100%, 50%, 0.5)`

Kết quả: `rgba(128, 255, 0, 0.5)`


### hsv

> Tạo đối tượng màu từ các giá trị hue, saturation và value (HSV).

Đây là không gian màu dùng trong Photoshop, khác với không gian màu `hsl`.

Tham số:
* `hue`: Số nguyên (trong khoảng 0-360, tương ứng với số đo góc).
* `saturation`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `value`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).

Trả về: `color`

Ví dụ: `hsv(90, 100%, 50%)`

Kết quả: `#408000`


### hsva

> Tạo đối tượng màu trong suốt từ các giá trị hue, saturation, value và alpha (HSVA).

Đây là không gian màu dùng trong Photoshop, khác với không gian màu `hsla`.

Tham số:
* `hue`: Số nguyên (trong khoảng 0-360, tương ứng với số đo góc).
* `saturation`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `value`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).
* `alpha`: Phần trăm (trong khoảng 0-100%) hoặc số thập phân (trong khoảng 0-1).

Trả về: `color`

Ví dụ: `hsva(90, 100%, 50%, 0.5)`

Kết quả: `rgba(64, 128, 0, 0.5)`
