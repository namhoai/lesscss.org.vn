### ceil

> Làm tròn lên số nguyên gần nhất.

Tham số: `number` - số thực.

Trả về: `integer`

Ví dụ: `ceil(2.4)`

Kết quả: `3`


### floor

> Làm trong xuống số nguyên gần nhất.

Tham số: `number` - số thực.

Trả về: `integer`

Ví dụ: `floor(2.6)`

Kết quả: `2`


### percentage

> Chuyển đổi số thực sang dạng phần trăm

Tham số: `number` - số thực.

Trả về: `string`

Ví dụ: `percentage(0.5)`

Kết quả: `50%`


### round

> Làm tròn.

Tham số:
* `number`: số thực.
* `decimalPlaces`: không bắt buộc - số chữ số thập phân (sau dấy phẩy) của kết quả làm tròn. Mặc định là 0.

Trả về: `number`

Ví dụ: `round(1.67)`

Kết quả: `2`

Ví dụ: `round(1.67, 1)`

Kết quả: `1.7`


### sqrt

> Tính căn hai của một số, giữ nguyên đơn vị.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ:

```less
sqrt(25cm)
```

Kết quả:

```css
5cm
```

Ví dụ:

```less
sqrt(18.6%)
```

Kết quả:

```js
4.312771730569565%;
```


### abs

> Tính giá trị tuyệt đối của một số, giữ nguyên đơn vị.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ #1: `abs(25cm)`

Kết quả: `25cm`

Ví dụ #2: `abs(-18.6%)`

Kết quả: `18.6%;`


### sin

> Tính sin.

Với tham số truyền vào không có đơn vị, Less sẽ ngầm hiểu là radian.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ:

```less
sin(1); // sine of 1 radian
sin(1deg); // sine of 1 degree
sin(1grad); // sine of 1 gradian
```

Kết quả:

```
0.8414709848078965; // sine of 1 radian
0.01745240643728351; // sine of 1 degree
0.015707317311820675; // sine of 1 gradian
```


### asin

> Tính arcsine (đảo ngược của sin).

Trả về số đo góc (đơn vị radian), là một số trong khoảng từ `-π/2` đến `π/2`.

Tham số: `number` - số thực trong khoảng `[-1, 1]`.

Trả về: `number`

Ví dụ:

```less
asin(-0.8414709848078965)
asin(0)
asin(2)
```

Kết quả:

```
-1rad
0rad
NaNrad
```


### cos

> Tính cosine.

Với tham số truyền vào không có đơn vị, Less sẽ ngầm hiểu là radian.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ:

```less
cos(1) // cosine of 1 radian
cos(1deg) // cosine of 1 degree
cos(1grad) // cosine of 1 gradian
```

Kết quả:

```
0.5403023058681398 // cosine of 1 radian
0.9998476951563913 // cosine of 1 degree
0.9998766324816606 // cosine of 1 gradian
```


### acos

> Tính arccos (đảo ngược của cos).

Trả về số đo góc (đơn vị radian), là một số trong khoảng từ 0 đến π.

Tham số: `number` - số thực trong khoảng [-1, 1].

Trả về: `number`

Ví dụ:

```less
acos(0.5403023058681398)
acos(1)
acos(2)
```

Kết quả:

```
1rad
0rad
NaNrad
```


### tan

> Tính tan.

Với tham số truyền vào không có đơn vị, Less sẽ ngầm hiểu là radian.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ:

```less
tan(1) // tangent of 1 radian
tan(1deg) // tangent of 1 degree
tan(1grad) // tangent of 1 gradian
```

Kết quả:

```
1.5574077246549023   // tangent of 1 radian
0.017455064928217585 // tangent of 1 degree
0.015709255323664916 // tangent of 1 gradian
```


### atan

> Tính arctan (đảo ngược của tan).

Trả về số đo góc (đơn vị radian), là một số trong khoảng từ `-π/2` đến `π/2`.

Tham số: `number` - số thực.

Trả về: `number`

Ví dụ:

```less
atan(-1.5574077246549023)
atan(0)
round(atan(22), 6) // arctangent of 22 rounded to 6 decimal places
```

Kết quả:

```
-1rad
0rad
1.525373rad;
```


### pi

> Trả về &pi; (pi);

Tham số: `none`

Trả về: `number`

Ví dụ:

```less
pi()
```

Kết quả:

```
3.141592653589793
```


### pow

> Trả về lũy thừa của tham số thứ nhất với số mũ là tham số thứ hai.

Giá trị trả về có cùng đơn vị với tham số thứ nhất, Less bỏ qua đơn vị của tham số thứ hai.


Tham số:
* `number`: cơ số -số thực.
* `number`: số mũ - số thực.

Trả về: `number`

Ví dụ:

```less
pow(0cm, 0px)
pow(25, -2)
pow(25, 0.5)
pow(-25, 0.5)
pow(-25%, -0.5)
```

Kết quả:

```
1cm
0.0016
5
NaN
NaN%
```


### mod

> Trả về số dư của phép chia tham số thứ nhất cho tham số thứ hai.

Giá trị trả về có cùng đơn vị với tham số thứ nhất, Less bỏ qua đơn vị của tham số thứ hai. Hàm này làm việc với cả số âm và số thực.

Tham số:
* `number`: số thực.
* `number`: số thực.

Trả về: `number`

Ví dụ:

```less
mod(0cm, 0px)
mod(11cm, 6px);
mod(-26%, -5);
```

Kết quả:

```
NaNcm;
5cm
-1%;
```


### min

> Trả về giá trị nhỏ nhất trong các giá trị truyền vào.

Tham số: `value1, ..., valueN` - một hoặc nhiều giá trị

Trả về: giá trị nhỏ nhất.

Ví dụ: `min(5, 10);`

Kết quả: `5`

Ví dụ: `min(3px, 42px, 1px, 16px);`

Kết quả: `1px`


### max

> Trả về giá trị lớn nhất trong các giá trị truyền vào.

Tham số: `value1, ..., valueN` - một hoặc nhiều giá trị

Trả về: giá trị lớn nhất.

Ví dụ: `max(5, 10);`

Kết quả: `10`

Ví dụ: `max(3%, 42%, 1%, 16%);`

Kết quả: `42%`
