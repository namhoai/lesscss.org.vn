### escape

> Áp dụng [phép mã hóa URL](http://en.wikipedia.org/wiki/Percent-encoding) đối với các ký tự đặc biệt trong một chuỗi.

* Những ký tự sau đây sẽ không bị mã hóa: `,`, `/`, `?`, `@`, `&`, `+`, `'`, `~`, `!` và `$`.
* Các ký tự được mã hóa phổ biến bao gồm: `\<space\>`, `#`, `^`, `(`, `)`, `{`, `}`, `|`, `:`, `>`, `<`, `;`, `]`, `[` và `=`.

Tham số: `string` - Chuỗi ký tự cần escape.

Kết quả trả về: `string` - Chuỗi ký tự đã được escape không chứa dấu quote.

Ví dụ:

```less
escape('a=1')
```

Kết quả:

```css
a%3D1
```

Lưu ý: Nếu tham số truyền vào không phải dạng chuỗi, kết quả sẽ không được xác định. Function sẽ trả về `undefined` và tham số đầu vào trong trường hợp này. Tuy nhiên cách xử lý này có thể thay đổi trong tương lai.


### e

> Escape CSS, thay thế cú pháp `~"value"`.

Function này yêu cầu đầu vào là một chuỗi và trả về kết quả là một chuỗi không chứa quote. Nó có thể được sử dụng để in ra các giá trị CSS không đúng cú pháp, hoặc sử dụng các cú pháp đặc biệt mà Less không thể nhận ra.

Tham số: `string` - Chuỗi cần escape.

Kết quả trả về: `string` - : Chuỗi ký tự đã được escape không chứa dấu quote.

Ví dụ:

```less
filter: e("ms:alwaysHasItsOwnSyntax.For.Stuff()");
```

Kết quả:

```css
filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
```

Lưu ý: Function này chấp nhận đầu vào là cả các giá trị escape `~""` và các con số. Nếu tham số đầu vào không hợp lệ, function sẽ báo lỗi trả về.


### % format

> Function `%(string, arguments ...)` có tác dụng format một chuỗi.

Tham số đầu tiên là một chuỗi đi kèm với placeholder. Toàn bộ các placeholder đều bắt đầu bằng ký tự `%` và theo sau bởi một trong các chữ cái `s`,`S`,`d`,`D`,`a`, or `A`. Các tham số còn lại là các biểu thức để thay thế cho các placeholder. Nếu bạn muốn in ra một ký tự `%`, hãy sử dụng một ký tự `%` khác đi kèm `%%`.

Hãy sử dụng placeholder dạng in hoa nếu như bạn muốn escape các ký tự đặc biệt thành mã escape dạng utf-8.
Function này sẽ escape toàn bộ các ký tự ngoại trừ `()'~!`. Dấu cách sẽ được escape thành `%20`. Các placeholder dạng viết thường sẽ được giữ nguyên các ký tự đặc biệt.

Placeholder:
* `d`, `D`, `a`, `A` - có thể được thay thế bằng một loại tham số bất kỳ (màu sắc, số, giá trị đã escape, biểu thức, ...). Nếu như bạn sử dụng chúng kết hợp với chuỗi, thì toàn bộ chuỗi sẽ được sử dụng - bao gồm cả các quote của nó. Tuy nhiên, quote sẽ được giữ nguyên vị trí trong chuỗi và không bị escape bởi ký tự "/" hoặc cái gì đó tương tự.
* `s`, `S` - có thể được thay thế bằng một loại tham số bất kỳ ngoại trừ màu sắc. Nếu bạn sử dụng chúng kết hợp với chuỗi, thì chỉ có giá trị của chuỗi được sử dụng - quote của string sẽ bị loại bỏ.

Tham số:

* `string`: format chuỗi với placeholder,
* `anything`* : các giá trị để thay thế cho các placeholder.

Kết quả trả về: `string` - chuỗi đã được format.

Ví dụ:

```less
format-a-d: %("repetitions: %a file: %d", 1 + 2, "directory/file.less");
format-a-d-upper: %('repetitions: %A file: %D', 1 + 2, "directory/file.less");
format-s: %("repetitions: %s file: %s", 1 + 2, "directory/file.less");
format-s-upper: %('repetitions: %S file: %S', 1 + 2, "directory/file.less");
```
Kết quả:

```css
format-a-d: "repetitions: 3 file: "directory/file.less"";
format-a-d-upper: "repetitions: 3 file: %22directory%2Ffile.less%22";
format-s: "repetitions: 3 file: directory/file.less";
format-s-upper: "repetitions: 3 file: directory%2Ffile.less";
```


### replace

> Thay thế một đoạn văn bản trong chuỗi.

Được phát hành trong version [v1.7.0]({{ less.master }}CHANGELOG.md)

Tham số:

* `string`: Chuỗi để tìm kiếm và thay thế.
* `pattern`: Một chuỗi hoặc một mẫu biểu thức chính quy dùng để tìm kiếm.
* `replacement`: Chuỗi dùng để thay thế kết quả tìm kiếm được.
* `flags`: (Tùy ý) cờ biểu thức chính quy.

Kết quả trả về: Chuỗi với các giá trị đã được thay thế.

Ví dụ:

```less
replace("Hello, Mars?", "Mars\?", "Earth!");
replace("One + one = 4", "one", "2", "gi");
replace('This is a string.', "(string)\.$", "new $1.");
replace(~"bar-1", '1', '2');
```
Kết quả:

```css
"Hello, Earth!";
"2 + 2 = 4";
'This is a new string.';
bar-2;
```
