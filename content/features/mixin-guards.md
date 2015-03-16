> Mixin có điều kiện

Chắn thường được sử dụng khi bạn muốn so khớp _biểu thức_ thay vì so khớp những giá trị đơn giản hay số lượng tham số. Nếu bạn đã quen với lập trình hàm thì có thể bạn cũng từng gặp chắn.

Với cố gắng giữ cú pháp gần gũi với CSS chuẩn, Less đã chọn cú pháp điều kiện dạng **mixin có chắn** thay vì các lệnh `if`/`else`, bắt chước theo cú pháp của `@media` query trong chuẩn CSS.

Hãy cùng bắt đầu với ví dụ sau:

```less
.mixin (@a) when (lightness(@a) >= 50%) {
  background-color: black;
}
.mixin (@a) when (lightness(@a) < 50%) {
  background-color: white;
}
.mixin (@a) {
  color: @a;
}
```

Điểm mấu chốt ở đây là từ khóa `when`, theo sau là một chuỗi điều kiện chắn (ở đây chỉ có một chắn). Nếu ta viết như sau:

```less
.class1 { .mixin(#ddd) }
.class2 { .mixin(#555) }
```

Sẽ được kết quả:

```css
.class1 {
  background-color: black;
  color: #ddd;
}
.class2 {
  background-color: white;
  color: #555;
}
```

### Toán tử so sánh chắn

Các toán tử so sánh dùng được trong điều kiện chắn gồm có `>`, `>=`, `=`, `=<`, `<`. Ngoài ra, từ khóa `true` là giá trị đúng duy nhất, và như vậy hai mixin sau giống hệt nhau:

```less
.truth (@a) when (@a) { ... }
.truth (@a) when (@a = true) { ... }
```

Các giá trị khác ngoài `true` đều là phủ định:

```less
.class {
  .truth(40); // Không khớp với khai báo nào ở trên
}
```

Lưu ý rằng bạn cũng có thể so sánh các tham số với nhau, hoặc với một giá trị:

```less
@media: mobile;

.mixin (@a) when (@media = mobile) { ... }
.mixin (@a) when (@media = desktop) { ... }

.max (@a; @b) when (@a > @b) { width: @a }
.max (@a; @b) when (@a < @b) { width: @b }
```

### Toán tử logic trong điều kiện chắn

Bạn có thể sử dụng toán tử logic trong điều kiện chắn với cú pháp giống như media query của CSS.

Sử dụng từ khóa `and` để kết hợp các điều kiện chắn:

```less
.mixin (@a) when (isnumber(@a)) and (@a > 0) { ... }
```

Bạn có thể dùng `,` phân cách các điều kiện chắn thay cho toán tử *or*. Chỉ một điều kiện chắn đúng sẽ dẫn đến đúng toàn bộ:

```less
.mixin (@a) when (@a > 10), (@a < -10) { ... }
```

Use the `not` keyword to negate conditions:
Sử dụng từ khóa `not` để phủ định điều kiện:

```less
.mixin (@b) when not (@b > 0) { ... }
```

### Hàm kiểm tra kiểu

Cuối cùng, nếu bạn muốn khớp mixin dựa trên kiểu dữ lieeuj, bạn có thể sử dụng hàm `is`:

```less
.mixin (@a; @b: 0) when (isnumber(@b)) { ... }
.mixin (@a; @b: black) when (iscolor(@b)) { ... }
```

Dưới đây là những hàm kiểm tra kiểu cơ bản:

* `iscolor`
* `isnumber`
* `isstring`
* `iskeyword`
* `isurl`

Các hàm dưới đây kiểm tra đơn vị của giá trị:

* `ispixel`
* `ispercentage`
* `isem`
* `isunit`

### Mixin có điều kiện

_(**FIXME**)_ Additionally, the `default` function may be used to make a mixin match depending on other mixing matches, and you may use it to create "conditional mixins" similar to `else` or `default` statements (of `if` and `case` structures respectively):

```less
.mixin (@a) when (@a > 0) { ...  }
.mixin (@a) when (default()) { ... } // chỉ khớp khi mixin đầu tiên không khớp, ví dụ khi @a <= 0
```
