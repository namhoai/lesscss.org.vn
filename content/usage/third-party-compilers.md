---
title: Trình dịch Less từ các bên thứ ba
---

## Các trình dịch Node.js

* **[grunt-contrib-less](https://github.com/gruntjs/grunt-contrib-less)**
* **[assemble-less](https://github.com/assemble/assemble-less)**: Plugin Grunt.js cung cấp đầy đủ tính năng để dịch tệp tin Less thành CSS, với các tùy chọn bổ sung cho việc duy trì các thư viện của các thành phần và theme Less. Nếu bạn là người sử dụng nâng cao, plugin này cho phép bạn định nghĩa và quản lý "các gói" hoặc "các nhóm" Less bằng cách sử dụng JSON, các template [Lo-dash](https://github.com/bestiejs/lodash)(gạch dưới)(Ví dụ: `<%= bootstrap.less %>`), và [node-glob](https://github.com/isaacs/node-glob) / [minimatch](https://github.com/isaacs/minimatch) (Ví dụ: `'../src/**/*.less"`). _assemble-less_ cũng cung cấp một số các tùy chọn bao gồm cả việc nén các tập tin CSS
* **[gulp-less](https://github.com/plus3network/gulp-less)**: Hãy lưu ý rằng plugin này đã loại bỏ các tùy chọn `source-map` và thay thế bằng thư viện [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps).
* **[RECESS](https://github.com/twitter/recess)**: Một công cụ đánh giá chất lượng mã nguồn của Twitter dành cho các tệp tin CSS được dịch từ Less. RECESS có các tùy chọn để dịch tệp tin Less thành CSS, cũng như là linting, formatting và nén các tệp tin CSS.
* **[autoless](https://github.com/jgonera/autoless)**: Một công cụ theo dõi các tệp tin Less, có chức năng truy vết phụ thuộc (bao gồm cả những thay đổi của các tệp tin được import do cập nhật) và các thông báo.
* **[Connect Middleware for Less.js](https://github.com/emberfeather/less.js-middleware)**: Kết nối Middleware để biên dịch Less


## Các công nghệ khác

**Wro4j Runner CLI**
Tải về tệp tin [wro4j-runner.jar](http://wro4j.googlecode.com/files/wro4j-runner-1.4.1-jar-with-dependencies.jar) và chạy dòng lệnh sau:

```bash
java -jar wro4j-runner-1.5.0-jar-with-dependencies.jar --preProcessors lessCss
```

Để biết thêm thông tin chi tiết, hãy tham khảo: [Wro4j Runner CLI](http://code.google.com/p/wro4j/wiki/wro4jRunner)

**CSS::LESSp**

http://search.cpan.org/~drinchev/CSS-LESSp/

```bash
lessp.pl styles.less > styles.css
```

**Windows Script Host**

Lưu ý rằng Less node phiên bản chính thức chạy trên Windows, vì thế công nghệ này có thể thực sự không cần thiết.

[Less.js cho Windows](https://github.com/duncansmart/less.js-windows) được sử dụng như sau:

```bash
cscript //nologo lessc.wsf input.less [output.css] [-compress]
```
hoặc

```bash
lessc input.less [output.css] [-compress]
```

**dotless**

[dotless cho Windows](http://www.dotlesscss.org/) được sử dụng như sau:

```bash
dotless.Compiler.exe [-switches] <inputfile> [outputfile]
```

**Bạn cũng có thể tham khảo:** 

* [Các cổng của Less](/about/#ports)
