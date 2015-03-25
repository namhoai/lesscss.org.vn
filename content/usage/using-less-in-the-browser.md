---
title: Sử dụng Less trong trình duỵệt
---

Chúng tôi khuyên bạn chỉ nên sử dụng less trong trình duyệt khi phát triển hoặc khi bạn cần dịch less động và không thể làm thế trên server.
Bởi vì less là một file có kích thước khá lớn và quá trình dịch less trước khi người dùng có thể nhìn thấy kết quả sẽ tốn rất nhiều thời gian. Thêm vào đó,
quá trình dịch trên các thiết bị di động còn chậm hơn thế nữa. Khi phát triển, bạn hãy cân nhắc sử dụng công cụ theo dõi (watcher) và live reload (có thể chạy bằng grunt hoặc gulp) sẽ phù hợp hơn.

Để sử dụng less trong trình duyệt, điều đầu tiên là bạn phải tích hợp mã less.

```html
<!-- Trong trường hợp này, bạn có thẻ tích hợp bất kỳ plugin less nào, bất kỳ shim của các trình duyệt yêu cầu và tùy ý thiết lập less = bất kỳ tùy chọn nào  -->
<script src="less.js"></script>
```

Đoạn mã sau đây sẽ tìm kiếm bất kỳ thẻ less style nào trên trang này:

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

và tạo ra các thẻ style với mã css đã được dịch một cách đồng bộ.

### Các tùy chọn thiết lập

Bạn cũng có thể thiết lập các tùy chọn một cách lập trình hóa (programmatically), bằng cách thiết lập chúng trên một đối tượng less trước thẻ script sẽ tác động đến toàn bộ các thẻ link khởi tạo và việc sử dụng less một cách lập trình hóa (programmatic).

```html
<script>
  less = {
    env: "development"
  };
</script>
<script src="less.js"></script>
```

Ngoài ra, có một cách khác nữa là chỉ rõ các tùy chọn trên các thẻ script. Ví dụ:

```html
<script>
  less = {
    env: "development"
  };
</script>
<script src="less.js" data-env="development"></script>
```

Và bạn cũng có thể làm như thế này đối với các thẻ link để ghi đè các các thiết lập (một số các thiết lập của less toàn cục như verbose không thể bị ghi đè).

```html
<link data-dump-line-numbers="all" data-global-vars='{ "myvar": "#ddffee", "mystr": "\"quoted\"" }' rel="stylesheet/less" type="text/css" href="less/styles.less">
```

Một số điểm quan trọng đối với các tùy chọn thuộc tính gồm có..

 - Mức độ quan trọng: window.less < script tag < link tag
 - Tên của các thuộc tính dữ liệu không phải ở dạng camelCase (Ví dụ: logLevel -> data-log-level)
 - Các tùy chọn thẻ link chỉ sinh ra các tùy chọn thời gian (Ví dụ: verbose, logLevel ... không được hỗ trợ)
 - Giá trị của các thuộc tính dữ liệu không phải là chuỗi phải ở dạng đúng của JSON (Ví dụ: Sử dụng dấu ngoặc kép thay vì ngoặc đơn như sau `data-global-vars='{ "myvar": "#ddffee", "mystr": "\"quoted\"" }'`)

### Chế độ theo dõi (Watch mode)
Để kích hoạt chế độ theo dõi (Watch mode), tùy chọn `env` phải được thiết lập `development`. Và SAU KHI file less.js được tích hợp, hãy gọi `less.watch()`, như sau:

```html
<script>less = { env: 'development'};</script>
<script src="less.js"></script>
<script>less.watch();</script>
```

Ngoài ra, bạn có thể kích hoạt chế độ theo dõi một cách tạm thời bằng cách thêm `#!watch` vào sau URL.

### Chỉnh sửa biến số
Kích hoạt tính năng cho phép sửa đổi các biến số Less trong thời gian chạy (run-time). Khi được gọi với một giá trị mới, file Less sẽ được dịch lại mà không cần phải tải lại. Cách sử dụng đơn giản:

```js
less.modifyVars({
  '@buttonFace': '#5B83AD',
  '@buttonText': '#D9EEF2'
});
```

### Debug
Bạn có thể sinh ra các rule trong CSS của bạn cho phép các công cụ xác định nguồn của các rule đó.

Ngoài ra, bạn cũng có thể chỉ rõ tùy chọn `dumpLineNumbers` giống như trên hoặc thêm `!dumpLineNumbers:mediaquery` vào url.

Bạn có thể sử dụng tùy chọn `comments` với công cụ [FireLESS](https://addons.mozilla.org/en-us/firefox/addon/fireless/) và tùy chọn `mediaquery` option công cụ phát triển FireBug/Chrome (tương tự như dạng debug media query của SCSS).

### Các tùy chọn

Thiết lập các tùy chọn trên đối tượng `less` toàn cục **trước khi** tải script less.js:

``` html
<!-- thiết lập các tùy chọn trước script less.js -->
<script>
  less = {
    env: "development",
    logLevel: 2,
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    globalVars: {
      var1: '"string value"',
      var2: 'regular value'
    },
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```

#### async
Kiểu dữ liệu: `Boolean`
Giá trị mặc định: `false`

Sử dụng tùy chọn async với request các file import hoặc không. Hãy tham khảo [fileAsync](#using-less-in-the-browser-fileasync).

#### dumpLineNumbers
Kiểu dữ liệu: `String`
Các giá trị: `''`| `'comments'`|`'mediaquery'`|`'all'`
Giá trị mặc định: `''`

Khi thiết lập, tùy chọn này sẽ thêm thông tin dòng ở file nguồn trong file css đầu ra. Việc này giúp bạn debug được nguồn gốc của một rule nào đó.

Giá trị `comments` được sử dụng cho nội dung mà người dùng có thể hiểu được ở đầu ra, trong khi đó giá trị `mediaquery` sử dụng cho các extension của firefox để phân tách mã css và lấy thông tin.

Trong tương lai chúng tôi hy vọng tùy chọn này sẽ được thay thế bằng sourcemaps.

#### env
Kiểu dữ liệu: `String`
Giá trị mặc định: phụ thuộc vào URL của trang

Môi trường chạy có thể là `development` hoặc `production`.

Ở môi trường production, css của bạn được cache trong kho lưu trữ cục bộ và các thông báo không được in ra console.

Nếu như URL của trang bắt đầu bằng `file://` hoặc URL đó ở trên máy tính cá nhân của bạn (local machine) hoặc có cổng kết nối không phải ở dạng chuẩn, giá trị của tùy chọn này sẽ tự động được thiết lập `development`.

Ví dụ:
```js
less = { env: 'production' };
```

#### errorReporting
Kiểu dữ liệu: `String`

Các tùy chọn: `html`|`console`|`function`

Giá trị mặc định: `html`

Thiết lập phương thức thông báo lỗi khi quá trình dịch gặp lỗi.

#### fileAsync
Kiểu dữ liệu: `Boolean`

Giá trị mặc định: `false`

Request import một cách không đồng bộ trong một trang với một giao thức file.

#### functions
Kiểu dữ liệu: `object`

Các function của người dùng, được xác định bằng tên.

Ví dụ:
```js
less = {
    functions: {
        myfunc: function() {
            return new(less.tree.Dimension)(1);
        }
    }
};
```

và nó cũng có thể được sử dụng như function thuần túy trong Less. Ví dụ:

```less
.my-class {
  border-width: unit(myfunc(), px);
}
```

#### logLevel
Kiểu dữ liệu: `Number`

Giá trị mặc định: 2

Số lượng log trong console của javascript. Lưu ý rằng: Nếu bạn đang trong môi trường `production` bạn sẽ không thể thấy được bất kỳ log nào.

```bash
2 - Lỗi và nội dung lỗi
1 - Lỗi (Không có thông tin)
0 - Không có gì
```

#### poll
Kiểu dữ liệu: `Integer`

Giá trị mặc định: `1000`

Lượng thời gian (tính bằng mili giây) giữa những lần poll trong chế độ theo dõi (watch mode).

### relativeUrls
Kiểu dữ liệu: `Boolean`

Giá trị mặc định: `false`

Tùy ý điều chỉnh URL về dạng tương đối. Nếu giá trị là false thì có nghĩa là URL đang ở dạng tương đối với toàn bộ file less.

#### globalVars
Kiểu dữ liệu: `Object`

Giá trị mặc định: `undefined`

Danh sách các biến số toàn cục được thêm vào code. Khóa của các đối tượng là tên của các biến số, giá trị của các đối tượng cũng sẽ là giá trị của biến số. Các biến số dạng "chuỗi" phải được thêm quote một cách rõ ràng nếu cần thiết.

Ví dụ:

```js
less.globalVars = { myvar: "#ddffee", mystr: "\"quoted\"" };
```

Tùy chọn này định nghĩa một biến số có thể được tham chiếu đến từ một file. Để hiệu quả nhất, việc khai báo nên đặt ở phía trên cùng của file Less cơ sở, điều đó có nghĩa là nó có thể được sử dụng nhưng cũng có thể bị ghi đè nếu như biến số này được định nghĩa trong file đó.

#### modifyVars
Kiểu dữ liệu: `Object`

Giá trị mặc định: `undefined`

Có cùng format với [globalVars](#using-less-in-the-browser-globalvars).

Ngược lại với tùy chọn [globalVars](#using-less-in-the-browser-globalvars), tùy chọn này đặt việc khai báo ở phía dưới cùng của file Less cơ sở, điều đó có nghĩa là nó sẽ ghi đè toàn bộ những lần được định nghĩa trước đó trong file.

#### rootpath
Kiểu dữ liệu: `String`

Giá trị mặc định: `false`

Một đường dẫn được dùng để thêm vào điểm bắt đầu của các URL resource.

#### useFileCache
Kiểu dữ liệu: `Boolean`

Giá trị mặc định: `true` (trước đó là `false` trong các phiên bản cũ hơn phiên bản v2)

Được dùng để chỉ rõ việc có sử dụng session file cache hay không. Tùy chọn này cache các file less để bạn có thể gọi modifyVars và nó sẽ không truy xuất toàn bộ các file less một lần nữa.
Nếu như bạn sử dụng công cụ theo dõi (watcher) hoặc gọi refresh với tùy chọn reload được thiết lập là true, thì cache sẽ được làm sạch trước khi chạy.
