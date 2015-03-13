> Các phép toán sau _tương tự_ (có thể không hẳn là y hệt) với các chế độ hòa trộn trong các phần mềm sửa ảnh như Photoshop, Fireworks hay GIMP. Bạn có thể sử dụng chúng để tạo ra các màu CSS phù hơpj với ảnh của bạn.

### multiply

> `Multiply` hai màu. Giá trị màu ở các kênh RGB tương ứng được nhân lại với nhau, sau đó chia cho 255, cho ra một màu tối hơn hai màu gốc.

Tham số:

* `color1`: đối tượng màu.
* `color2`: đối tượng màu.

Trả về: `color`

**Ví dụ**:

```less
multiply(#ff6600, #000000);
```
![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
multiply(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#331400:#ffffff/text:331400)

```less
multiply(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
multiply(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#993d00:#ffffff/text:993d00)

```less
multiply(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
multiply(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
multiply(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
multiply(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
multiply(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)


### screen

> Ngược lại với `multiply`. Cho ra màu sáng hơn hai màu gốc.

Tham số:

* `color1`: đối tượng màu.
* `color2`: đối tượng màu.

Trả về: `color`

Ví dụ:

```less
screen(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
screen(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ffa366:#ffffff/text:ffa366)

```less
screen(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ffc299:#000000/text:ffc299)

```less
screen(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffe0cc:#000000/text:ffe0cc)

```less
screen(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
screen(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ffff00:#ffffff/text:ffff00)

```less
screen(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### overlay

> Kết hợp `multiply` và `screen`, làm sáng lên kênh màu sáng và làm tối đi kênh màu tối. **Lưu ý**: Kênh màu sáng hay tối là phụ thuộc vào màu thứ nhất

Tham số:

* `color1`: Màu gốc, cũng là màu được dùng để xác định kênh màu sáng hay tối.
* `color2`: Đối tượng màu để _overlay_

Trả về: `color`

Ví dụ:

```less
overlay(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
overlay(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5200:#ffffff/text:ff5200)

```less
overlay(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7a00:#ffffff/text:ff7a00)

```less
overlay(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffa300:#ffffff/text:ffa300)

```less
overlay(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)


### softlight

> Tương tự như `overlay` nhưng tránh làm cho màu thành đen tuyền hoặc trắng toát

Tham số:

* `color1`: Đối tượng màu để _soft light_ màu còn lại.
* `color2`: Đối tượng màu để được _soft light_.

Trả về: `color`

Ví dụ:

```less
softlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff4100:#ffffff/text:ff4100)

```less
softlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5a00:#ffffff/text:ff5a00)

```less
softlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7200:#ffffff/text:ff7200)

```less
softlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ff8a00:#ffffff/text:ff8a00)

```less
softlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)


### hardlight

> Tương tự như `overlay` nhưng đảo ngược thứ tự tham số.

Tham số:

* `color1`: Đối tượng màu để _overlay_
* `color2`: Màu gốc, cũng là màu được dùng để xác định kênh màu sáng hay tối.

Trả về: `color`

Ví dụ:

```less
hardlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
hardlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
hardlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
hardlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
hardlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
hardlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
hardlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
hardlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#00ff00:#ffffff/text:00ff00)

```less
hardlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#0000ff:#ffffff/text:0000ff)


### difference

> Trừ giá trị màu thứ nhất đi giá trị màu thứ hai trong các kênh màu tương ứng. Giá trị âm được đảo ngược. Trừ giá trị màu đen tuyền sẽ không gây ra thay đổi nào; Trừ giá trị màu trắng sẽ tạo nên hiệu ứng đảo ngược màu.

Tham số:

* `color1`: Màu bị trừ.
* `color2`: Màu trừ.

Trả về: `color`

Ví dụ:

```less
difference(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
difference(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc3333:#ffffff/text:cc3333)

```less
difference(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#990066:#ffffff/text:990066)

```less
difference(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#663399:#ffffff/text:663399)

```less
difference(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#3366cc:#ffffff/text:3366cc)

```less
difference(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
difference(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
difference(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
difference(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### exclusion

> Hiệu ứng tương tự như `difference` nhưng với độ tương phản thấp hơn.

Tham số:

* `color1`: Màu bị trừ.
* `color2`: Màu trừ.

Kết quả: `color`

Ví dụ:

```less
exclusion(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
exclusion(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc7033:#ffffff/text:cc7033)

```less
exclusion(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#997a66:#ffffff/text:997a66)

```less
exclusion(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#668599:#ffffff/text:668599)

```less
exclusion(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#338fcc:#ffffff/text:338fcc)

```less
exclusion(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
exclusion(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
exclusion(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
exclusion(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### average

> Tính giá trị màu trung bình của hai màu trên các kênh RGB tương ứng.

Tham số:

* `color1`: Đối tượng màu.
* `color2`: Đối tượng màu.

Kết quả: `color`

Ví dụ:

```less
average(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#803300:#ffffff/text:803300)

```less
average(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#994d1a:#ffffff/text:994d1a)

```less
average(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#b36633:#ffffff/text:b36633)

```less
average(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#cc804d:#ffffff/text:cc804d)

```less
average(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#e69966:#ffffff/text:e69966)

```less
average(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffb380:#000000/text:ffb380)

```less
average(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff3300:#ffffff/text:ff3300)

```less
average(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#80b300:#ffffff/text:80b300)

```less
average(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#803380:#ffffff/text:803380)

### negation

> Tạo ra hiệu ứng ngược lại với `difference`

Tạo ra màu sáng hơn màu gốc. **Lưu ý**: Hiệu ứng _ngược lại_ không có nghĩa là _đảo ngược_ hiêu ứng bằng cách thay phép trừ bằng _phép cộng_.

Tham số:

* `color1`: Màu bị trừ.
* `color2`: Màu trừ.

Kết quả: `color`

Ví dụ:

```less
negation(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
negation(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc9933:#ffffff/text:cc9933)

```less
negation(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#99cc66:#ffffff/text:99cc66)

```less
negation(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#66ff99:#ffffff/text:66ff99)

```less
negation(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#33cccc:#ffffff/text:33cccc)

```less
negation(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
negation(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
negation(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
negation(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#ffffff/text:ff66ff)
