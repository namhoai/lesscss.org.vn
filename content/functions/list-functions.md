### length

> Trả về số lượng phần tử trong danh sách giá trị.

Parameters: `list` - a comma or space separated list of values.
Tham số: `list` - danh sách (ngăn cách bởi dấu phẩy hay dấu cách)
Trả về: số nguyên (số lượng phần tử trong danh sách)

Ví dụ: `length(1px solid #0080ff);`
Kết quả: `3`

Ví dụ:

```less
@list: "banana", "tomato", "potato", "peach";
n: length(@list);
```

Kết quả:

```
n: 4;
```

### extract

> Trả về giá trị ở một vị trí xác định trong danh sách

Tham số:
`list` - danh sách (ngăn cách bởi dấu phẩy hay dấu cách)
`index` - số nguyên (vị trí của phần tử cần lấy về trong danh sách)
Trả về: giá trị ở vị trí xác định trong danh sách

Ví dụ: `extract(8px dotted red, 2);`
Kết quả: `dotted`

Ví dụ:

```less
@list: apple, pear, coconut, orange;
value: extract(@list, 3);
```

Kết quả:

```
value: coconut;
```
