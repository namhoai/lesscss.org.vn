### color

> Phân tách một màu sắc, từ đó một chuỗi đại diện cho một màu sắc sẽ được chuyển thành màu sắc.

Tham số: `string`: Một chuỗi đại diện cho một màu sắc cụ thể.

Kết quả trả về: `color`

Ví dụ: `color("#aaa");`

Kết quả: `#aaa`

### image-size

> Lấy kích thước ảnh từ một tệp tin.

Tham số: `string`: Tệp tin dùng để lấy kích thước.

Kết quả trả về: `dimension`

Ví dụ: `image-size("file.png");`

Kết quả: `10px 10px`

Lưu ý: Function này cần phải được thực thi trong từng môi trường. Hiện tại function này chỉ có thể sử dụng trong môi trường node.

Được cập nhật vào phiên bản: v2.2.0

### image-width

> Lấy chiều rộng của ảnh từ một tệp tin.

Tham số: `string`: Tệp tin dùng để lấy kích thước.

Kết quả trả về: `dimension`

Ví dụ: `image-width("file.png");`

Kết quả: `10px`

Lưu ý: Function này cần phải được thực thi trong từng môi trường. Hiện tại function này chỉ có thể sử dụng trong môi trường node.

Được cập nhật vào phiên bản: v2.2.0

### image-height

> Lấy chiều cao của ảnh từ một tệp tin.

Tham số: `string`: Tệp tin dùng để lấy kích thước.

Kết quả trả về: `dimension`

Ví dụ: `image-height("file.png");`

Kết quả: `10px`

Lưu ý: Function này cần phải được thực thi trong từng môi trường. Hiện tại function này chỉ có thể sử dụng trong môi trường node.

Được cập nhật vào phiên bản: v2.2.0

### convert

> Chuyển một số từ đơn vị này sang đơn vị khác.

Tham số đầu tiên là một số đi kèm với đơn vị cần chuyển đổi, tham số thứ 2 là đơn vị sẽ chuyển đổi sang. Nếu như các đơn vị là tương đồng, việc chuyển đổi sẽ diễn ra, ngược lại tham số đầu tiên sẽ được trả về.

Hãy tham khảo phần [unit](#misc-functions-unit) để thay đổi đơn vị mà không cần chuyển đổi.

_Các nhóm đơn vị tương đồng_:

* lengths: `m`, `cm`, `mm`, `in`, `pt` and `pc`,
* time: `s` and `ms`,
* angle: `rad`, `deg`, `grad` and `turn`.

Tham số:
* `number`: Một số thực đi kèm với đơn vị.
* `identifier`, `string` or `escaped value`: đơn vị sẽ chuyển đổi sang

Kết quả trả về: `number`

Ví dụ:

```less
convert(9s, "ms")
convert(14cm, mm)
convert(8, mm) // incompatible unit types
```

Kết quả:

```
9000ms
140mm
8
```


### data-uri

> Sử dụng cú pháp dạng inline và `url()` nếu như tùy chọn ieCompat được kích hoạt và kích thước tài nguyên quá lớn, hoặc nếu như bạn sử dụng function trên trình duyệt. Nếu như kiểu MIME không được cung cấp, node sẽ sử dụng gói mime để xác định kiểu mime đúng.

Tham số:
* `mimetype`: (Tùy ý) Một chuỗi kiểu MIME.
* `url`: Đường dẫn tương đối của tệp tin

Ví dụ: `data-uri('../data/image.jpg');`

Kết quả: `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

Kết quả hiển thị trên trình duyệt: `url('../data/image.jpg');`

Ví dụ: `data-uri('image/jpeg;base64', '../data/image.jpg');`

Kết quả: `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

Ví dụ: `data-uri('image/svg+xml;charset=UTF-8', 'image.svg');`

Kết quả: `url("data:image/svg+xml;charset=UTF-8,%3Csvg%3E%3Ccircle%20r%3D%229%22%2F%3E%3C%2Fsvg%3E");`

### default

> Chỉ sẵn có trong các điều kiện gaurd và trả về `true` chỉ khi nào không có bất kỳ mixin nào tương ứng, ngược lại trả về `false`.

Ví dụ:

```less
.mixin(1)                   {x: 11}
.mixin(2)                   {y: 22}
.mixin(@x) when (default()) {z: @x}

div {
  .mixin(3);
}

div.special {
  .mixin(1);
}
```
Kết quả:

```css
div {
  z: 3;
}
div.special {
  x: 11;
}
```

Bạn cũng có thể sử dụng giá trị được trả về bởi `default` bằng cách sử dụng các phép toán gaurd. Chẳng hạn `.mixin() when not(default()) {}` sẽ chỉ có tác dụng khi mà một mixin được định nghĩa khác đã được ghép với lời gọi `.mixin()`:

```less
.mixin(@value) when (ispixel(@value)) {width: @value}
.mixin(@value) when not(default())    {padding: (@value / 5)}

div-1 {
  .mixin(100px);
}

div-2 {
  /* ... */
  .mixin(100%);
}
```
Kết quả:

```css
div-1 {
  width: 100px;
  padding: 20px;
}
div-2 {
  /* ... */
}
```

Less cho phép tạo nhiều lời gọi `default()` trong cùng một điều kiện gaurd hoặc trong các điều kiện khác nhau của mixin có cùng tên:

```less
div {
  .m(@x) when (default()), not(default())    {always: @x}
  .m(@x) when (default()) and not(default()) {never:  @x}

  .m(1); // OK
}
```
Tuy nhiên Less sẽ báo lỗi nếu như nó phát hiện ra mâu thuẫn *tiềm ẩn* giữa các mixin được định nghĩa sử dụng `default()`:

```less
div {
  .m(@x) when (default())    {}
  .m(@x) when not(default()) {}

  .m(1); // Lỗi
}
```
Trong ví dụ trên, ta hoàn toàn có thể xác định giá trị mà mỗi lời gọi `default()` trả về vì chúng phụ thuộc vào nhau một cách đệ quy.

Cách sử dụng nhiều `default()` nâng cao:

```less
.x {
  .m(red)                                    {case-1: darkred}
  .m(blue)                                   {case-2: darkblue}
  .m(@x) when (iscolor(@x)) and (default())  {default-color: @x}
  .m('foo')                                  {case-1: I am 'foo'}
  .m('bar')                                  {case-2: I am 'bar'}
  .m(@x) when (isstring(@x)) and (default()) {default-string: and I am the default}

  &-blue  {.m(blue)}
  &-green {.m(green)}
  &-foo   {.m('foo')}
  &-baz   {.m('baz')}
}
```
Kết quả:

```css
.x-blue {
  case-2: #00008b;
}
.x-green {
  default-color: #008000;
}
.x-foo {
  case-1: I am 'foo';
}
.x-baz {
  default-string: and I am the default;
}
```

Function `default` sẽ có thể sử dụng như một function được tích hợp sẵn _chỉ khi nó nằm trong các biểu thức gaurd_. Nếu như nó được sử dụng bên ngoài mixin trong điều kiện gaurd, thì nó sẽ được biên dịch giống như một giá trị CSS thông thường:

Ví dụ:

```less
div {
  foo: default();
  bar: default(42);
}
```
Kết quả:

```css
div {
  foo: default();
  bar: default(42);
}
```


### unit

> Được sử dụng để xóa bỏ hoặc thay đổi đơn vị của kích thước

Tham số:
* `dimension`: Một con số, có thể đi kèm hoặc không đi kèm đơn vị.
* `unit`: (Tùy ý) đơn vị sẽ chuyển đổi thành, nếu như không được truyền vào, function sẽ xóa bỏ phần đơn vị.

Hãy tham khảo phần [convert](#misc-functions-convert) để biết cách thay đổi đơn vị mà không cần chuyển đổi.

Ví dụ: `unit(5, px)`

Kết quả: `5px`

Ví dụ: `unit(5em)`

Kết quả: `5`



### get-unit

> Trả về các đơn vị của một số.

Nếu như tham số đầu vào là một con số đi kèm với đơn vị, thì function sẽ trả về đơn vị của nó. Ngược lại, sẽ trả về giá trị rỗng.

Tham số:
* `number`: Một số có thể đi kèm hoặc không đi kèm đơn vị

Ví dụ: `get-unit(5px)`

Kết quả: `px`

Ví dụ: `get-unit(5)`

Kết quả: ` //nothing` 



### svg-gradient

> Sử dụng để tạo ra multi-stop svg gradient.

Function svg-gradient tạo ra multi-stop svg gradient, yêu cầu phải có ít nhất 3 tham số được truyền vào. Tham số đầu tiên chỉ loại gradient và hướng và các tham số còn lại chỉ các màu sắc và vị trí tương ứng. Vị trí của màu đầu tiên và màu cuối cùng là tùy ý, các màu sắc còn lại phải có các vị trí tương ứng.

Tham số "hướng" phải là một trong số `to bottom`, `to right`, `to bottom right`, `to top right`, `ellipse` hoặc `ellipse at center`. Tham số này có thể được truyền vào dưới dạng giá trị escaped hoặc chuỗi các từ phân tách nhau bởi dấu cách.

Tham số:
* `escaped value` hoặc `list of identifiers`: hướng
* `color [percentage]`: màu sắc đầu tiên và vị trí tương đối của nó (ví trị có thể có hoặc không)
* `color percent`: (tùy ý) màu sắc thứ 2 và vị trí tương đối của nó
* ...
* `color percent`: (tùy ý) màu sắc thứ n và vị trí tương đối của nó
* `color [percentage]`: màu sắc cuối cùng và vị trí tương đối của nó (vị trí có thể có hoặc không)

Kết quả trả về: `url` cùng với "URI-Encoded" svg gradient.

Ví dụ:
````
div {
  background-image: svg-gradient(to right, red, green 30%, blue);
}
````

sẽ được dịch thành:
````
div {
  background-image: url('data:image/svg+xml,%3C%3Fxml%20version%3D%221.0%22%20%3F%3E%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20version%3D%221.1%22%20width%3D%22100%25%22%20height%3D%22100%25%22%20viewBox%3D%220%200%201%201%22%20preserveAspectRatio%3D%22none%22%3E%3ClinearGradient%20id%3D%22gradient%22%20gradientUnits%3D%22userSpaceOnUse%22%20x1%3D%220%25%22%20y1%3D%220%25%22%20x2%3D%22100%25%22%20y2%3D%220%25%22%3E%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%23ff0000%22%2F%3E%3Cstop%20offset%3D%2230%25%22%20stop-color%3D%22%23008000%22%2F%3E%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%230000ff%22%2F%3E%3C%2FlinearGradient%3E%3Crect%20x%3D%220%22%20y%3D%220%22%20width%3D%221%22%20height%3D%221%22%20fill%3D%22url(%23gradient)%22%20%2F%3E%3C%2Fsvg%3E');
}
````
Lưu ý: Đối với các phiên bản cũ hơn 2.2.0 thì kết quả trả về sẽ được mã hóa theo thuật toán `base64`.

Ảnh background được sinh ra sẽ có màu đỏ ở phía bên trái, màu xanh tại vị trí 30% chiều rộng của nó và kết thúc bằng màu xanh. Phần mã hóa theo thuật toán base64 chứa svg-gradient sau:
````xml
<?xml version="1.0" ?>
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="100%" height="100%" viewBox="0 0 1 1" preserveAspectRatio="none">
    <linearGradient id="gradient" gradientUnits="userSpaceOnUse" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="#ff0000"/>
        <stop offset="30%" stop-color="#008000"/>
        <stop offset="100%" stop-color="#0000ff"/>
    </linearGradient>
    <rect x="0" y="0" width="1" height="1" fill="url(#gradient)" />
</svg>
````

