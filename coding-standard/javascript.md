# Javascript coding convention
### File  

- Khi đặt tên file chỉ được dùng **lowercase**, dùng dấu `-` để nối các từ trong tên file.
- Tên file với đuôi mở rộng sẽ để dấu `.` ngăn cách. Ví dụ `.env.example` thay vì đặt là `.env-example`
- File Encoding phải là **UTF-8**

### Object, Array

- Khai báo object dùng `{}` không sử dụng `new Object()`
- Khai báo array dùng `[]` không sử dụng `new Array()`
- Không sử dụng các [reserved words](http://es5.github.io/#x7.6.1) cho các key của Object
- Khi thêm phần tử vào mảng dùng `push()` không dùng `index` của array  

```javascript
// bad
users[users.length] = 'new user';

// good
users.push('new user');
```

- Khi muốn copy một array dùng `...`

```javascript
const itemsCopy = [...items];
```
- Convert từ array sang object sử dụng `Array.prototype.slice`

### String, Interger, ...

- Không dùng từ khóa `var` để khai báo, sử dụng `let`. Dùng `const` cho những biến hằng
- Khai báo `string` chỉ dùng `'` không nên dùng `"`
- Convert sang `string` chỉ cộng thêm `''` vào trước biến, không cộng vào sau
- Khi biến `string` 1 dòng không quá 100 kí tự.
- Sử dụng `Array#join` để nối chuối trong mảng
- Khi nối text với 1 biến sử dụng [`prefer-template`](http://eslint.org/docs/rules/prefer-template.html)

```javascript
function sayHi(name) {
  return `How are you, ${name}?`;
}
```
- Khi ép kiểu sang `int` thì dùng `Number` hoặc dùng `parseInt` thì phải thêm param radix `parseInt(string, 10)`
- Khai báo biến là element html thêm `$` trước tên biến : `let $sidebar = $('.sidebar');`
- Khai báo biến đều bắt đầu bằng từ khóa tương ứng, không sử dụng `,` để khai báo nhiều biến
- Những biết cùng dạng thì khai báo cùng nhau

```javascript
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;
```

### Đặt tên

- Đặt tên biến và tên function sử dụng [Camel case](https://en.wikipedia.org/wiki/Camel_case)
- Đặt tên class sử dụng [PascalCase](https://en.wikipedia.org/wiki/PascalCase)
- Khi đặt tên có tính tự giải thích
- Khi đặt tên biến cho các element với jQuery thêm `$` vào trước tên biến : `let $sidebar = $('.sidebar');`
- Khi comment nhiều dòng dùng `/** ... */`
- Khi comment 1 dòng dùng `//` và comment vào 1 dòng mới. Bên trên phải là 1 dòng trắng

```javascript
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  var type = this.type || 'no type';

  return type;
}
```

### Function

- Không đặt tên param là `arguments`
- Khai báo function `{` phải cùng dòng với tên function
- Khai báo function sau `()` phải có 1 khoảng trắng trước `{`
- Không khai báo function trong 1 block, nếu khai báo trong 1 block thì phải gán cho 1 biến

```javascript
let test;
if (currentUser) {
  test = function test() {
    console.log('Yup.');
  };
}
```

- Khi function có tham số có giá trị mặc định luôn để ở dưới cùng

```javascript
// good
function handleThings(name, opts = {}) {
  // ...
}
```

### Khoảng trắng
- Sử dụng 2 khoảng trắng tương ứng với 1 tab
- Sau các từ khóa `if`, `while`, `do`, ... phải có 1 khoảng trắng
- Trước và sau các biến có khoảng trắng
- Kết thúc 1 block phải có 1 dòng trắng
- Trước và sau các toán tử (= + - * / ) phải có 1 khoảng trắng
- Nếu array có nhiều dòng, trước và sau array có 1 dòng trắng

```javascript
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  }
];

const numberInArray = [
  1,
  2
];
```

### Các phép toán

- Sử dụng `===` và `!==` thay vì dùng `==` và `!=`
- Khi check `booleans` dùng các biểu thức rút gọn : 

```javascript
// bad
if (isValid === true) {
  // ...
}

// good
if (isValid) {
  // ...
}

// bad
if (name) {
  // ...
}

// good
if (name !== '') {
  // ...
}

// bad
if (collection.length) {
  // ...
}

// good
if (collection.length > 0) {
  // ...
}
```
