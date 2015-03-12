---
title: Mở đầu
---

Less là một bộ tiền xử lý CSS, mở rộng ngôn ngữ CSS sẵn có bằng cách thêm các tính năng như cho phép đặt biến, mixins, các chức năng và nhiều kỹ thuật giúp bạn tạo ra được mã CSS có cấu trúc tốt hơn, ổn định hơn và dễ mở rộng hơn.

Less chạy bên trong Node, trong trình duyệt và bên trong Rhino. Ngoài ra có rất nhiều công cụ của bên thứ 3 cho phép bạn biên dịch các tệp tin và theo dõi các thay đổi của bạn.

Ví dụ:

```less
@base: #f938ab;

.box-shadow(@style, @c) when (iscolor(@c)) {
  -webkit-box-shadow: @style @c;
  box-shadow:         @style @c;
}
.box-shadow(@style, @alpha: 50%) when (isnumber(@alpha)) {
  .box-shadow(@style, rgba(0, 0, 0, @alpha));
}
.box {
  color: saturate(@base, 5%);
  border-color: lighten(@base, 30%);
  div { .box-shadow(0 0 5px, 30%) }
}
```

được biên dịch thành:

```css
.box {
  color: #fe33ac;
  border-color: #fdcdea;
}
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```
