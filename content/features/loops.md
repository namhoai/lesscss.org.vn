> Tạo các vòng lặp

Với Less, các mixin có thể gọi đến chính nó. Những mixin như vậy, khi kết hợp với [biểu thức chắn](#mixin-guards-feature) và [so khớp mẫu](#mixins-parametric-feature-pattern-matching), sẽ tạo thành nhiều cấu trúc lặp khác nhau.

Example:

```less
.loop(@counter) when (@counter > 0) {
  .loop((@counter - 1));    // next iteration
  width: (10px * @counter); // code for each iteration
}

div {
  .loop(5); // launch the loop
}
```

Kết quả:

```css
div {
  width: 10px;
  width: 20px;
  width: 30px;
  width: 40px;
  width: 50px;
}
```

Một ví dụ chung về cách sử dụng vòng lặp đệ quy để tạo ra class cho grid:

```less
.generate-columns(4);

.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
```

Kết quả:

```css
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
```
