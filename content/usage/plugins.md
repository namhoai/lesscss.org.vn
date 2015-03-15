## Làm thế nào để sử dụng plugin? - command line

Nếu bạn sử dụng lessc, điều đầu tiên cần làm là cài plugin đó. Less khuyên dùng các plugin có tên bắt đầu bằng "less-plugin", tuy nhiên không bắt buộc. Ví dụ, để cài plugin clean css, bạn cần gõ lệnh này vào command line `npm install less-plugin-clean-css`.

Để sử dụng plugin, nếu bạn truyền vào một tùy chọn được hỗ trợ trong chuẩn lessc, lessc sẽ thử load plugin với tên tương ứng, ví dụ:
```
lessc --clean-css="advanced"
```

Với lệnh trên, less sẽ load và sử dụng plugin clean css vừa được cài đặt bên trên. Bạn cũng có thể gọi plugin một cách cụ thể hơn, ví dụ:

```
lessc --plugin=path_to_plugin=options
```

## Sử dụng plugin trong code

Để sử dụngl một plugin trong Node, bạn cần truyền plugin đó vào làm một phần tử trong mảng plugins, ví dụ:

```
var myPlugin = require("my-plugin");
less.render(myCSS, { plugins: [myPlugin] })
   .then(function(output) {
    },
    function(error) {
    });
```

## Trong trình duyệt

Các plugin thường đi cùng một file javascript, để sử dụng nó bạn chỉ cần thêm file javascript này vào *trước* file less.js.

```
<script src="plugin.js"></script>
<script>
less = { 
    plugins: [plugin]
};
</script>  
<script src="less.min.js"></script>
```

## Danh sách plugin

Các plugin nổi bật
 - [Clean CSS - nén css](https://github.com/less/less-plugin-clean-css)
 - [Autoprefixer - thêm các tiền tố trình duyệt, nâng cao tính tương thích ngược cho css của bạn](https://github.com/less/less-plugin-autoprefix)
 - [Inline urls - thay các url ảnh dạng `url()` thành `data-uri()`](https://github.com/less/less-plugin-inline-urls)
 - [Group CSS Media Queries - gom nhóm các media query](https://github.com/bassjobsen/less-plugin-group-css-media-queries)
 - [CSS Wiring - nén css](https://github.com/bassjobsen/less-plugin-csswring)
 - [CSS Flip - tạo CSS cho ngôn ngữ trái-sang-phải (LTR) hoặc phải-sang-trái (RTL)](https://github.com/bassjobsen/less-plugin-css-flip)
 - [RTL - đảo ngược Less từ LTR thành RTL](https://github.com/less/less-plugin-rtl)
 - [Pleeease - bộ xử lý Less](https://github.com/bassjobsen/less-plugin-pleeease)
 - [CSScomb](https://github.com/bassjobsen/less-plugin-csscomb/)
 
Các thư viện/framework tiền xử lý:
 - [Npm Import - nhập một repo npm con](https://github.com/less/less-plugin-npm-import)
 - [Bower Resolve - nhập từ gói bower](https://github.com/Mercateo/less-plugin-bower-resolve)
 - [Bootstrap cho less.js](https://github.com/bassjobsen/less-plugin-bootstrap/)
 - [Lesshat cho less.js](https://github.com/bassjobsen/less-plugin-lesshat/)
 - [Flexbox grid từ flexboxgrid.com cho less.js](https://github.com/bassjobsen/less-plugin-flexboxgrid) 
 - [Flexible Grid System (flexible.gs) cho less.js ](https://github.com/bassjobsen/less-plugin-flexiblegs)
 - [Cardinal CSS cho less.js](https://github.com/bassjobsen/less-plugin-cardinal)
 - [Ionic cho less.js](https://github.com/bassjobsen/less-plugin-ionic)
 - [Skeleton cho less.js](https://github.com/bassjobsen/less-plugin-skeleton)

Plugin thêm function cho Less:
 - [Thêm các function xử lý ảnh nâng cao giúp tìm các màu tương phản](https://github.com/less/less-plugin-advanced-color-functions/)
 - [Function cubehelix(y,a,b,t) trả về màu giữa hai màu a và b, sử dụng giá trị hiệu chỉnh gamma băng 1](https://github.com/bassjobsen/less-plugin-cubehelix). (Dựa trên [bảng phối màu `cubehelix` của Dave Green](https://www.mrao.cam.ac.uk/~dag/CUBEHELIX/))


## Dành cho người viết plugin

Less hỗ trợ vài điểm mở cho phép các plugin gắn kết với less. Less sẽ hỗ trợ thêm một số điểm mở trong thời gian tới.

Một plugin cơ bản chỉ cần một cấu trúc đơn giản như sau:
```
{
    install: function(less, pluginManager) {
    },
    minVersion: [2, 0, 0] /* optional */
}
```
Như trên, plugin có thể sử dụng đối tưởng less (Less v2 có thêm nhiều class, thuận tiện cho việc kế thừa và mở rộng) và trình quản lý plugin (cung cấp một số hook để thêm visitor, trình quản lý file và bộ xử lý).

Nếu plugin của bạn hỗ trợ lessc, dưới đây là cấu trúc chi tiết hơn để gắn kết với lessc

```
{
    install: function(less, pluginManager) { 
    },
    setOptions: function(argumentString) { /* optional */
    },
    printUsage: function() { /* optional */
    },
    minVersion: [2, 0, 0] /* optional */
}
```
Ở đây có thêm hàm setOptions (nhận vào chuỗi người dùng nhập khi gọi plugin của bạn), và hàm printUsage sử dụng để in ra hướng dẫn về các tùy chọn và chi tiết về plugin của bạn.

Đây là một vài ví dụ về các kiểu plugin khác nhau:
bộ xử lý: https://github.com/less/less-plugin-clean-css
visitor: https://github.com/less/less-plugin-inline-urls
trình quản lý file: https://github.com/less/less-plugin-npm-import

Note: Plugins are different from creating a version of less for a different environment but they do have similarities, for example node provides 2 file managers by default and browser provides one and that is the main step in getting less to run within a specific environment. The plugin allows you to add file managers.
