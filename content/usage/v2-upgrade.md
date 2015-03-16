---
title: Hướng dẫn nâng cấp lên phiên bản V2
---

Các thay đổi của ngôn ngữ
----------------

Màu sắc sẽ được giữ nguyên trong kết quả trả về, vì thế `purple` sẽ vẫn là `purple` và nó sẽ không bị chuyển đổi thành mã hexa.

Sử dụng dòng lệnh
------------------

### Clean CSS

Chúng tôi đã xóa bỏ dependency trên clean css và chuyển nó tới [plugin](https://github.com/less/less-plugin-clean-css).
Việc này cho phép chúng tôi 1. Cập nhật dependency và tích hợp mà không cần đến một bản phát hành của less 2. Không ràng buộc những nguời dùng (người mà không sử dụng clean css) vào việc phải tải xuống bằng npm.

Cách sử dụng vẫn tương tự, bạn chỉ việc cài đặt plugin (`npm install -g less-plugin-clean-css`) và sau đó có thể sử dụng bằng tham số 
`--clean-css`.

```bash
# cũ
lessc --clean-css --clean-option=--compatibility:ie8 --clean-option=--advanced
# mới
lessc --clean-css="--compatibility=ie8 --advanced"
```

### Sourcemaps

Chúng tôi đã cải tiến các tùy chọn sourcemap và việc sinh ra đường dẫn để sourcemap có thể được tạo ra tại đúng đường dẫn mà không phải chỉ rõ các tùy chọn.

Sử dụng chương trình
------------------

Chúng tôi đã loại bỏ việc sử dụng less.Parser và toCss để sinh ra mã css. Để thay thế, chúng tôi khuyên bạn nên sử dụng `less.render`.
Hãy tham khảo [Sử dụng chương trình](#programmatic-usage) để biết thêm thông tin chi tiết.

Hơn thế nữa, thay vì việc trả về kết quả là 1 chuỗi css, chúng tôi trả về một đối tượng với trường `css` có giá trị là 1 chuỗi và một trường  `map` được thiết lập giá trị là sourcemap (nếu được áp dụng).

Các tùy chọn sourcemap lúc này được thiết lập trên sourceMap thay vì trực tiếp trên các tùy chọn. Do đó, thay vì `options.sourceMapFullFilename = ` bạn sẽ sử dụng `options.sourceMap = { sourceMapFullFilename: `.

Sử dụng trình duyêt
-------------

Việc sử dụng trinh duyệt không thay đổi quá nhiều. Các tùy chọn thiết lập trên đối tượng `less` được tìm thấy trên `less.options` sau khi mã less chạy thay vì "làm ô nhiễm" `less`.

Bạn cũng có thể chỉ rõ các tùy chọn trên script và các thẻ less để đơn giản hóa các thiết lập của tùy chọn trên trình duyệt. Hãy tham khảo phần sử dụng trình duyệt để biết thêm thông tin chi tiết.
