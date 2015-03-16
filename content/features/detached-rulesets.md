> Allow wrapping of a css block, defined in a mixin

Có từ phiên bản [v1.7.0]({{ less.master }}CHANGELOG.md)

Ruleset tách rời là một nhóm các thuộc tính css, các ruleset lồng, các khai báo media hoặc bất cứ thứ gì khác lưu trong một biến. Bạn có thể thêm nó vào một ruleset khác hoặc một cấu trúc khác, và tất cả các thuộc tính của nó sẽ được sao chép sang đó. Bạn cũng có thể sử dụng nó như một tham số gọi mixin hay sử dụng nó như một biến bình thường.

Ví dụ đơn giản:
````less
// khai báo ruleset tách rời
@detached-ruleset: { background: red; };

// sử dụng ruleset tách rời
.top {
    @detached-ruleset(); 
}
````

Kết quả:
````css
.top {
  background: red;
}
````

Cặp dấu ngoặc ở sau lời gọi ruleset là bắt buộc. Câu lệnh `@detached-ruleset;` sẽ KHÔNG hoạt động.

Có thể ứng dụng tập luât tách rời để tạo ra một mixin làm nhiệm vụ bọc một đoạn code trong một câu media query hoặc trong một class dành riêng cho trình duyệt không được hỗ trợ. Các ruleset có thể được ném vào trong mixin và sau đó được mixin bọc lại, ví dụ:

```less
.desktop-and-old-ie(@rules) {
  @media screen and (min-width: 1200) { @rules(); }
  html.lt-ie9 &                       { @rules(); }
}

header {
  background-color: blue;

  .desktop-and-old-ie({
    background-color: red;
  });
}
```

Ở đây, mixin `desktop-and-old-ie` tạo ra câu media query và class gốc, và bạn có thể dùng mixin này để bọc một đoạn code. Kết quả như sau:

```css
header {
  background-color: blue;
}
@media screen and (min-width: 1200) {
  header {
    background-color: red;
  }
}
html.lt-ie9 header {
  background-color: red;
}
```

Ruleset có thế được gán vào một biến và có thể sử dụng khi gọi mixin, và cũng có thể chứa tất cả các tính năng của less, ví dụ:

```less
@my-ruleset: {
    .my-selector {
      background-color: black;
    }
  };
```

Bạn cũng có thể sử dụng cùng [bong bóng media query](#features-overview-feature-media-query-bubbling-and-nested-media-queries), ví dụ

```less
@my-ruleset: {
    .my-selector {
      @media tv {
        background-color: black;
      }
    }
  };
@media (orientation:portrait) {
    @my-ruleset();
}
```

kết quả:

```css
@media (orientation: portrait) and tv {
  .my-selector {
    background-color: black;
  }
}
```

Lệnh gọi ruleset tách rời có thể mở (trả về) tất cả các mixin vào trong selector gọi, tương tự như khi sử dụng mixin. Tuy nhiên, nó KHÔNG trả về biến.

Mixin trả về:
````less
// ruleset tách rời với mixin
@detached-ruleset: { 
    .mixin() {
        color:blue;
    }
};
// gọi đến ruleset tách rời
.caller {
    @detached-ruleset(); 
    .mixin();
}
````

Kết quả:
````css
.caller {
  color: blue;
}
````

Biến private:
````less
detached-ruleset: { 
    @color:blue; // biến chỉ có phạm vi trong ruleset
};
.caller {
    color: @color; // lỗi cú pháp, biến @color không tồn tại
}
````

## Phạm vị
Một ruleset tách rời có thể sử dụng tất cả các biến và mixin trong phạm vi ở nơi nó được *khai báo* và ở nơi nó được *gọi*. Nói cách khác, nó có quyền truy cập trong phạm vi khai báo và phạm vi gọi của nó. Nếu cả hai phạm vi đều có cùng một biến hay mixin, phạm vi khai báo sẽ được ưu tiên.

*Phạm vi khai báo* là nơi phần thân ruleset tách rời được khai báo. Copy một luật tách rời từ một biến này vào một biến khác không thể thay đổi phạm vi của nó. ruleset không có quyền truy cập đến phạm vi mới khi chỉđược tham chiếu ở đó.

Cuối cùng, một ruleset tách rời có thể truy cập đến phạm vi bằng cách được mở (được nhập) vào nó.

#### Tầm nhìn của phạm vi khai báo và phạm vi gọi
Ruleset tách rồi nhìn thấy các biến và mixin của selector gọi nó:

````less
@detached-ruleset: {
  caller-variable: @callerVariable; // bieens không tồn tại
  .callerMixin(); // mixin không tồn tại 
};

selector {
  // sử dụng ruleset tách rời
  @detached-ruleset(); 

  // khai báo biến và mixin cần được sử dụng trong ruleset tách rời
  @callerVariable: value;
  .callerMixin() {
    variable: declaration;
  }
}
````

Kết quả:
````css
selector {
  caller-variable: value;
  variable: declaration;
}
````

Biến và mixin có thể truy cập được từ nơi khai báo được ưu tiên hơn biến và mixin ở nơi gọi:
````less
@variable: global;
@detached-ruleset: {
  // sẽ sử dụng biến toàn cục (giá trị global)
  // do biến này có thể truy cập được từ
  // nơi khai báo ruleset tách rời
  variable: @variable; 
};

selector {
  @detached-ruleset();
  @variable: value; // giá trị được khai báo ở nơi gọi sẽ bị bỏ qua
}
````

Kết quả:
````css
selector {
  variable: global;
}
````

#### Việc Tham Chiếu *Không* Thay Đổi Phạm Vi Của Ruleset Tách Rời
Một tập luận không có quyền truy cập tại phạm vi khi chỉ được tham chiếu ở đó:
````less
@detached-1: { scope-detached: @one @two; };
.one {
  @one: visible;
  .two {
    @detached-2: @detached-1; // copy/đổi tên ruleset
    @two: visible; // ruleset không thể thấy biến này
  }
}

.usePlace {
  .one > .two(); 
  @detached-2();
}
````

Sẽ sinh ra lỗi:
````
ERROR 1:32 The variable "@one" was not declared.
````

#### Mở Khóa *Có* Thay Đổi Phạm Vi Của Ruleset Tách Rời
Một ruleset tách rời sẽ được thêm quyền truy cập khi được mở khóa (được nhập) ở trong một phạm vi:
````less
#space {
  .importer1() {
    @detached: { scope-detached: @variable; }; // khai báo ruleset tách rời
  }
}

.importer2() {
  @variable: value; // ruleset tách rời đã được mở khóa CÓ THỂ nhìn thấy biến này
  #space > .importer1(); // mở khóa/nhập ruleset tách rời
}

.usePlace {
  .importer2(); // mở khóa/nhập ruleset tách rời
   @detached();
}
````

Kết quả:
````css
.usePlace {
  scope-detached: value;
}
````
