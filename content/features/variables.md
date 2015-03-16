---
title: Biến số
---

> Bộ điều khiển sử dụng chung các giá trị trong cùng một địa điểm.

## Tổng quan

Chúng ta có thể nhiều lần trông thấy các giá trị được lặp đi lặp lại trong stylesheet:

```css
a,
.link {
  color: #428bca;
}
.widget {
  color: #fff;
  background: #428bca;
}
```

Biến số giúp bạn dễ dàng kiểm soát các giá trị này, từ đó giúp cho mã nguồn của bạn dễ bảo trì hơn:

```less
// Khai báo biến
@link-color:        #428bca; // xanh nước biển
@link-color-hover:  darken(@link-color, 10%);

// Sử dụng
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```

## Biến số nội suy

Ví dụ bên trên chú trọng vào việc sử dụng biến số để kiểm soát _các giá trị trong các quy tắc CSS_, nhưng ngoài ra, chúng cũng có thể được sử dụng ở những nơi khác nữa, chẳng hạn như tên của các selector, tên của các thuộc tính, URL và các câu lệnh `@import`.


### Selector

Phiên bản: 1.4.0

```less
// Khai báo biến
@mySelector: banner;

// Sử dụng
.@{mySelector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```
Được dịch thành:

```css
.banner {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

### URL

```less
// Khai báo biến
@images: "../img";

// Sử dụng
body {
  color: #444;
  background: url("@{images}/white-sand.png");
}
```

### Các câu lệnh Import

Phiên bản: 1.4.0

Cú pháp: `@import "@{themes}/tidal-wave.less";`

Lưu ý rằng trong các phiên bản cũ hơn phiên bản v2.0.0, chỉ có các biến số được khai báo trong root hoặc trong phạm vi hiện tại mới có thể sử dụng và chỉ có tệp tin hiện tại và các tệp tin được gọi đến mới được sử dụng để tìm kiếm biến số.

Ví dụ:

```less
// Khai báo biến
@themes: "../../src/themes";

// Sử dụng
@import "@{themes}/tidal-wave.less";
```

### Các thuộc tính

Phiên bản: 1.6.0

```less
@property: color;

.widget {
  @{property}: #0ee;
  background-@{property}: #999;
}
```

Được dịch thành:

```css
.widget {
  color: #0ee;
  background-color: #999;
}
```

## Tên của biến số

Hoàn toàn có thể định nghĩa biến số với một cái tên:

```less
@fnord:  "I am fnord.";
@var:    "fnord";
content: @@var;
```

Sẽ được dịch thành:

```
content: "I am fnord.";
```

## Lazy Loading

> Các biến số có thể lazy load và không nhất thiết phải được khai báo trước khi sử dụng.

Hãy xem đoạn mã Less hợp lệ sau đây:

```less
.lazy-eval {
  width: @var;
}

@var: @a;
@a: 9%;
```
Và đây cũng là một đoạn mã Less hợp lệ khác:

```less
.lazy-eval-scope {
  width: @var;
  @a: 9%;
}

@var: @a;
@a: 100%;
```
Và cả hai đều sẽ được dịch thành:

```css
.lazy-eval-scope {
  width: 9%;
}
```

Khi bạn định nghĩa một biến số nhiều lần thì biến số trong lần định nghĩa cuối cùng sẽ được sử dụng (biến số được tìm kiếm trong phạm vi hiện tại theo hướng từ dưới lên). Điều này rất giống với CSS nơi mà thuộc tính cuối cùng trong một lần định nghĩa được sử dụng để xác định giá trị.

Ví dụ:

```less
@var: 0;
.class {
  @var: 1;
  .brass {
    @var: 2;
    three: @var;
    @var: 3;
  }
  one: @var;
}
```
Sẽ được dịch thành:

```css
.class {
  one: 1;
}
.class .brass {
  three: 3;
}
```

## biến số mặc định

Đôi khi chúng ta có nhu cầu sử dụng các biến số mặc định - một khái niệm cho phép thiết lập giá trị của biến số nếu như nó chưa được tạo ra trước đó. Tính năng này không nhất thiết phải sử dụng vì lý do bạn có thể dễ dàng ghi đè một biến số bằng cách định nghĩa về sau đó.

Ví dụ:

```less
// Giả sử đoạn code này được khai báo trong thư viện
@base-color: green;
@dark-color: darken(@base-color, 10%);

// Và đây là đoạn code khi sử dụng thư viện trên
@import "library.less";
@base-color: red;
```

Ví dụ này vẫn sẽ hoạt động bởi [Lazy Loading](#variables-feature-lazy-loading) - base-color đã được ghi đè và dark-color sẽ là màu đỏ tối.
