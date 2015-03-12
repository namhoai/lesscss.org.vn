> Cách truyền tham số vào mixin

Mixin có thể nhận tham số là các biến.

Ví dụ:

```less
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

Và sau đó ta có thể sử dụng nó trong các ruleset:


```less
#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
```

Các tham số cũng có thể có giá trị mặc định:

```less
.border-radius(@radius: 5px) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

Ta có thể gọi nó như sau:

```less
#header {
  .border-radius;
}
```

Và #header sẽ có border-radius 5px

Ta cũng có thể sử dụng mixin tham số nhưng không đặt tham số nào. Cách này hữu dụng khi ta không muốn in mixin đó ra CSS, nhưng lại muốn sử dụng các thuộc tính của nó ở trong các ruleset khác:

```less
.wrap() {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}

pre { .wrap }
```

Kết quả:

```css
pre {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}
```

### Mixins nhiều tham số
Các tham số truyền vào mixin cách nhau bằng *chấm phẩy (;)* hoặc *phẩy (,)*, tuy nhiên nên sử dụng *chấm phẩy*. Dấu phẩy có khi mang hai nghĩa: vừa là ký tự phân cách tham số mixin, cũng đồng thời là ký tự phân cách của một danh sách trong CSS chuẩn.

Bởi vậy, khi sử dụng dấu phẩy để phân cách tham số mixin, ta sẽ không có cách nào truyền vào một danh sách CSS. Hơn nữa, nếu trình dịch nhìn thấy ít nhất một ký tự chấm phẩy trong lời gọi mixin, nó sẽ ngầm hiểu rằng các tham số được phân cách bằng chấm phẩy, và vì vậy các dấu phẩy là của danh sách CSS:

* hai tham số đều là danh sách: `.name(1, 2, 3; something, else)`,
* ba tham số đều là số: `.name(1, 2, 3)`,
* sử dụng dấu chấm phẩy bù nhìn để gọi một mixin với tham số là danh sách css có chứa dấu phẩy: `.name(1, 2, 3;)`,
* giá trị mặc định của tham số là danh sách

Less cho phép khai báo nhiều mixin cùng tên và số lượng tham số. Trong số các mixin cùng tên đó, Less sẽ sử dụng các thuộc tính của tất cả các mixin có thể. Nếu bạn gọi mixin với một tham số, ví dụ `.mixin(green);`, thì tất cả thuộc tính của các mixin với chính xác một tham số thiết yếu sẽ được sử dụng:

```less
.mixin(@color) {
  color-1: @color;
}
.mixin(@color; @padding: 2) {
  color-2: @color;
  padding-2: @padding;
}
.mixin(@color; @padding; @margin: 2) {
  color-3: @color;
  padding-3: @padding;
  margin: @margin @margin @margin @margin;
}
.some .selector div {
  .mixin(#008000);
}
```

Kết quả:

```css
.some .selector div {
  color-1: #008000;
  color-2: #008000;
  padding-2: 2;
}
```

### Truyền tham số bằng tên

Khi truyền tham số vào lệnh gọi mixin, ta có thể sử dụng tên thay vì vị trí. Bất kỳ tham số nào cũng có thể được tham chiếu bằng tên, và không bắt buộc phải ở trong vị trí đặc biệt nào:

```less
.mixin(@color: black; @margin: 10px; @padding: 20px) {
  color: @color;
  margin: @margin;
  padding: @padding;
}
.class1 {
  .mixin(@margin: 20px; @color: #33acfe);
}
.class2 {
  .mixin(#efca44; @padding: 40px);
}
```
kết quả:

```css
.class1 {
  color: #33acfe;
  margin: 20px;
  padding: 20px;
}
.class2 {
  color: #efca44;
  margin: 10px;
  padding: 40px;
}
```

### Biến `@arguments`

`@arguments` là biến đặc biệt trong mixin, có giá trị là tất cả các tham số truyền vào khi mixin được gọi. `@arguments` sẽ hữu ích cho bạn khi bạn không muốn xử lý các tham số rời:

```less
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}
.big-block {
  .box-shadow(2px; 5px);
}
```

Kết quả:

```css
.big-block {
  -webkit-box-shadow: 2px 5px 1px #000;
     -moz-box-shadow: 2px 5px 1px #000;
          box-shadow: 2px 5px 1px #000;
}
```

### Tham số nâng cao và biến `@rest`

Bạn có thể sử dụng `...` nếu bạn muốn mixin của bạn nhận một số lượng tham số bất kỳ. Sử dunjg `...` sau một tên biến sẽ gán các tham số truyền vào vào biến đó.

```less
.mixin(...) {        // matches 0-N arguments
.mixin() {           // matches exactly 0 arguments
.mixin(@a: 1) {      // matches 0-1 arguments
.mixin(@a: 1; ...) { // matches 0-N arguments
.mixin(@a; ...) {    // matches 1-N arguments
```

Ngoài ra:

```less
.mixin(@a; @rest...) {
   // @rest is bound to arguments after @a
   // @arguments is bound to all arguments
}
```

## So khớp mẫu

Đôi khi bạn sẽ muốn thay đổi hành vi của mixin dựa vào tham số truyền vào. Hãy xem với ví dụ cơ bản sau:

```less
.mixin(@s; @color) { ... }

.class {
  .mixin(@switch; #888);
}
```

Giả dụ bạn muốn `.mixin` đưa ra các xử lý khác nhau dựa trên giá trị của `@switch`, ta có thể khai báo `.mixin` như sau:

```less
.mixin(dark; @color) {
  color: darken(@color, 10%);
}
.mixin(light; @color) {
  color: lighten(@color, 10%);
}
.mixin(@_; @color) {
  display: block;
}
```

Và ta gọi mixin như sau:

```less
@switch: light;

.class {
  .mixin(@switch; #888);
}
```

Kết quả:

```css
.class {
  color: #a2a2a2;
  display: block;
}
```

Trong đó, màu được truyền vào `.mixin` đã được làm sáng lên. Nếu giá trị `@switch` là `dark`,
màu truyền vào sẽ được làm tối đi.

Cụ thể như sau:

* Mixin đầu tiên không khớp vì tham số đầu tiên nó nhận phải là `dark`
* Mixin thứ hai khớp, vì tham số đầu tiên nó nhận là `light`.
* Mixin thứ ba khớp vì nó nhận giá trị bất kỳ.

Less sẽ chỉ sử dụng các mixin khớp. Các biến được so khớp và gán vào giá trị bất kỳ.
Anything other than a variable matches only with a value equal to itself.

Ta cũng có thể so khớp dựa trên số lượng tham số, ví dụ:

```less
.mixin(@a) {
  color: @a;
}
.mixin(@a; @b) {
  color: fade(@a; @b);
}
```

Nếu ta gọi `.mixin` với một tham số, ta sẽ gọi đến khai báo đầu tiên, nhưng nếu ta gọi mixin với
*hai* tham số, ta sẽ gọi đến khai báo thứ hai.
