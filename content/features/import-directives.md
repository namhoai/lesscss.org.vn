> Nhập style từ các file style sheet khác

Trong CSS chuẩn, luật `@import` phải khai báo trước tất cả các luật khác. Nhưng Less.js không quan tâm đến việc bạn đặt câu lệnh `@import` ở đâu.

Ví dụ:

```less
.foo {
  background: #900;
}
@import "this-is-valid.less";
```

## Đuôi file
Câu lệnh `@import` sẽ được Less diễn giải khác nhau tùy theo đuôi file:

* Tên file có đuôi `.css` sẽ được hiểu như CSS và lệnh `@import` sẽ được để nguyên không dịch (tham khảm [tùy chọn trực tiếp](#import-options-inline) bên dưới).
* Tên file có đuôi khác sẽ được hiểu như Less và sẽ được nhập.
* Tên file không có đuôi, Less sẽ mặc định hiểu là file `.less` và sẽ nhập file dạng less

Ví dụ:

```less
@import "foo";      // nhập foo.less
@import "foo.less"; // nhập foo.less
@import "foo.php";  // nhập foo.php và dịch như file less
@import "foo.css";  // để nguyên, không dịch
```

Các tùy chọn sau có thể được sử dụng để thay đổi hành vi mặc định trên.

# Tùy chọn nhập
> Less hỗ trợ rất nhiều đuôi file với câu lệnh CSS `@import`, nhằm tăng tính linh hoạt trong việc nhập file ngoài.

Cú pháp: `@import (tu-khoa) "ten-file";`

Less hiện đã hỗ trợ các chỉ thị import sau:

* `reference`: sử dụng một file Less nhưng không in ra
* `inline`: in ra nội dung file đó nhưng không xử lý
* `less`: xử lý như file Less, bất kể đuôi file như thế nào
* `css`: xử lý như file CSS, bất kể đuổi file như thế nào
* `once`: chỉ nhập một lần (hành vi mặc định)
* `multiple`: nhập nhiều lần
* `optional`: tiếp tục dịch kể cả khi file đó không tìm thấy

> Less cho phép sử dụng nhiều hơn một từ khóa trong câu lệnh `@import`, phân cách nhau bằng dấu phẩy:

Ví dụ: `@import (optional, reference) "foo.less";`

## reference

> Sử dụng `@import (reference)` để nhập file ngoài, nhưng không in ra nội dung ở đầu ra CSS, trừ khi được tham chiếu.

Có từ phiên bản [v1.5.0]({{ less.master }}CHANGELOG.md)

Ví dụ: `@import (reference) "foo.less";`

`reference` là một trong những tính năng mạnh nhất của ngôn ngữ Less. Hãy thử tưởng tượng rằng `reference` đánh dấu tất cả các chỉ thị và selector với một _cờ tham chiếu_ trong file đươcj nhập, sau đó nhập bình thường, nhưng khi sinh CSS, các selector "tham chiếu" (và tất cả các media query chỉ chứa các selector tham chiếu) được lược bỏ. Các style `reference` sẽ không xuất hiện trong CSS được sinh ra, trừ khi các style tham chiếu được sử dụng như [mixins](#mixins-feature) hoặc [extended](#extend-feature).

Ngoài ra, **`reference`** tạo ra các kết quả khác nhau với mixin và extend:

* **[extend](#extend-feature)**: When a selector is extended, only the new selector is marked as _not referenced_, and it is pulled in at the position of the reference `@import` statement.
* **[mixins](#mixins-feature)**: When a `reference` style is used as an [implicit mixin](#mixins-feature), its rules are mixed-in, marked "not reference", and appear in the referenced place as normal.

* **[extend](#extend-feature)**: Khi một selector được mở rộng, chỉ có selector mới được đánh dấu là _không tham chiếu_, và sẽ được in ra ở vị trí câu lệnh `@import`
* **[mixins](#mixins-feature)**: Khi một style `reference` được sử dụng như một [mixin ngầm](#mixins-feature), các luật của nó được trộn vào, được đánh dấu là "không tham chiếu", và xuất hiện ở vị trí tham chiếu như thường.


### ví dụ về reference
Với reference, bạn có thể chỉ sử dụngnhững style mong muốn trong một thư viên như [Bootstrap](https://github.com/twbs/bootstrap) bằng cách làm như sau:

```less
.navbar:extend(.navbar all) {}
```

Và sẽ chỉ những style liên quan đến `.navbar` được in ra trong file CSS sinh bởi Less.


## inline
> Sử dụng `@import (inline)` để nhập những file ngoài, nhưng không xử lý chúng.

Có từ phiên bản [v1.5.0]({{ less.master }}CHANGELOG.md)

Ví dụ: `@import (inline) "not-less-compatible.css";`

Less hỗ trợ hầu hết các chuẩn CSS, nhưng không hỗ trợ comment ở một số chỗ và không hỗ trợ tất cả các `CSS hacks` mà không phải thay đổi CSS. Vậy nên bạn sẽ muốn sử dụng từ khóa inline này khi file CSS không tương thích với Less

Bạn có thể sử dụng tùy chọn này để nhập các file vào để chỉ cần có một file CSS ở đầu ra.


## less
> Sử dụng `@import (less)` để nhập các file theo dạng Less, bất kể đuôi file.

Có từ phiên bản [v1.4.0]({{ less.master }}CHANGELOG.md)

Ví dụ:

```less
@import (less) "foo.css";
```


## css
> Sử dụng `@import (css)` để nhập các file theo dạng CSS thông thường, bất kể đuôi file. Less sẽ để nguyên câu lệnh import và không xử lý.

Có từ phiên bản [v1.4.0]({{ less.master }}CHANGELOG.md)

Ví dụ:

```less
@import (css) "foo.less";
```
Kết quả:

```less
@import "foo.less";
```


## once
> Hành vi mặc định của câu lệnh `@import`. File đó sẽ được nhập duy nhất một lần, và các lệnh nhập sau sẽ bị bỏ qua.

Có từ phiên bản [v1.4.0]({{ less.master }}CHANGELOG.md)

Đây là hành vi mặc định của các câu lệnh `@import`.

Ví dụ:

```less
@import (once) "foo.less";
@import (once) "foo.less"; // lệnh nhập này sẽ bị bỏ qua
```


## multiple
> Sử dụng `@import (multiple)` để nhập nhiều lần một file. Đây là hành vi ngược lại với `once`.

Có từ phiên bản [v1.4.0]({{ less.master }}CHANGELOG.md)

Ví dụ:

```less
// file: foo.less
.a {
  color: green;
}
// file: main.less
@import (multiple) "foo.less";
@import (multiple) "foo.less";
```
Kết quả:

```less
.a {
  color: green;
}
.a {
  color: green;
}
```

## optional
> Sử dụng `@import (optional)` để nhập các file khi nó tồn tại. Nếu không có từ khóa `optional`, Less sẽ tung ra lỗi FileError và sẽ dừng quá trình dịch khi nhập một file không tồn tại.

Có từ phiên bản [v2.3.0]({{ less.master }}CHANGELOG.md)
