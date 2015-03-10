> Referencing parent selectors with `&`

Toán tử `&` đại diện cho selector cha của một [luật lồng](#features-overview-feature-nested-rules) và được sử dụng nhiều nhất khi áp dụng class biến đổi hay giả-class vào selector có sẵn:

```less
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```

kết quả:

```css
a {
  color: blue;
}

a:hover {
  color: green;
}
```

Lưu ý rằng khi không có `&`, ví dụ trên sẽ thành `a :hover` (ứng với các phần tử được di chuột qua nằm trong thẻ `<a>`) và không phải là điều chúng ta thường muốn thực hiện với luật lồng `:hover`.

Toán tử "selector cha" có nhiều cách sử dụng, về cơ bản, là bất cứ khi nào bạn cần kết hợp các selector con trong luật lồng theo cách khác với cách thông thường. Ví dụ, một cách dùng  điển hình khác của `&` là tạo ra các class lặp đi lặp lại:

```less
.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
```

kết quả:

```css
.button-ok {
  background-image: url("ok.png");
}
.button-cancel {
  background-image: url("cancel.png");
}
.button-custom {
  background-image: url("custom.png");
}
```

### Nhiều `&`

Trong một selector có thể có nhiều `&`, cho phép tham chiếu đến selector cha mà không cần lặp lại tên.

```less
.link {
  & + & {
    color: red;
  }

  & & {
    color: green;
  }

  && {
    color: blue;
  }

  &, &ish {
    color: cyan;
  }
}
```

kết quả:

```css
.link + .link {
  color: red;
}
.link .link {
  color: green;
}
.link.link {
  color: blue;
}
.link, .linkish {
  color: cyan;
}
```


Lưu ý là `&` thay thế cho tất cả các selector cha (không chỉ là một selector cha gần nhất), ví dụ:

```less
.grand {
  .parent {
    & > & {
      color: red;
    }

    & & {
      color: green;
    }

    && {
      color: blue;
    }

    &, &ish {
      color: cyan;
    }
  }
}
```

Kết quả:

```css
.grand .parent > .grand .parent {
  color: red;
}
.grand .parent .grand .parent {
  color: green;
}
.grand .parent.grand .parent {
  color: blue;
}
.grand .parent,
.grand .parentish {
  color: cyan;
}
```


### Thay đổi thứ tự selector

Trong một số trường hợp, bạn có thể cần thêm một selector vào trước selector cha (selector kế thừa). Có thể thực hiện việc này bằng cách đặt `&` vào sau selector hiện tại.
Ví dụ, khi sử dụng Modernizr, bạn có thể muốn tạo ra các luật khác nhau dựa trên các tính năng được hỗ trợ bởi trình duyệt:

```less
.header {
  .menu {
    border-radius: 5px;
    .no-borderradius & {
      background-image: url('images/button-background.png');
    }
  }
}
```

Selector `.no-borderradius &` sẽ gắn `.no-borderradius` và selector cha `.header .menu`, tạo thành `.no-borderradius .header .menu`:

```css
.header .menu {
  border-radius: 5px;
}
.no-borderradius .header .menu {
  background-image: url('images/button-background.png');
}
```


### Bùng nổ tổ hợp


`&` cũng được sử dụng để tạo ra hoán vị của các cặp selector trong một danh sách (ngăn cách bằng dấu phẩy):

```less
p, a, ul, li {
  border-top: 2px dotted #366;
  & + & {
    border-top: 0;
  }
}
```

Tạo ra tất cả (16) tổ hợp của các phần tử đã định:

```css
p,
a,
ul,
li {
  border-top: 2px dotted #366;
}
p + p,
p + a,
p + ul,
p + li,
a + p,
a + a,
a + ul,
a + li,
ul + p,
ul + a,
ul + ul,
ul + li,
li + p,
li + a,
li + ul,
li + li {
  border-top: 0;
}
```
