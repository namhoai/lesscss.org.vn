---
title: Các trình duyệt được hỗ trợ
---

Less chỉ hỗ trợ khi chạy trên các trình duyệt hiện đại (các phiên bản gần đây của Chrome, Firefox, Safari and IE). Chúng tôi không khuyến khích sử dụng Less phía client khi phát hành - vì nó sẽ làm giảm hiệu năng của người dùng và họ sẽ thấy một khoảng thời gian trễ (thậm chí kể cả là 1 giây) khi Less được dịch thành CSS, và có thể gây ra lỗi nếu như có lỗi của Javascript.

Lưu ý rằng PhantomJS hiện tại không thực thi `Function.prototype.bind`, vì thế bạn sẽ cần thêm bán vá es-5 cho chức năng này để chạy dưới PhantomJS (Chúng tôi sử dụng PhantomJS để kiểm thử và chúng tôi đã gắn thêm es5-shim để có thể làm được điều đó).

Cũng có những lý do để sử dụng Less phía client khi phát hành, chẳng hạn như nếu bạn muốn cho phép người dùng tùy chỉnh được biến số mà từ đó tác động đến sự thay đổi của theme và bạn muốn cho người dùng thấy được điều đó ở thời gian thực - trong trường hợp này người dùng không cần phải chờ đợi style được cập nhật trước khi nhìn thấy những thay đổi.

Nếu như bạn muốn sử dụng less trên các trình duyệt cũ, hãy sử dụng [es-5 shim](https://github.com/kriskowal/es5-shim) để thêm các tính năng javascript mà less yêu cầu.

Ngoài ra, nếu như bạn sử dụng các tùy chọn như là các thuộc tính trên script hoặc các thẻ link, bạn sẽ cần trình duyệt hỗ trợ `JSON.parse` hoặc  một phương án dự phòng tương ứng.
