> Các thuộc tính "mix-in" (tạm dịch: hòa trộn) từ những style sẵn có

Bạn có thể mix-in các selector dạng class và dạng id, ví dụ như sau:

```less
.a, #b {
  color: red;
}
.mixin-class {
  .a();
}
.mixin-id {
  #b();
}
```
Kết quả:
```css
.a, #b {
  color: red;
}
.mixin-class {
  color: red;
}
.mixin-id {
  color: red;
}
```

Lưu ý rằng để gọi mixin không bắt buộc phải có dấu ngoặc.

```less
.a();   //these lines do the same thing
.a;
```

## Không in ra mixin

Nếu bạn muốn tạo một mixin nhưng không muốn in mixin đó ra, bạn có thể đặt cặp dấu ngoặc đằng sau nó.

```less
.my-mixin {
  color: black;
}
.my-other-mixin() {
  background: white;
}
.class {
  .my-mixin;
  .my-other-mixin;
}
```
Kết quả

```css
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
```

## Selector trong mixin

Ngoài các thuộc tính, mixin còn có thể chứa các selector.

Ví dụ:

```less
.my-hover-mixin() {
  &:hover {
    border: 1px solid red;
  }
}
button {
  .my-hover-mixin();
}
```

Kết quả

```css
button:hover {
  border: 1px solid red;
}
```

## Namespace

Nếu bạn muốn hòa trộn các thuộc tính trong một selector phức tạp, bạn có thể chồng nhiều id hoặc class.

```less
#outer {
  .inner {
    color: red;
  }
}

.c {
  #outer > .inner;
}
```

cả `>` và khoảng trống đều là không bắt buộc

```less
// all do the same thing
#outer > .inner;
#outer > .inner();
#outer .inner;
#outer .inner();
#outer.inner;
#outer.inner();
```

Bằng cách trên, ta có thể tạo ra namespace. Bạn có thể đặt các mixin bên trong một selector dạng id và có thể yên tâm rằng chúng không xung đột với các thư viện khác.

Ví dụ:

```less
#my-library {
  .my-mixin() {
    color: black;
  }
}
// which can be used like this
.class {
  #my-library > .my-mixin();
}
```

## Từ khóa `!important`

Sử dụng từ khóa `!important` sau lệnh gọi mixin để đánh dấu tất cả các thuộc tính kế thừa là `!important`:

Ví dụ:

```less
.foo (@bg: #f5f5f5, @color: #900) {
  background: @bg;
  color: @color;
}
.unimportant {
  .foo();
}
.important {
  .foo() !important;
}
```

Kết quả:

```css
.unimportant {
  background: #f5f5f5;
  color: #900;
}
.important {
  background: #f5f5f5 !important;
  color: #900 !important;
}
```
