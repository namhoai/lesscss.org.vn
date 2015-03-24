Cảm ơn bạn vì đã nghĩ đến chuyện góp sức xây dựng less. Vui lòng đọc [hướng dẫn đóng góp]({{ less.master }}CONTRIBUTING.md) cẩn thận để tránh lãng phí công sức.

## Cài đặt những công cụ sau

* **node** - <http://nodejs.org/>
* **phantomjs** - <http://phantomjs.org/download.html>

hãy gõ lệnh `node -v` và `phantomjs -v` từ môi trường dòng lệnh để đảm bảo rằng bạn đã cài đặt đúng các đường dẫn.

* clone repo less.js về máy
* tại repo less.js tại máy bạn, gõ lệnh `npm install` để cài đặt các gói cần thiết
* nếu trước đây như bạn chưa sử dụng grunt, bạn cần cài "grunt" bằng lệnh `npm instal grunt-cli -g`

## Sử dụng

Tại thư mục gốc của repo less tại máy bạn, gõ lệnh `grunt test` để chạy tất cả các test. Gõ `grunt browsertest` để chạy riêng những test liên quan đến trình duyệt. Gõ lệnh `node bin/lessc duong/dan/den/file.less` để thử dịch một file bằng phiên bản less hiện tại.

Để debug các test liên quan đến trình duyệt, gõ lệnh `grunt browsertest-server`, sau đó dùng trình duyệt mở http://localhost:8088/tmp/browser/.

Không bắt buộc: Gõ lệnh `npm -g install less` để cài phiên bản less mới nhất.

Sau khi cài less, bạn có thể gõ `lessc file.less` để dịch file.less và in kết quả ra stdout, từ đó so sánh kết quả với phiên bản chạy ở máy bạn (`node bin/lessc file.less`).

Các lệnh grunt khác

* `grunt benchmark` - chạy các test đo hiệu năng
* `grunt stable` - tạo bản release mới
* `grunt readme` - tạo file readme.md mới tại thư mục gốc (sau khi release)

## Chạy less trên các môi trường khác

Trong folder libs, bạn sẽ thấy các folder `less`, `less-node`, `less-browser`. Folder less chỉ chứa javascript mã nguồn và không phụ thuộc vào môi trường. Require `less/libs/less` sẽ trả về một function nhận vào tham số là biến môi trường và mảng các trình quản lý file. Các trình quản lý file này có thể là các plugin.

```js
var createLess = require("less/libs/less"),
    myLess = createLess(environment, [myFileManager]);
```

API môi trường được viết trong [less/libs/less/environment/environment-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/environment-api.js) và API trình quản lý file được viết trong [less/libs/less/environment/file-manager-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/file-manager-api.js).

Với các trình quản lý file, chúng tôi khuyến nghị việc sử dụng new AbstractFileManager làm prototype. Với cách làm đó, bạn có thể tùy ý override, và chúng tôi có thể thêm function mới mà không làm hỏng các trình quản lý file đã có. Để có cái nhìn thực tế về trình quản lý file, bạn có thể xem 2 bản node, bản cho trình duyệt hoặc bản cho plugin import npm.

## Hướng dẫn

[http://www.gliffy.com/go/publish/4784259](http://www.gliffy.com/go/publish/4784259), đây là sơ đồ biểu diễn thiết kế của less. Lưu ý! Sơ đồ này cần được cập nhật với những thay đổi ở v2.


## Sách

* [Less Web Development Essentials](http://www.packtpub.com/less-web-development-essentials/book), by Bass Jobsen, Foreword by Alexis Sellier
* [Less Web Development Cookbook](https://www.packtpub.com/web-development/less-web-development-cookbook), by Bass Jobsen and Amin Meyghani, Foreword by Luke Page
