> "if" với selector

Có từ phiên bản [v1.5.0]({{ less.master }}CHANGELOG.md)

Chắn còn được áp dụng vào các selector css, thuận tiện cho việc tạo và gọi mixin tức thì.

Ví dụ, trước phiên bản 1.5.0, bạn có thể phải viết như sau:

```less
.my-optional-style() when (@my-option = true) {
  button {
    color: white;
  }
}
.my-optional-style();
```

Giờ đây, bạn có thể áp dụng trực tiếp chắn lên một style.

```less
button when (@my-option = true) {
  color: white;
}
```

Bạn cũng có thể tạo ra một mệnh đề `if` bằng cách kết hợp chắn với `&`, cho phép bạn gom nhóm nhiều chắn.
```less
& when (@my-option = true) {
  button {
    color: white;
  }
  a {
    color: blue;
  }
}
```
