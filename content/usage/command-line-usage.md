---
title: Sử dụng dòng lệnh
---

> Dịch các tệp tin `.less` thành `.css` sử dụng dòng lệnh

<span class="warning">Lưu ý, nếu như bạn không thành thạo sử dụng dòng lệnh, hãy sử dụng [GUIs cho Less](#guis-for-less).</span>

### Cài đặt lessc để sử dụng toàn cục

Cài đặt bằng [npm](https://www.npmjs.org/)

```bash
npm install less -g
```

và sau đó bạn sẽ có thể sử dụng lệnh `lessc` ở bất kỳ nơi đâu bạn muốn. Đối với một phiên bản cụ thể (hoặc thẻ) bạn có thể thêm `@VERSION` vào sau tên gói của chúng tôi, Ví dụ: `npm install less@1.6.2 -g`.

### Cài đặt cho việc phát triển node

Ngoài ra, nếu như bạn không sử dụng trình dịch một cách toàn cục, bạn có thể sử dụng:

```bash
npm i less --save-dev
```

Dòng lệnh này sẽ cài đặt phiên bản chính thức mới nhất của lessc trong thư mục chứa dự án của bạn, cũng như là thêm nó vào `devDependencies` trong nội dung tệp tin `package.json` trong dự án của bạn.

Lưu ý rằng một [khoảng phiên bản chứa dấu ngã][] sẽ tự động được chỉ rõ trong `package.json`. Việc này sẽ rất có ích vì những bản vá lỗi của phiên bản mới nhất sẽ được tự động cài đặt bởi npm.

#### Các phiên bản Beta của lessc

Theo định kỳ, khi một tính năng mới được phát triển, lessc sẽ công bố trên npm, và được đánh dấu là phiên bản beta. Tuy nhiên phiên bản này _không_ không được công bố như là bản phát hành chính thức `@latest`, và sẽ vẫn có "beta" trong tên phiên bản (hãy sử dụng `lessc -v` để biết phiên bản hiện tại).

Vì các bản vá lỗi là không thể phá vỡ nên chúng tôi sẽ công bố các bản vá lỗi ngay tức thò và các phiên bản alpha/beta/candidate sẽ được công bố như là phiên bản cập nhật trực tiếp (minor) hoặc chủ yếu (major) (Chúng tôi đã cố gằng từ phiên bản 1.4.0 để làm theo việc [đánh dấu phiên bản dạng ngữ nghĩa](http://semver.org/)).

#### Cài đặt một phiên bản đang phát triển chưa được công bố của lessc

Nếu như bạn muốn cài đặt một phiên bản đang phát triển, chưa được công bố của lessc, hãy làm theo những chỉ dẫn sau để chỉ rõ một [URL git như một sự phụ thuộc][] và phải chắc chắn chỉ rõ một commit SHA thực sự (không phải một tên của nhánh) theo dạng `commit-ish`. Việc này đảm bảo cho dự án của bạn luôn sử dụng phiên bản chính xác của lessc.

URL git có thể trực tiếp dẫn đến repo chính thức của lessc hoặc một fork.


[khoảng phiên ản có dấu ngã]: https://www.npmjs.org/doc/misc/semver.html#Ranges
[URL git như một sự phụ thuộc]: https://npmjs.org/doc/json.html#Git-URLs-as-Dependencies

### Cách sử dụng dòng lệnh phía server

Mã nhị phân đã được bao gồm trong repository này, `bin/lessc` hoạt động với [Node.js](http://nodejs.org/) trên *nix, OSX và Windows.

**Cách sử dụng**: `lessc [option option=parameter ...] <source> [destination]`

### Sử dụng dòng lệnh

```bash
lessc [option option=parameter ...] <source> [destination]
```

Nếu như source là `-' (dấu gạch ngang), thì đầu vào sẽ được đọc từ stdin.

#### Các ví dụ

```bash
# dịch bootstrap.less thành bootstrap.css
$ lessc bootstrap.less bootstrap.css

# dịch bootstrap.less thành bootstrap.css và sau đó nén kết quả
$ lessc -x bootstrap.less bootstrap.css
```

### Các tùy chọn

#### Trợ giúp

```bash
lessc --help
lessc --h
```

Hiển thị tin nhắn trợ giúp với các tùy chọn sẵn có và thoát.

#### Các đường dẫn

```bash
lessc --include-path=PATH1;PATH2
```

Thiết lập các đường dẫn có sẵn được phân tách bởi dấu ':' hoặc ';' trên Windows.

Sử dụng lệnh này để cấu hình danh sách các đường dẫn mà less sẽ sử dụng để tìm kiếm các import trong đó. Bạn có thể sử dụng lệnh này để chỉ rõ một đường dẫn tới một thư viện mà bạn muốn tham chiếu một cách đơn giản và tương đối trong các tệp tin less.

Trong node, thiết lập một tùy chọn đường dẫn như sau:
```js
{ paths: ['PATH1', 'PATH2']  }
```

#### Tạo tệp tin

```bash
lessc -M
lessc --depends
```

#### Không màu sắc

```bash
lessc --no-color
```

#### Không tương thích với IE

```bash
lessc --no-ie-compat
```

Hiện tại chỉ sử dụng cho chức năng data-uri để đảm bảo các hình ảnh không bị tạo ra với dung lượng quá lớn so với mức mà trình duyệt có thể xử lý được.

#### Vô hiệu hóa JavaScript

```bash
lessc --no-js
```

#### Lint

```bash
lessc --lint
lessc --l
```

Chạy bộ phân tách less và chỉ thông báo lỗi khi không có đầu ra.

#### Im lặng

```bash
lessc -s
lessc --silent
```

Vô hiệu hóa việc hiển thị các cảnh báo.

#### Import chặt chẽ

```bash
lessc --strict-imports
```

#### Cho phép các import từ các host https không an toàn

```bash
lessc --insecure
```

#### Phiên bản

```bash
lessc -v
lessc --version
```

#### Nén

```bash
lessc -x
lessc --compress
```

Nén sử dụng phương pháp nén được tích hợp sẵn của Less. Phương pháp này hoạt động tốt, nhưng chưa tận dụng hết các thủ thuật nén CSS. Hãy tùy ý cải tiến phương pháp nén của chúng tôi bằng một request pull.

#### Dọn dẹp rác CSS

Trong các phiên bản v2 của less, Clean CSS không còn được tích hợp như là một dependency trực tiếp. Để sử dụng clean css với lessc, hãy tham khảo [plugin dọn dẹp css](https://github.com/less/less-plugin-clean-css).

#### Tên tệp tin trong đầu ra của Source Map

```bash
lessc --source-map
lessc --source-map=file.map
```

Yêu cầu less tạo ra sourcemap. Nếu bạn sử dụng tùy chọn sourcemap mà không cung cấp tên tệp tin, dòng lệnh sẽ sử dụng tên tệp tin less nguồn nhưng với phần mở rộng map.

#### Đường dẫn gốc của Source Map

```bash
lessc --source-map-rootpath=dev-files/
```

Chỉ rõ một đường dẫn gốc (thường là đường dẫn liền trước đường dẫn của mỗi tệp tin less trong sourcemap và cũng có thể liền trước đường dẫn tới tệp tin map được chỉ rõ trong CSS đầu ra).

Vì đường dẫn cơ sở mặc định được dẫn đến thư mục chứa tệp tin less đầu vào, nên đường dẫn gốc mặc định sẽ là đường dẫn từ tệp tin đầu ra của sourcemap tới thư mục cơ sở chứa tệp tin less đầu vào.

Sử dụng tùy chọn này nếu như bạn có một tệp tin CSS được sinh ra bởi root trên web server của bạn nhưng không có các tệp tin less/css/map nguồn trong một thư mục khác. Vì vậy đối với tùy chọn bên trên, có thể bạn cần:

```bash
output.css
dev-files/output.map
dev-files/main.less
```

#### Đường dẫn cơ sở Source Map

```bash
lessc --source-map-basepath=less-files/
```

Tùy chọn này ngược lại với tùy chọn đường dẫn gốc (rootpath), nó chỉ rõ một đường dẫn sẽ được xóa bỏ khỏi các đường dẫn đầu ra. Chẳng hạn nếu như bạn đang dịch một tệp tin trong thư mục chưa các tệp tin less nhưng các tệp tin nguồn đã có sẵn trên web server của bạn trong thư mục gốc hoặc thư mục hiện tại của bạn, bạn có thể chỉ rõ điều này bằng cách xóa bỏ phần `less-files` trong đường dẫn.

Nó mặc định là đường dẫn tới tệp tin less đầu vào.

#### Source Map Less Inline

```bash
lessc --source-map-less-inline
```

Tùy chọn này chỉ rõ rằng chúng ta nên thêm toàn bộ các tệp tin Less vào sourcemap. Điều đó có nghĩa là, bạn chỉ cần tệp tin map của bạn để truy xuất tới tệp tin nguồn của bạn.

Tùy chọn này có thể được sử dụng cùng với tùy chọn map inline để bạn không cần có bất kỳ tệp tin bên ngoài nào cả.

#### Source Map Map Inline

```bash
lessc --source-map-map-inline
```

Tùy chọn này chỉ rõ rằng tệp tin map nên được đặt trên cùng một dòng trong CSS đầu ra. Việc này không khuyến khích đối với khi phát hành, nhưng đối với giai đoạn phát triển nó cho phép trình dịch tạo ra một tệp tin đầu ra riêng lẻ mà trình duyệt hỗ trợ, sử dụng mã CSS đã đươc dịch nhưng hiển thị mã nguồn less chưa được dịch.

#### Source Map URL

```bash
lessc --source-map-url=../my-map.json
```

Cho phép bạn ghi đè URL trong CSS trỏ đến tệp tin map. Tùy chọn này thường được sử dụng trong trường hợp tùy chọn đường dẫn gốc (rootpath) và đường dẫn cơ sở (basepath) không tạo ra chính xác nhưng gì bạn cần.

#### Đường dẫn gốc

```bash
lessc -rp=resources/
lessc --rootpath=resources/
```

Cho phép bạn thêm một đường dẫn vào tất cả các import được sinh ra cũng như là url trong CSS của bạn. Nó không ảnh hưởng tới các câu lệnh import trong less đã được xử lý mà chỉ ảnh hưởng tới các câu lệnh import trong tệp tin CSS đầu ra.

Chẳng hạn, nếu như toàn bộ hình ảnh mà CSS sử dụng đều ở trong một thư mục được gọi là tài nguyên (resources), bạn có thể sử dụng tùy chọn này để có được tên của thư mục đã được cấu hình.

#### Các URL tương đối

```bash
lessc -ru
lessc --relative-urls
```

Mặc định, các URL được giữ nguyên, vì thế nếu như bạn import một tệp tin trong một thư mục con tham chiếu đến một hình ảnh thì URL đó sẽ được giữ nguyên trong CSS đầu ra. Tùy chọn này cho phép bạn thay đổi URL trong tệp tin được import để URL luôn luôn ở dạng tương đối với tệp tin được import. Ví dụ:

```less
# main.less
@import "files/backgrounds.less";
# files/backgrounds.less
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

Ví dụ trên sẽ cho kết quả đầu ra như sau:

```css
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

Nhưng với tùy chọn này, kết quả đầu ra sẽ là:

```css
.icon-1 {
  background-image: url('files/images/lamp-post.png');
}
```

Bạn có thể cân nhắc sử dụng chức năng data-uri thay vì tùy chọn này (chức năng cho phép nhúng hình ảnh vào CSS)

#### Strict Math

```bash
lessc -sm=on
lessc --strict-math=on
```

Mặc định, tùy chọn này không được kích hoạt.

Nếu như tùy chọn này không được kích hoạt, Less sẽ cố gắng và xử lý toàn bộ các phép toán trong CSS của bạn. Ví dụ:

```less
.class {
  height: calc(100% - 10px);
}
```

Sẽ được xử lý như bình thường.

Nếu như tùy chọn này được kích hoạt, chỉ có những phép toán mà các dấu ngoặc không cần thiết nằm bên trong mới được xử lý. Ví dụ:

```less
.class {
  width: calc(100% - (10px  - 5px));
  height: (100px / 4px);
  font-size: 1 / 4;
}
```

```css
.class {
  width: calc(100% - 5px);
  height: 25px;
  font-size: 1 / 4;
}
```

Lúc đầu chúng tôi dự kiến để mặc định là tùy chọn này được kích hoạt sẵn, nhưng nó là một tùy chọn gây tranh cãi và chúng tôi đang cân nhắc có xử lý vấn đề này theo hướng phù hợp, hoặc less sẽ có các exception cho các trường hợp kiểu như `/` là đúng hoặc calc được sử dụng.

#### Các đơn vị chặt chẽ 

```bash
lessc -su=on
lessc --strict-units=on
```

Mặc đinh, tùy chọn này không được kích hoạt.

Nếu tùy chọn này không được kích hoạt, less sẽ cố gắng để đoán đơn vị đầu ra khi thực hiện phép toán. Ví dụ:

```less
.class {
  property: 1px * 2px;
}
```

Trong trường hợp này, mọi thứ rõ ràng là không đúng - chiều dài nhân chiều rộng thì bằng diện tích, nhưng CSS không hỗ trợ việc chỉ rõ diện tích. Vì thế chúng tôi giả định một trong các giá trị là giá trị thực sự, không phải là một đơn vị của chiều dài và chúng tôi cho ra kết quả là `2px`.

Nếu tùy chọn này được kích hoạt, chúng tôi giả định đây là lỗi trong khi tính toán và sẽ báo lỗi ở kết quả đầu ra.

#### Biến số toàn cục

```bash
lessc --global-var="my-background=red"
```

Tùy chọn này cho phép định nghĩa một biến số và biến số này có thể được tham chiếu tới bời một tệp tin. Tốt hơn hết, việc khai báo nên được đặt ở phía trên cùng của tệp tin Less cơ sở để có thể sử dụng nó hoặc ghi đè nếu như biến số này được định nghĩa bên trong tệp tin.

#### Thay đổi biến số

```bash
lessc --modify-var="my-background=red"
```

Trái ngược với tùy chọn biến số toàn cục, tùy chọn này đặt việc khai báo ở phía dưới cùng của tệp tin cơ sở của bạn, có nghĩa là nó sẽ ghi đè toàn bộ những lần định nghĩa trước đó của biến số đó trong tệp tin.

#### Các tham số của URL

```bash
lessc --url-args="cache726357"
```

Tùy chọn này cho phép bạn chỉ rõ một tham số trên các URL. Chẳng hạn, nó có thể được sử dụng để tăng tốc độ cache.

#### Số lượng dòng

```bash
lessc --line-numbers=comments
lessc --line-numbers=mediaquery
lessc --line-numbers=all
```

Tùy chọn này sinh ra source-mapping dạng inline. Đây là tùy chọn duy nhất mà trước khi trình duyệt bắt đầu hỗ trợ sourcemap. Chúng tôi đang cân nhắc loại bỏ nó, vì vậy hãy liên hệ với chúng tôi nếu như bạn thực sự muốn sử dụng tùy chọn này ở đâu đó.

#### Plugin

```bash
lessc --clean-css
lessc --plugin=clean-css="advanced"
```

--plugin Load một plugin. Bạn cũng có thể không sử dụng --plugin= nếu như plugin bắt đầu 
less-plugin. Ví dụ: Plugin dọn dẹp CSS được gọi là less-plugin-clean-css
khi nó đã được cài đặt (npm install less-plugin-clean-css), sử dụng với
--plugin=less-plugin-clean-css hoặc just --clean-css
để chỉ rõ các tùy chọn theo sau. Ví dụ: --plugin=less-plugin-clean-css="advanced"
or --clean-css="advanced"
