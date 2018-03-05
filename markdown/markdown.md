# Markdown

## Markdown là gì:

- Markdown là một syntax đơn giản và dễ sử dụng để style đoạn văn bản trên nền tảng GitHub
- Markdown cho phép người dùng format chữ cái, thêm ảnh hay tạo danh sách sử dụng một vài kí tự đặc biệt ví dụ như # hay *

## Syntax

Một vài syntax của markdown:

### Heading

```
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

# h1
## h2
### h3
#### h4
##### h5
###### h6

### Styling

Bold : ```** **``` hoặc ```__ __```

Italic : ```* *``` hoặc ```_ _```

Strikethrough : ```~~ ~~```

Bold và italic : ```** **``` và ```_ _```

```
bold is **this** or __this__
italic is *this* or _this_
this is ~~strikethrough~~
this is **_bold and italic_*
```

bold is **this** or __this__

italci is *this* or _this_

this is ~~strikethrough~~

this is **_bold and italic_*

### List

#### Unordered list

Sử dụng syntax - hoặc *

```
- item 1
- item 2
* item 3
* item 4
```

- item 1
- item 2
* item 3
* item 4

#### Ordered list

Bắt đầu dòng bằng 1 số

```
1. item 1
2. item 2
3. item 3
```

1. item 1
2. item 2
2. item 3

#### Task list

```- [x]``` đánh dấu task đã hoàn thành, 
```- []``` đánh dấu task chưa hoàn thành

```
- [x] Finished task
- [ ] Unfinish task
- [ ] Open pull request
```

- [x] Finished task
- [ ] Unfinish task
- [ ] Unfinish task

### Hình ảnh

```
Đây là logo công ty (hover để xem tiêu đề):

Inline-style: 
![alt text](https://haposoft.com/assets/front/img/haposoft.png "Logo 1")

Reference-style: 
![alt text][logo]

[logo]: https://haposoft.com/assets/front/img/haposoft.png "Logo 2"
```

Đây là logo công ty (hover để xem tiêu đề):

Inline-style: 
![alt text](https://haposoft.com/assets/front/img/haposoft.png "Logo 1")

Reference-style: 
![alt text][logo]

[logo]: https://haposoft.com/assets/front/img/haposoft.png "Logo 2"

### Links

Có rất nhiều cách để tạo liên kết bằng markdown :

```
Inline style : [inline-style link](http://wiki.haposoft.com/)

Inline với tiêu đề (hover để xem tiêu đề) : [inline-style with title](http://wiki.haposoft.com/ "Haposoft")

Reference style : [reference-style link][Haposoft]

[Haposoft]: http://wiki.haposoft.com/

Hoặc có thể ghi trực tiếp liên kết vào như http://wiki.haposoft.com/ hay <http://wiki.haposoft.com/>
```

Inline style : [inline-style link](http://wiki.haposoft.com/)

Inline với tiêu đề (hover để xem tiêu đề) : [inline-style with title](http://wiki.haposoft.com/ "Haposoft")

Reference style : [reference-style link][Haposoft]

[Haposoft]: http://wiki.haposoft.com/

Hoặc có thể ghi trực tiếp liên kết vào như http://wiki.haposoft.com/ hay <http://wiki.haposoft.com/>

### Xuống dòng

Để xuống dòng ta chèn vào giữa một dòng trống

```
Đây là đoạn văn thứ nhất

Đây là đoạn văn thứ hai
```

Đây là đoạn văn thứ nhất

Đây là đoạn văn thứ hai

### Emoji

Có thể thêm emoji bằng cách sử dụng syntax :Mã emoji:

```
:+1: :smile: :family:
```

:+1:  :smile:  :family:

Xem danh sách toàn bộ emoji và code ở [Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

### Bảng

Mỗi hàng được viết trên 1 dòng. Dòng header cell được phân biệt bằng cách sử dung tối thiểu 3 dấu ```-```. 
Các cột được phân biệt với nhau bằng dấu ```|```

```
Tên | Tuổi
--- | ---
Nguyễn Văn A | 20
Hoàng Văn B | 30
```

Tên | Tuổi
--- | ---
Nguyễn Văn A | 20
Hoàng Văn B | 30