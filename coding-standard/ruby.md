# Ruby coding convention

### Mở đầu

Phạm vi bài viết này chọn lọc những quy ước thường gặp nhất khi dùng Ruby trong software development. Có cả những quy ước chủ quan dựa trên kinh nghiệm của người viết và tham khảo các styleguide được đánh giá cao ở trên Github

- [https://github.com/styleguide/ruby](https://github.com/styleguide/ruby)

- [https://github.com/bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)

### General

- Cài đặt Editor của bạn sử dụng soft-tabs với độ rộng 2-spaces
- Làm cho dòng code trở nên dễ đọc hơn với độ dài vừa phải. Nếu không có lý do gì khác, luôn giữ số kí tự trên 1 dòng dưới 80-120 ký tự
- Không để lại những space thừa
- Sử dụng space quanh các toán tử, sau dấu `comma` (,), `colons`, `semicolons`, quanh dấu `{` và `}`

```ruby
sum = 1 + 2
a, b = 1, 2
1 > 2 ? true : false; puts "Hello World"
[1, 2, 3].each { |e| puts e }
```

- Không sử dụng dấu space sau `(`, `[` và trước `]`, `)`

```ruby
method_call(arg).other
[1, 2, 3].length
```

- Không sử dụng space sau `!`

```ruby
!array.include? element
```

- Sử dụng `when` cùng độ sâu với `case`

```ruby
case
when song.name == "Misty"
  puts "Not again!"
when song.duration > 120
  puts "Too long!"
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end
```

- Sử dụng các toán tử gán nếu có thể

```ruby
x = x + y
x = x * y
x = x**y
x = x / y
x = x || y
x = x && y

# good
x += y
x *= y
x **= y
x /= y
x ||= y
x &&= y
```

- Method với parameters quá dài, vượt quá 80 ký tự thì phải xuống dòng với indent

```ruby
# Bad Ex (viết 1 mạch quá 80 kí tự)
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
end

# Bad (Trong trường hợp tên class và tên hàm quá dài dẫn đến indent xấu)
# Trang https://github.com/bbatsov/ruby-style-guide định nghĩa TH này là Good
def send_mail(source)
  Mailer.deliver(to: 'bob@example.com',
                 from: 'us@example.com',
                 subject: 'Important message',
                 body: source.text)
end

# Good
def send_mail(source)
  Mailer.deliver(
    to: 'bob@example.com',
    from: 'us@example.com',
    subject: 'Important message',
    body: source.text)
```

### Loop

- Sử dụng loop với `each` thay cho `for`:

```ruby
arr = [1, 2, 3]

# Bad
for elem in arr do
  puts elem
end

# Good
arr.each { |elem| puts elem }
```

Nguyên nhân là do biến `elem` được truyền trong `scope` nên sẽ không có thể gọi được từ bên ngoài nữa

- Không sử dụng `while/until condition do` cho multiline mà chỉ là `while/until`

```ruby
# bad
while x > 5 do
  # body omitted
end

until x > 5 do
  # body omitted
end

# good
while x > 5
  # body omitted
end

until x > 5
  # body omitted
end
```

- Với `while` nếu có thể viết one-line thì viết thành one-line

```ruby
# Bad
while some_condition
  do_something
end

# Good
do_something while some_condition
```

- Với loop vô hạn thì sử dụng `Kernel#loop`

```ruby
# bad
while true
  do_something
end

until false
  do_something
end

# good
loop do
  do_something
end
```

### Conditional Syntax

- Không sử dùng keyword `then` ở câu điều kiện `if/unless`

```ruby
# Bad
if some_condition then
end

# Good
if some_condition
end
```

- Trong TH câu điều kiện if/else/end có thể xử lý được trong 1 dòng, thay vào đó sử dụng toán tử 3 ngôi

```ruby
# Bad
result = if some_condition then something else something_else end

# Good
result = some_condition ? something : something_else
```

- Khi toán tử 3 ngôi có điều kiện con, thay vào đó lại quay về sử dụng `if/else`

```ruby
# Bad
some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

# Good
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
```

- Trong TH không có mệnh đề `else` thì và có thể viết thành 1 dòng thì hãy viết thành 1 dòng

```ruby
# Bad
if some_condition
end

# Good
do_something if some_condition
```

- Mệnh đề phủ định thì hãy sử dụng `unless` thay vì `!`

```ruby
# Bad
do_something if !some_condition

# Good
do_something unless some_condition
```

- Không dùng `unless/else`, thay vào đó hãy dùng `if/else`

```ruby
# Bad
unless success?
  puts 'failure'
else
  puts 'success'
end

# Good
if success?
  puts 'success'
else
  puts 'failure'
end
```

- Không cần dấu `()` ở mệnh đề `if/unless/while`

```ruby
# Bad
if (x > 10)
end

# Good
if x > 10
end
```

- Trong mệnh đề `if` thì không thêm các biểu thức gán tắt

```ruby
# Bad
if (v = array.grep(/foo/)) ...

# Bad
if v = array.grep(/foo/) ...

# Bad
if (v = self.next_value) == "hello" ...

# Good
v = self.next_value
if v == 'hello' ...
```

- Không được sử dụng `and` hoặc `or` mà hãy sử dụng `&&` và `||`

### Strings

- Sử dụng String Interpolation thay cho nối chuỗi

```ruby
# bad
email_with_name = user.name + " <" + user.email + ">"

# good
email_with_name = "#{user.name} <#{user.email}>"
```

- Nếu không sử dụng String Interpolation thì khuyến khích sử dụng single quote để khai báo

```ruby
# Good
name = 'Bozhidar'

# Bad
name = "Bozhidar"
```

- Sử dụng `heredoc` nếu muốn khai báo MultipleLines String

```ruby
str <<-HEREDOC
        Subscription expiring soon!
        Your free trial will expire in #{days_until_expiration} days.
        Please update your billing information.
      HEREDOC
```

### Block

- Block nếu viết được trong 1 dòng thì sử dụng `{...}`, ngược lại nếu nhiều dòng thì sẽ sử dụng cặp `do...end`

```ruby
names = ['Bozhidar', 'Steve', 'Sarah']

# Good
names.each { |name| puts name }

# Bad
names.each do |name|
  puts name
end

# Bad
names.each { |name| puts sugoku.nagai.shori(fukuzatsu.na.shori(name)) }

# Good
names.each do |name|
  name = fukuzatsu.na.shori(name)
  name = sugoku.nagai.shori(name)
  puts name
end
```

- Đối với `block` với method chain thì sử dụng `{...}`

```ruby
# Good
names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

# Bad
names.select do |name|
  name.start_with?("S")
end.map { |name| name.upcase }
```

- Tham số không sử dụng của `block` thì sử dụng `_`

```ruby
# Bad
result = hash.map { |k, v| v + 1 }

# Good
result = hash.map { |_, v| v + 1 }
```

### Method

- Method không có tham số thì không cần thêm cặp `()` vào sau tên method

```ruby
# Bad
def some_method()
end

# Good
def some_method
end

# Bad
def some_method_with_args arg1, arg2
end

# Good
def some_method_with_args(arg1, arg2)
end
```

- Giữa 2 hàm luôn cách nhau 1 dòng

```ruby
def some_method
  data = initialize(options)

  data.manipulate!

  data.result
end

def some_method
  result
end
```

- Không cần `return` ở cuối hàm

```ruby
# Bad
def some_method(some_arr)
  return some_arr.size
end

# Good
def some_method(some_arr)
  some_arr.size
end
```

- Với các giá trị mặc định của tham số hàm, thì cần thêm space quanh dấu `=`

```ruby
# Bad
def some_method(arg1=:default, arg2=nil, arg3=[])
end

# Good
def some_method(arg1 = :default, arg2 = nil, arg3 = [])
end
```

- Tránh sử dụng one-line method

```ruby
# Bad
def too_much; something; something_else; end

# Good
def some_method
  body
end
```

### Variables

- Với các biến có thể đã được khởi tạo mà muốn gán lại, hãy sử dụng `||=`

```ruby
name ||= 'Bozhidar' # name = Bozhidar nếu name == nil
```

- Tuy nhiên với các giá trị Boolean thì không được sử dụng `||=`

```ruby
# Bad
enabled ||= true

# Good
enabled = true if enabled.nil?
```

### Array, Hash

- Nếu khai báo mảng String thì sử dụng `%w` được thích hơn

```ruby
# bad
STATES = ["draft", "open", "closed"]

# good
STATES = %w(draft open closed)
```

- Ruby 1.9 trở đi thì `Hash` sử dụng ký pháp mới 

```ruby
# Bad
hash = { :one => 1, :two => 2 }

# Good
hash = { one: 1, two: 2 }
```

- Access phần tử đầu và cuối của Array thì dùng `first` và `last` thay vì `[0]` hay `[1]`

### Keyword Arguments

[Keyword Arguments](http://magazine.rubyist.net/?Ruby200SpecialEn-kwarg) là tính năng từ Ruby 2.0 cho phép truyền 1 hash các option vào làm arguments của method.

Thay vì sử dụng

```ruby
def remove_member(user, skip_membership_check=false)
  # ...
end
# Giá trị true ở phía dưới khá khó hiểu
remove_member(user, true)
```

Ta có thể viết lại đẹp hơn với keyword arguments

```ruby
def remove_member(user, skip_membership_check: false)
  # ...
end
remove_member user, skip_membership_check: true
```

### Lambda

- Ruby 1.9 thì `lambda` sử dụng cú pháp `literal`

```ruby
# Bad
lambda = lambda { |a, b| a + b }
lambda.call(1, 2)

# Good
lambda = ->(a, b) { a + b }
lambda.(1, 2)
```

### Numbers

- Sử dụng `range` nếu muốn tìm số random

```ruby
# bad
rand(6) + 1

# good
rand(1..6)
```

- Cẩn trọng với `to_i`

```ruby
nil.to_i #=> 0
```

### Classes

- Sử dụng `def self.method` để định nghĩa `singleton method` vì dễ refactor hơn

```ruby
class TestClass
  # bad
  def TestClass.some_method
    # body omitted
  end

  # good
  def self.some_other_method
    # body omitted
  end
```

- Tránh sử dụng biến global với khai báo `@@` để tránh các hiệu ứng phụ

```ruby
class Parent
  @@class_var = 'parent'

  def self.print_class_var
    puts @@class_var
  end
end

class Child < Parent
  @@class_var = 'child'
end

Parent.print_class_var # => will print 'child'
```

- Tránh sử dụng `class << self` ngoài những TH cần thiết như single accessor hay aliased attributes

```ruby 
class TestClass
  # bad
  class << self
    def first_method
      # body omitted
    end

    def second_method_etc
      # body omitted
    end
  end

  # good
  class << self
    attr_accessor :per_page
    alias_method :nwo, :find_by_name_with_owner
  end

  def self.first_method
    # body omitted
  end

  def self.second_method_etc
    # body omitted
  end
end
```

- Indent 1 khoảng trắng để phân cách các scope method

```ruby
class SomeClass
  def public_method
    # ...
  end

  private
  def private_method
    # ...
  end
end
```

- Với các class không có body thì nên viết kiểu one-line

```ruby
# bad
class FooError < StandardError
end

# Good
class FooError < StandardError; end
```

### Rules đặt tên

- Tên biến và tên method dùng `snake_case`
- Tên Class và Module sử dụng `PascalCase`
- Hằng số sử dụng `SCREAMING_SNAKE_CASE`
- Với các hàm trả về với giá trị Boolean, giống như `Array#empty?`, tên hàm cần thêm dấu `?` ở cuối
- Những method ghi đè phá huỷ `self` thì thêm `!` ở cuối tên hàm

```ruby
class Array
  def flatten_once!
    res = []

    each do |e|
      [*e].each { |f| res << f }
    end

    replace(res)
  end

  def flatten_once
    dup.flatten_once!
  end
end
```

### Exceptions

- Sử dụng `raise` thay vì `fail`

```ruby
# bad
fail SomeException, 'message'

# good
raise SomeException, 'message'
```

- Sử dụng exception với class và message như 2 tham số với `raise` thay vì sử dụng Exceprion Instance

```ruby
# bad
raise SomeException.new('message')
# Note that there is no way to do `raise SomeException.new('message'), backtrace`.

# good
raise SomeException, 'message'
# Consistent with `raise SomeException, 'message', backtrace`.
```

- Sử dụng `implicit begin block` nếu có thể

```ruby
# bad
def foo
  begin
    # main logic goes here
  rescue
    # failure handling goes here
  end
end

# good
def foo
  # main logic goes here
rescue
  # failure handling goes here
end
```

### Comments

- Sử dụng 1 dấu space sau `#`
- Tránh comment dư thừa

```ruby
# bad
counter += 1 # Increments counter by one.
```

- Comment cũng cần được update với code, nếu comment không update cùng với xử lý thì thà không viết còn hơn

- Sử dụng 1 số anotation để đánh dấu khi cần thiết
  - `TODO`: note lại các tính năng chưa hoàn thành cần làm sau
  - `FIXME`: note lại lỗi đang tồn tại, cần sửa
  - `OPTIMIZE`: note lại vị trí xử lý chậm ảnh hưởng tới hiệu năng