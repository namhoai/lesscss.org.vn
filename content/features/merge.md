> Kết hợp các thuộc tính

Tính năng `hợp nhất` cho phép ta gộp chung giá trị từ nhiều thuộc tính vào một danh sách ngăn cách bằng dấu phẩy hoặc khoảng trống trong một thuộc tính đơn. `hợp nhất` hữu ích cho các thuộc tính như background và transform.

## Dấu phẩy

> Gắn thêm giá trị thuộc tính bằng dầu phẩy

Có từ phiên bản [v1.5.0]({{ less.master }}CHANGELOG.md)

Ví dụ:

```less
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}
```
Kết quả:

```css
.myclass {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}
```

## Khoảng trống

> Gắn thêm giá trị thuộc tính bằng khoảng trống

Có từ phiên bản [v1.7.0]({{ less.master }}CHANGELOG.md)

Ví dụ:

```less
.mixin() {
  transform+_: scale(2);
}
.myclass {
  .mixin();
  transform+_: rotate(15deg);
}
```
Kết quả:

```css
.myclass {
  transform: scale(2) rotate(15deg);
}
```

Để tránh việc gắn kết ngoài dự kiến, `hợp nhất` yêu cầu phải có chỉ báo `+` hoặc `+_` ở mỗi khai báo chưa kết thúc.
