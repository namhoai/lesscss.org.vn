> Extend là một pseudo-class của Less cho phép sử dụng kết hợp selector (nơi mà nó được sử dụng) và selector tương ứng với giá trị tham chiếu được truyền vào.

Phiên bản [v1.4.0]({{ less.master }}CHANGELOG.md)

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
```

Trong ví dụ trên, selector `:extend` sẽ áp dụng "extending selector" (`nav ul`) vào class `.inline` _bất kỳ nơi nào mà class `.inline` xuất hiện_. Block khai báo sẽ được giữ nguyên mà không có bất kỳ tham chiếu nào tới extend (vì extend không phải là CSS).

Vì thế đoạn mã sau đây:

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
.inline {
  color: red;
}
```

Sẽ được dịch thành:

```css
nav ul {
  background: blue;
}
.inline,
nav ul {
  color: red;
}
```

Hãy lưu ý cái cách mà selector `nav ul:extend(.inline)` được biên dịch thành `nav ul` - extend đã bị xóa đi trước khi dịch ra và selector block nằm phía bên trái dấu ":" được giữ nguyên (nav ul). Nếu như không có bất kỳ thuộc tính nào được sử dụng bên trong block đó thì nó sẽ bị xóa bỏ (mặc dù extend vẫn ảnh hưởng đến các selector khác).

## Cú pháp của extend
Extend có thể được sử dụng gắn với 1 selector cụ thể hoặc được đặt trong một ruleset (Giống như một pseudo-class với một tham số selector tùy ý được theo sau bởi từ khóa `all`):

Ví dụ:

```less
.a:extend(.b) {}

// tương đương với
.a {
  &:extend(.b);
}
```

```less
.c:extend(.d all) {
  // extend tất cả các selector có chứa ".d", ví dụ ".x.d" hoặc ".d.x"
}
.c:extend(.d) {
  // chỉ extend các selector có chứa ".d"
}
```

Bạn có thể truyền vào nhiều class để thực hiện extend, các class được phân cách với nhau bằng dấu phẩy.

Ví dụ:

```less
.e:extend(.f) {}
.e:extend(.g) {}

// tương đương với
.e:extend(.f, .g) {}
```

### Extend gắn với selector
Extend gắn với selector giống như một pseudo-class thông thường với tham số truyền vào là một selector. Một selector có thể có nhiều class extend và toàn bộ các class này phải nằm ở vị trí cuối cùng của selector.

* Extend theo sau selector: `pre:hover:extend(div pre)`.
* Cho phép sử dụng dấu cách giữa selector và extend: `pre:hover :extend(div pre)`.
* Cho phép sử dụng nhiều extend đồng thời: `pre:hover:extend(div pre):extend(.bucket tr)` (Tương tự như `pre:hover:extend(div pre, .bucket tr)`)
* Không cho phép: `pre:hover:extend(div pre).nth-child(odd)`. Extend phải nằm ở vị trí cuối cùng.

Nếu như một ruleset chứa nhiều selector thì mỗi selector đều có thể có riêng một extend. Các selector cùng với extend phải nằm trong cùng một ruleset:

```less
.big-division,
.big-bag:extend(.bag),
.big-bucket:extend(.bucket) {
  // body
}
```

### Extend nằm trong ruleset
Extend có thể được đặt trong phần nội dụng của ruleset bằng cách sử dụng cú pháp `&:extend(selector)`. Việc đặt extend bên trong nội dung của ruleset giống cho một cách viết ngắn gọn cho việc áp dụng nó vào từng selector của ruleset.


Ví dụ:

```less
pre:hover,
.some-class {
  &:extend(div pre);
}
```

sẽ tương tự như:

```less
pre:hover:extend(div pre),
.some-class:extend(div pre) {}
```

### Sử dụng selector dạng lồng nhau khi extend
Có thể sử dụng selector dạng lồng nhau với extend như ví dụ sau đây:

Ví dụ:

```less
.bucket {
  tr { // ruleset mức trong
    color: blue;
  }
}
.some-class:extend(.bucket tr) {} // sử dụng ruleset mức trong
```
sẽ được dịch thành:

```css
.bucket tr,
.some-class {
  color: blue;
}
```

Hơn nữa, extend nhận diện được selector dạng lồng nhau trong mã CSS đã biên dịch chứ không phải trong mã Less gốc. Hãy xem ví dụ sau đây:

Ví dụ:

```less
.bucket {
  tr & { // ruleset mức trong
    color: blue;
  }
}
.some-class:extend(tr .bucket) {} // sử dụng ruleset mức trong
```

sẽ được dịch thành:

```css
tr .bucket,
.some-class {
  color: blue;
}
```


### Tìm kiếm chính xác với Extend
Theo mặc định Extend sẽ tìm kiếm selector chính xác nhất trong số các selector, phụ thuộc vào việc selector có sử dụng ký tự "*" phía trước hay không. Việc tìm kiếm cũng không phụ thuộc vào việc 2 biểu thức dạng nth- có cùng ý nghĩa, chỉ cần chùng có cùng định dạng khi tìm kiếm. Ngoại trừ dấu ngoặc(", ') nằm bên trong thuộc tính của selector (ví dụ: input[type="text"]), less hiểu được rằng chúng có cùng ý nghĩa và chọn chúng.

Ví dụ:

```less
.a.class,
.class.a,
.class > .a {
  color: blue;
}
.test:extend(.class) {} // KHÔNG khớp với selector nào bên trên
```

Phụ thuộc vào ký tự "*". Selector `*.class` và `.class` là tương đương, tuy nhiên extend hiểu chúng khác nhau:

```less
*.class {
  color: blue;
}
.noStar:extend(.class) {} // // KHÔNG khớp selector *.class
```

sẽ được dịch thành:

```css
*.class {
  color: blue;
}
```

Phụ thuộc vào thứ tự của các pseudo-class. Selector `link:hover:visited` và `link:visited:hover` đều tương ứng với một tập hợp các phần tử, tuy nhiên extend hiểu chúng khác nhau:

```less
link:hover:visited {
  color: blue;
}
.selector:extend(link:visited:hover) {}
```
sẽ được dịch thành:

```css
link:hover:visited {
  color: blue;
}
```

### biểu thức dạng nth

Không phụ thuộc vào biểu thức dạng Nth. Biểu thức `1n+3` và `n+3` là tương đương, tuy nhiên extend hiểu chúng khác nhau:

```less
:nth-child(1n+3) {
  color: blue;
}
.child:extend(:nth-child(n+3)) {}
```
sẽ được dịch thành:

```css
:nth-child(1n+3) {
  color: blue;
}
```

Không phụ thuộc vào dấu quote (",') trong selector. Các trường hợp sau đây là tương đương.

```less
[title=identifier] {
  color: blue;
}
[title='identifier'] {
  color: blue;
}
[title="identifier"] {
  color: blue;
}

.noQuote:extend([title=identifier]) {}
.singleQuote:extend([title='identifier']) {}
.doubleQuote:extend([title="identifier"]) {}
```
sẽ được dịch thành:

```css
[title=identifier],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title='identifier'],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title="identifier"],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}
```

## Extend "toàn bộ"

Khi bạn sử dụng từ khóa "all" vào cuối cùng trong danh sách các tham số truyền vào extend, thì khi đó Less sẽ hiểu selector đó như một phần của một selector khác. Selector đó sẽ được copy và phần tương ứng với selector sẽ được thay thế bằng selector được extend để tạo ra một selector mới.

Ví dụ:

```less
.a.b.test,
.test.c {
  color: orange;
}
.test {
  &:hover {
    color: green;
  }
}

.replacement:extend(.test all) {}
```

sẽ được dịch ra thành:

```css
.a.b.test,
.test.c,
.a.b.replacement,
.replacement.c {
  color: orange;
}
.test:hover,
.replacement:hover {
  color: green;
}
```

_Bạn có thể nghĩ cơ chế này giống như việc tìm kiếm và thay thế không hoàn toàn_


### Selector dạng nội suy và Extend
> Selector với các biến số không thể sử dụng với extend. Nếu một selector chứa biến số, extend sẽ bỏ qua nó.

Đã có một yêu cầu về vấn đề này nhưng việc thay đổi là không hề dễ dàng. Tuy nhiên, extend lại có thể sử dụng với selector dạng nội suy

Selector chứa biến số sẽ bị bỏ qua:

```less
@variable: .bucket;
@{variable} { // selector nội suy, sẽ in ra .bucket { ... }
  color: blue;
}
.some-class:extend(.bucket) {} // KHÔNG khớp với selector trên
```

và extend với tham số được truyền vào là biến số sẽ không thể sử dụng:

```less
.bucket {
  color: blue;
}
.some-class:extend(@{variable}) {} // KHÔNG khớp với selector trên
@variable: .bucket;
```

Cả hai ví dụ trên được dịch thành:

```less
.bucket {
  color: blue;
}
```

Tuy nhiên, `:extend` sử dụng với selector dạng nội suy lại được chấp nhận:

```less
.bucket {
  color: blue;
}
@{variable}:extend(.bucket) {}
@variable: .selector;
```

đoạn mã less trên được dịch thành:

```less
.bucket, .selector {
  color: blue;
}
```

## Scoping / Extend bên trong @media

Extend được viết bên trong phần khai báo của media sẽ chỉ có thể sử dụng với các selector nằm trong phần khai báo của media đó:

```less
@media print {
  .screenClass:extend(.selector) {} // extend bên trong media
  .selector { // trong cùng một media, khớp với lệnh extend
    color: black;
  }
}
.selector { // ruleset ở ngoài media - không extend
  color: red;
}
@media screen {
  .selector {  // ruleset ở trong media query khác - không extend
    color: blue;
  }
}
```

sẽ được dịch thành:

```css
@media print {
  .selector,
  .screenClass { /*  ruleset trong cùng media sẽ được extend */
    color: black;
  }
}
.selector { /* ruleset ở ngoài media sẽ không extend */
  color: red;
}
@media screen {
  .selector { /* ruleset ở trong media khác sẽ không extend */
    color: blue;
  }
}
```

Extend được viết bên trong phần khai báo của media sẽ không thể sử dụng với các selector của các media mức trong:

```less
@media screen {
  .screenClass:extend(.selector) {} // extend bên trong media
  @media (min-width: 1023px) {
    .selector {  // ruleset ở media mức trong - không extend
      color: blue;
    }
  }
}
```

được dịch thành:

```css
@media screen and (min-width: 1023px) {
  .selector { /* ruleset ở media mức trong - không extend */
    color: blue;
  }
}
```

Extend sẽ kết hợp với toàn bộ các selector tìm kiếm được bao gồm cả các selector nằm bên trong media mức trong:

```less
@media screen {
  .selector {  /* ruleset ở media mức trong - khớp với extend ở mức ngoài cùng */
    color: blue;
  }
  @media (min-width: 1023px) {
    .selector {  /* ruleset ở media mức trong - khớp với extend ở mức ngoài cùng */
      color: blue;
    }
  }
}

.topLevel:extend(.selector) {} /* extend mức ngoài cùng khớp với tất cả các selector trên */
```

sẽ được dịch thành:

```css
@media screen {
  .selector,
  .topLevel { /* ruleset trong media được extend */
    color: blue;
  }
}
@media screen and (min-width: 1023px) {
  .selector,
  .topLevel { /* ruleset ở media mức trong được extend */
    color: blue;
  }
}
```

### Phát hiện kép

Thực tế thì không có tồn tại phát hiện kép.

Ví dụ:

```less
.alert-info,
.widget {
  /* khai báo */
}

.alert:extend(.alert-info, .widget) {}
```
sẽ được dịch thành:

```css
.alert-info,
.widget,
.alert,
.alert {
  /* khai báo */
}
```

## Các Use Case cho Extend

### Use Case cổ điển

Use case dạng cổ điển được sử dụng để tránh việc thêm class cơ sở. Ví dụ, nếu như bạn có:

```css
.animal {
  background-color: black;
  color: white;
}
```

và bạn muốn có một biến thể của animal được tạo ra bằng cách ghi đè background color thì bạn có 2 lựa chọn, đầu tiên hãy thay đổi mã HTML của bạn:

```html
<a class="animal bear">Bear</a>
```
```css
.animal {
  background-color: black;
  color: white;
}
.bear {
  background-color: brown;
}
```

hoặc đơn giản hóa mã html và sử dụng extend trong mã less của bạn. Ví dụ:

```html
<a class="bear">Bear</a>
```

```less
.animal {
  background-color: black;
  color: white;
}
.bear {
  &:extend(.animal);
  background-color: brown;
}
```

### Giảm thiểu kích thước của mã CSS

Mixin copy toàn bộ các thuộc tính vào bên trong một selector, điều đó có thể sẽ dẫn đến việc lặp lại một cách không cần thiết. Vì thế bạn có thể sử dụng extend thay vì mixin để di chuyển selector lên phía trên. Xem ví dụ bên dưới:

Ví dụ - sử dụng mixin:

```less
.my-inline-block() {
    display: inline-block;
  font-size: 0;
}
.thing1 {
  .my-inline-block;
}
.thing2 {
  .my-inline-block;
}
```

sẽ được dịch thành:

```css
.thing1 {
  display: inline-block;
  font-size: 0;
}
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

Ví dụ - sử dụng extend:

```less
.my-inline-block {
  display: inline-block;
  font-size: 0;
}
.thing1 {
  &:extend(.my-inline-block);
}
.thing2 {
  &:extend(.my-inline-block);
}
```

sẽ được dịch thành:

```css
.my-inline-block,
.thing1,
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

### Style kết hợp / mixin dạng nâng cao

Một use-case khác cũng được sử dụng để thay thế cho mixin khi cần thiết - vì mixin chỉ có thể sử dụng với các selector đơn giản, nếu như bạn có 2 block html khác nhau, nhưng cần phải áp dụng cùng một style vào cả 2 block đó, khi đó bạn có thể sử dụng extend để liên kết 2 block này.

Ví dụ:

```less
li.list > a {
  // style cho list
}
button.list-style {
  &:extend(li.list > a); // sử dụng lại style cho list vừa khai báo ở trên
}
```
