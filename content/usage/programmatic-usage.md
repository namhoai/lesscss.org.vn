---
title: Sử dụng Less trong code
---

Điểm mở chính kết nối vào less là function less.render. Nó có dạng như sau:

```
less.render(lessInput, options)
    .then(function(output) {
        // output.css = string of css
        // output.map = string of sourcemap
        // output.imports = array of string filenames of the imports referenced
    },
    function(error) {
    });

// or...

less.render(css, options, function(error, output) {})
```

Các tham số tùy chọn là tùy ý. Nếu như bạn cung cấp 1 callback thì một promise sẽ không được trả về, ngược lại promise sẽ được trả vế.
Thật ra, phiên bản của callback được sử dụng để less có thể được sử dụng một cách đồng bộ.

Nếu như bạn muốn render một tệp tin, thì trước hết bạn phải đọc nó vào một chuỗi (để truyền vào less.render) và sau đó thiết lập trường tên tệp tin trên các tùy chọn để có được tên của tệp tin chính. Less sẽ xử lý toàn bộ quá trình import.

Tùy chọn `sourceMap` là một đối tượng cho phép bạn thiết lập các tùy chọn sourcemap con. Các tùy chọn con gồm có: `sourceMapURL`,`sourceMapBasepath`,`sourceMapRootpath`,`outputSourceFiles` và `sourceMapFileInline`. Lưu ý rằng tùy chọn `sourceMap` không sẵn có cho less.js trên các trình dịch của trình duyêt hiện nay.

```
less.render(lessInput)
    .then(function(output) {
        // output.css = string of css
        // output.map = undefined
}
//,
less.render(lessInput, {sourceMap: {}})
    .then(function(output) {
        // output.css = string of css
        // output.map = string of sourcemap
}
//or,
less.render(lessInput, {sourceMap: {sourceMapFileInline: true}})
    .then(function(output) {
        // output.css = string of css \n /*# sourceMappingURL=data:application/json;base64,eyJ2ZXJ..= */
        // output.map = undefined
}
```

Trước đây, chúng tối cũng đã khuyên bạn nên tạo một less.Parser và sau đó gọi toCSS trên kết quả trả về. Tuy nhiên việc này gặp phải 2 trở ngại rất nghiêm trọng - thứ nhất đó là bộ phân tách của chúng tôi thực chất bị ràng buộc vào toàn bộ mã less và trở ngại thứ 2 là lời gọi đến toCSS phải đồng bộ.

Bạn có thể có được cây phân tách less, nhưng sẽ mất khá nhiều bước. Bạn có thể tham khảo cách làm [trong function render](https://github.com/less/less.js/blob/master/lib/less/render.js) nhưng chúng tôi *sẽ không* sẽ không hỗ trợ sử dụng less theo cách này và có thể sẽ thay đổi chức năng này trong một phiên bản nhỏ (chúng tôi sẽ không phá vỡ nó trong các bản vá).

### Truy cập vào log

Bạn có thể thêm một bộ nghe log (log listener) với đoạn mã sau đây:

```
less.logger.addListener({
    debug: function(msg) {
    },
    info: function(msg) {
    },
    warn: function(msg) {
    },
    error: function(msg) {
    }
});
```

Lưu ý: Toàn bộ các function là tùy ý. Một lỗi sẽ không được log lại, nhưng sẽ được truyền ngược lại vào callback hoặc promise trong less.render
