---
title: Cách sử dụng ở phía server
---

> Less có thể được sử dụng thông qua dòng lệnh bằng npm, hoặc tải về tệp tin dưới dạng script từ trình duyệt hoặc thông qua rất nhiều các công cụ của bên thứ 3. Hãy xem phần [Sử dụng]({{resolve 'usage'}}) để biết thêm chi tiết
detailed information.

## Cách cài đặt

Cách đơn giản nhất để cài đặt Less trên server là sử dụng npm, một bộ quản lý gói của [node.js](http://nodejs.org/) như sau:

```bash
$ npm install -g less
```

## Sử dụng dòng lệnh

Sau khi cài đặt thành công, bạn có thể gọi trình biên dịch bằng dòng lệnh như sau:

```bash
$ lessc styles.less
```

Dòng lệnh trên sẽ ghi tệp tin CSS đã được biên dịch ra `stdout`, và sau đó bạn có thể chuyển hướng ra tệp tin mà bạn mong muốn như sau:

```bash
$ lessc styles.less > styles.css
```

Để ghi ra tệp tin CSS đã được nén, bạn chỉ việc truyền thêm tùy chọn `-x`. Nếu như bạn muốn sử dụng nhiều tùy chọn nén hơn,
[Clean CSS](https://github.com/GoalSmashers/clean-css) có thể giúp bạn điều đó với [plugin](https://github.com/less/less-plugin-clean-css) `--clean-css`.

Để biết toàn bộ các tùy chọn dòng lệnh khi chạy lessc ngoài các tham số, hãy xem [Cách sử dụng]({{resolve 'usage'}}).

## Cách sử dụng trong Code

Bạn có thể gọi trình biên dịch từ node như sau:

```js
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, output) {
  console.log(output.css);
});
```

Sẽ tạo ra:

```css
.class {
  width: 2;
}
```

## Cấu hình

Bạn có thể truyền một số tùy chọn vào trình biên dịch:

```js
var less = require('less');

less.render('.class { width: (1 + 1) }',
    {
      paths: ['.', './lib'],  // các thư mục để @import tìm file
      filename: 'style.less', // tên file, cho ra các báo lỗi rõ ràng hơn
      compress: true          // nén CSS
    },
    function (e, output) {
       console.log(output.css);
    });
```

Hãy xem phần [Cách sử dụng]({{resolve 'usage'}}) để biết thêm thông tin chi tiết.

## Các công cụ của bên thứ 3

Hãy xem phần [Cách sử dụng]({{resolve 'usage'}}) để biết thêm thông tin chi tiết về các công cụ.

# Dòng lệnh với Rhino
> Mỗi phiên bản less.js đều chứa một phiên bản tương thích với rhino.

Để sử dụng dòng lệnh với Rhino, yêu cầu phải có 2 tệp tin sau:
* less-rhino-<version>.js - tệp tin thực thi trình biên dịch,
* lessc-rhino-<version>.js - tệp tin hỗ trợ trình biên dịch.

Dòng lệnh để chạy trình biên dịch:
````
java -jar js.jar -f less-rhino-<version>.js lessc-rhino-<version>.js styles.less styles.css
````

Dòng lệnh này sẽ biên dịch tệp tin styles.less và lưu kết quả vào tệp tin styles.css. Bạn có thể tùy ý lựa chọn tệp tin đầu ra. Nếu như không được cung cấp, less sẽ đưa kết quả ra `stdout`.

# Cách sử dụng ở phía Client

> Sử dụng less.js trong trình duyệt được khuyến khích khi phát triển, tuy nhiên không nên sử dụng khi phát hành

Sử dụng Less ở phía Client là cách đơn giản nhất để làm quen với việc phát triển bằng Less, nhung khi phát hành, thời điểm mà hiệu năng và độ tin cậy được đặt lên hàng đầu, _bạn nên sử dụng phiên bản được biên dịch trước (pre-compiling) bởi node.js hoặc sử dụng một trong các công cụ sẵn có của bên thứ 3_ .

Để bắt đầu, hãy liên kết stylesheet `.less` vào dự án của bạn với thuộc tính `rel` được thiết lập "`stylesheet/less`":

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

Tiếp theo, [tải về less.js](https://github.com/less/less.js/archive/master.zip) và thêm nó vào thẻ `<script></script>` nằm trong thành phần `<head>` trong trang của bạn:

```html
<script src="less.js" type="text/javascript"></script>
```

### Lưu ý

* Hãy chắc chắn rằng bạn đã thêm stylesheet của bạn **vào trước** script.
* Khi bạn sử dụng nhiều stylesheet `.less` thì các tệp tin đó phải được biên dịch một cách độc lập. Khi đó các biến số, mixins hoặc namespaces mà bạn định nghĩa trong các stylesheet cũng sẽ độc lập với nhau.

## Các tùy chọn của trình duyệt

Các tùy chọn trên đối tượng `less` phải được thiết lập **trước** thẻ `<script src="less.js"></script>`:

``` html
<!-- thiếp lập less qua biến window.less trước khi load file less.js -->
<script>
  less = {
    env: "development",
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```

Hoặc ngắn gọn, chúng có thể được thiết lập như các thuộc tính trong script và các thẻ link (yêu cầu trình duyệt hỗ trợ JSON.parse hoặc polyfill).

``` html
<script src="less.js" data-poll="1000" data-relative-urls="false"></script>
<link data-dump-line-numbers="all" data-global-vars='{ myvar: "#ddffee", mystr: "\"quoted\"" }' rel="stylesheet/less" type="text/css" href="less/styles.less">
```

Hãy xem phần [Các tùy chọn của trình duyệt](usage/#using-less-in-the-browser-setting-options) để biết thêm chi tiết.
