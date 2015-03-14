### isnumber

> Trả về `true` nếu là một số, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là một số, `false` trong các trường hợp còn lại.

Ví dụ:

```less
isnumber(#ff0);     // false
isnumber(blue);     // false
isnumber("string"); // false
isnumber(1234);     // true
isnumber(56px);     // true
isnumber(7.8%);     // true
isnumber(keyword);  // false
isnumber(url(...)); // false
```


### isstring

> Trả về `true` nếu là một chuỗi ký tự, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là một chuỗi ký tự, `false` trong các trường hợp còn lại.

Ví dụ:

```less
isstring(#ff0);     // false
isstring(blue);     // false
isstring("string"); // true
isstring(1234);     // false
isstring(56px);     // false
isstring(7.8%);     // false
isstring(keyword);  // false
isstring(url(...)); // false
```


### iscolor

> Trả về `true` nếu là một màu, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là một màu, `false` trong các trường hợp còn lại.

Ví dụ:

```less
iscolor(#ff0);     // true
iscolor(blue);     // true
iscolor("string"); // false
iscolor(1234);     // false
iscolor(56px);     // false
iscolor(7.8%);     // false
iscolor(keyword);  // false
iscolor(url(...)); // false
```


### iskeyword

> Trả về `true` nếu là một từ khóa, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là một từ khóa, `false` trong các trường hợp còn lại.

Ví dụ:

```less
iskeyword(#ff0);     // false
iskeyword(blue);     // false
iskeyword("string"); // false
iskeyword(1234);     // false
iskeyword(56px);     // false
iskeyword(7.8%);     // false
iskeyword(keyword);  // true
iskeyword(url(...)); // false
```


### isurl

> Trả về `true` nếu là một url, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là một url, `false` trong các trường hợp còn lại.

Ví dụ:

```less
isurl(#ff0);     // false
isurl(blue);     // false
isurl("string"); // false
isurl(1234);     // false
isurl(56px);     // false
isurl(7.8%);     // false
isurl(keyword);  // false
isurl(url(...)); // true
```


### ispixel

> Trả về `true` nếu là một số có đơn vị pixel, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` có đơn vị pixel, `false` trong các trường hợp còn lại.

Ví dụ:

```less
ispixel(#ff0);     // false
ispixel(blue);     // false
ispixel("string"); // false
ispixel(1234);     // false
ispixel(56px);     // true
ispixel(7.8%);     // false
ispixel(keyword);  // false
ispixel(url(...)); // false
```


### isem

> Trả về `true` nếu là một số có đơn vị em, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` có đơn vị em, `false` trong các trường hợp còn lại.

Ví dụ:

```less
isem(#ff0);     // false
isem(blue);     // false
isem("string"); // false
isem(1234);     // false
isem(56px);     // false
isem(7.8em);    // true
isem(keyword);  // false
isem(url(...)); // false
```


### ispercentage

> Trả về `true` nếu là phần trăm, `false` trong các trường hợp còn lại.

Tham số: `value` - giá trị hoặc biến cần đánh giá.

Trả về: `true` nếu `value` là phần trăm, `false` trong các trường hợp còn lại.

Ví dụ:

```less
ispercentage(#ff0);     // false
ispercentage(blue);     // false
ispercentage("string"); // false
ispercentage(1234);     // false
ispercentage(56px);     // false
ispercentage(7.8%);     // true
ispercentage(keyword);  // false
ispercentage(url(...)); // false
```


### isunit

> Trả về `true` nếu là một số có đơn vị nhất định, `false` trong các trường hợp còn lại.

Tham số:
* `value` - giá trị hoặc biến cần đánh giá.
* `unit` - đơn vị đối chiếu (có thể có hoặc không có ngoặc)

Trả về: `true` nếu `value` là số có đơn vị đối chiếu, `false` trong các trường hợp còn lại.

Ví dụ:

```less
isunit(11px, px);  // true
isunit(2.2%, px);  // false
isunit(33px, rem); // false
isunit(4rem, rem); // true
isunit(56px, "%"); // false
isunit(7.8%, '%'); // true
isunit(1234, em);  // false
isunit(#ff0, pt);  // false
isunit("mm", mm);  // false
```


### isruleset

> Trả về `true` nếu là một ruleset, `false` trong các trường hợp còn lại.

Tham số:
* `value` - a variable being evaluated.

Trả về: `true` nếu `value` là một ruleset, `false` trong các trường hợp còn lại.

Ví dụ:

```less
@rules: {
    color: red;
}

isruleset(@rules);   // true
isruleset(#ff0);     // false
isruleset(blue);     // false
isruleset("string"); // false
isruleset(1234);     // false
isruleset(56px);     // false
isruleset(7.8%);     // false
isruleset(keyword);  // false
isruleset(url(...)); // false
```
