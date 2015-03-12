---
title: Tổng quan về các tính năng
---

> Giống như một phần mở rộng của CSS, Less không chỉ tương thích ngược với CSS mà các tính năng của Less cũng đều sử dụng cú pháp sẵn có của CSS. Điều này giúp cho việc học Less trở nên dễ dàng hơn bao giờ hết.


### Biến số

Hãy xem ví dụ đơn giản sau đây:

```less
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header {
  color: @light-blue;
}
```

Sau khi biên dịch:

```css
#header {
  color: #6c94be;
}
```

Hãy chú ý rằng các biến số thực sự là "hằng số" bởi chúng chỉ có thể được định nghĩa một lần duy nhất.


### Mixins

Mixins thực chất là việc tích hợp ("mixing in") một tập hợp các thuộc tính từ một rule-set vào một rule-set khác. Giả sử chúng ta có class sau đây:

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

Và chúng ta muốn sử dụng những thuộc tính này vào bên trong các rule-set khác. Để thực hiện điều đó, chúng ta chỉ việc thêm tên của class đó và nơi mà ta muốn sử dụng các thuộc tính của nó, như sau:

```less
#menu a {
  color: #111;
  .bordered;
}

.post a {
  color: red;
  .bordered;
}
```

Các thuộc tính của class `.bordered` lúc này sẽ xuất hiện trong cả `#menu a` và `.post a`. (Lưu ý rằng bạn cũng có thể sử dụng `#ids` như là mixins.)

**Tham khảo**

* [Tham khảo về mixins](#mixins-feature)
* [Mixins dạng tham số](#mixins-parametric-feature)


### Các quy tắc lồng nhau

Less cho phép bạn sử dụng quy tắc lồng nhau thay vì hoặc kết hợp với phân tầng (cascading). Giả sử chúng ta có đoạn mã CSS sau:

```css
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

Trong Less, chúng ta có thể viết như sau:

```less
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```

Kết quả của 2 đoạn code trên là như nhau, và đều mô phỏng cấu trúc HTML của bạn.

Bạn cũng có thể kết hợp pseudo-selectors với các mixin của bạn bằng cách sử dụng phương pháp này. Sau đây là đoạn mã hack clearfix cổ điển, được viết lại bằng cách sử dụng mixin (`&` đại diện cho selector cha hiện tại):

```less
.clearfix {
  display: block;
  zoom: 1;

  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```

**Tham khảo**

* [Selector cha](#parent-selectors-feature)

### Bong bóng media query và các media query lồng nhau

Các media query có thể lồng nhau giống như các selector. Các selector được copy sang phần nội dung của media query:

```less
.screencolor {
  @media screen {
    color: green;
    @media (min-width: 768px) {
      color: red;
    }
  }
  @media tv {
    color: black;
  }
}

```
được dịch ra:

```css
@media screen {
  .screencolor {
    color: green;
  }
}
@media screen and (min-width: 768px) {
  .screencolor {
    color: red;
  }
}
@media tv {
  .screencolor {
    color: black;
  }
}
```

### Các phép toán

Các con số, màu sắc hoặc biến số đều có thể sử dụng để tính toán. Hãy xem các ví dụ sau đây:

```less
@base: 5%;
@filler: @base * 2;
@other: @base + @filler;

color: #888 / 4;
background-color: @base-color + #111;
height: 100% / 2 + @filler;
```

Kết quả được dịch ra sẽ giống như những gì bạn mong đợi - Less hiểu được sự khác nhau giữa màu sắc và đơn vị. Nếu một đơn vị được sử dụng trong phép toán, giống như:

```less
@var: 1px + 5;
```

Less sẽ sử dụng đơn vị đó cho kết quả cuối cùng—`6px` trong trường hợp này.

### Functions

Less cung cấp một số lượng lớn các function hỗ trợ biến đổi màu sắc, xử lý chuỗi và thực hiện tính toán. Chúng được viết chi tiết và đầy đủ trong phần tham khảo của function.

Cách sử dụng function khá rõ ràng. Ví dụ sau đây sử dụng phần trăm để chuyển đổi 0.5 thành 50%, tăng độ bão hòa của màu cơ sở lên 5% và sau đó tăng độ sáng của màu background lên 25% và xoay đi 8 độ:

```less
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```


### Namespaces and Accessors

(Đừng nhầm lẫn với [CSS `@namespace`](http://www.w3.org/TR/css3-namespace/) hoặc [namespace selectors](http://www.w3.org/TR/css3-selectors/#typenmsp)).

Đôi khi, bạn có thể muốn nhóm các mixin lại với nhau để tổ chức được tốt hơn , hoặc để việc đóng gói dễ dàng hơn. Khi đó, bạn có thể thực hiện được điều này một cách trực quan với Less, giả sử bạn muốn nhóm một số các mixin và biến số cho `#bundle`, để tái sử dụng sau này hoặc đem phân phối:

```less
#bundle {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab { ... }
  .citation { ... }
}
```

Lúc này, nếu bạn muốn mixin class `.button` vào `#header a`, ta có thể làm như sau:

```less
#header a {
  color: orange;
  #bundle > .button;
}
```

Lưu ý rằng các biến số được khai báo bên trong một namespace sẽ bị cô lập và không thể sử dụng bên ngoài phạm vi đó thông qua cú pháp tương tự mà bạn sử dụng để tham chiếu tới một mixin (`#Namespace > .mixin-name`). Vì thế, bạn không thể thực hiện việc giống như sau: (`#Namespace > @this-will-not-work`).

### Phạm vi

Khái niệm phạm vi trong Less khá giống với các ngôn ngữ lập trình khác. Đầu tiên, các biến số và mixin sẽ được tìm kiếm ở cục bộ, và nếu không tìm thấy, trình biên dịch sẽ tìm trong phạm vi cha, và cứ tiếp tục như vậy.

```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```

Các biến số và mixin không nhất thiết phải được khai báo trước khi sử dụng. Vì vậy đoạn mã Less sau đây sẽ tương tự với ví dụ phía trên:

```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```

**Tham khảo**

* [Lazy Loading](#variables-feature-lazy-loading)


### Chú thích

Cả chú thích dạng block và dạng inline đều được sử dụng:

```less
/* One hell of a block
style comment! */
@var: red;

// Get in line!
@var: white;
```

### Import

Import hoạt động khá hiệu quả. Bạn có thể import một tệp tin `.less`, và toàn bộ các biến số trong đó sẽ đều được import vào. Phần mở rộng được chỉ định một cách tùy ý cho các tệp tin `.less`.

```css
@import "library"; // library.less
@import "typo.css";
```
