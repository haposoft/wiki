#Laravel best practices

### **Nguyên tắc Đơn nhiệm - Single responsibility principle**

Class và method chỉ nên chịu 1 trách nhiệm.
Khi có các xử lý phức tạp thì nên tách ra thành các class, method mới để chịu trách nhiệm cho phần xử lý đó.

```php
public function getFullNameAttribute()
{
    if (auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified()) {
        return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
    } else {
        return $this->first_name[0] . '. ' . $this->last_name;
    }
}
```

Đoạn code trên có quá nhiều đoạn xử lý phức tạp nên được tách ra thành các function nhỏ hơn để chịu các trách nhiệm 
tương ứng.

```php
public function getFullNameAttribute()
{
    return $this->isVerifiedClient() ? $this->getFullNameLong() : $this->getFullNameShort();
}

public function isVerifiedClient()
{
    return auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified();
}

public function getFullNameLong()
{
    return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
}

public function getFullNameShort()
{
    return $this->first_name[0] . '. ' . $this->last_name;
}
```

### **Validation**

Không thực hiện việc validate trong controller như dưới đây:

```php
public function store(Request $request)
{
    $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
        'publish_at' => 'nullable|date',
    ]);

    ....
}
```

Phải tách riêng thành 1 class chịu trách nhiệm validate như sau:

```php
public function store(PostRequest $request)
{    
    ....
}

class PostRequest extends Request
{
    public function rules()
    {
        return [
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
            'publish_at' => 'nullable|date',
        ];
    }
}
```

### **Don't repeat yourself (DRY)**

Khi có các đoạn code xử lý mà bị lặp lại từ 2 lần trở lên cần xem xét lại để viết code sao cho có thể thể dễ dàng tái 
sử dụng, tránh việc lặp code.
Bằng cách tận dụng sức mạnh của [Blade Templates](https://laravel.com/docs/master/blade),
[Eloquent scopes](https://laravel.com/docs/master/eloquent#query-scopes),...

```php
public function getActive()
{
    return $this->where('verified', 1)->whereNotNull('deleted_at')->get();
}

public function getArticles()
{
    return $this->whereHas('user', function ($q) {
            $q->where('verified', 1)->whereNotNull('deleted_at');
        })->get();
}
```

Dễ dàng nhận thấy đoạn code `->where('verified', 1)->whereNotNull('deleted_at')` bị lặp và có thể viết lại như sau:

```php
public function scopeActive($q)
{
    return $q->where('verified', 1)->whereNotNull('deleted_at');
}

public function getActive()
{
    return $this->active()->get();
}

public function getArticles()
{
    return $this->whereHas('user', function ($q) {
            $q->active();
        })->get();
}
```

### **Mass assignment**

Tận dụng tối đa [Mass Assignment](https://laravel.com/docs/master/eloquent#mass-assignment) trong mọi trường hợp để tối 
giản code và tăng cường tính bảo mật.

```php
$article = new Article;
$article->title = $request->title;
$article->content = $request->content;
$article->verified = $request->verified;
// Add category to article
$article->category_id = $category->id;
$article->save();
```

Thay vì gán từng giá trị cho các property tương ứng chúng ta làm đơn giản hơn

```php
$category->article()->create($request->validated());
```

### **Eager Loading**

Sử dụng [Eager Loading](https://laravel.com/docs/master/eloquent-relationships#eager-loading) để tránh bị (N + 1) query 
trong các trường hợp cần truy xuất dữ liệu của các quan hệ. 

```php
$users = User::get();

...

@foreach ($users as $user)
    {{ $user->profile->name }}
@endforeach
```

Trong trường hợp trên khi truy xuất thông tin profile của 1 user thông qua quan hệ thì mỗi user sẽ mất 1 câu query.
Chúng ta có thể viết lại như sau:

```php
$users = User::with('profile')->get();

...

@foreach ($users as $user)
    {{ $user->profile->name }}
@endforeach
```

### **Không viết JS và CSS trong Blade templates, không viết HTML trong PHP class**

Không viết đoạn code JS trong các view 

```javascript
let article = `{{ json_encode($article) }}`;
```

Nên gán giá trị vào các `input` kiểu `hidden` hoặc các `attribute` và lấy giá trị thông qua các input và attribute này

```html
<input id="article" type="hidden" value="@json($article)">

Or

<button class="js-fav-article" data-article="@json($article)">{{ $article->name }}<button>
```

### **Sử dụng các giá trị lấy từ config hoặc các constants thay vì hardcode**

```php
public function isNormal()
{
    return $article->type === 'normal';
}

public function isAdmin()
{
    return $user->type === 1;
}

return back()->with('message', 'Your article has been added!');
```

Không sử dụng `string`  hoặc `number` để kiểm tra các điều kiện và hardcode các đoạn text mà sử dụng các `const` và lấy 
text từ trong các language files

```php
public function isNormal()
{
    return $article->type === Article::TYPE_NORMAL;
}

public function isAdmin()
{
    return $user->type === USER::TYPE_ADMIN;
}

return back()->with('message', __('app.article_added'));
```

### **Không lấy dữ liệu trực tiếp từ `.env`**

```php
$apiKey = env('API_KEY');
```

Thay vì lấy dữ liệu trực tiếp từ `.env` truyền data sang `config` tương ứng và sau đấy dùng hàm `config()` để lấy giá trị.
Nên set các giá trị mặc định nếu có.

```php
// config/api.php
'key' => env('API_KEY'),

// Use the data
$apiKey = config('api.key');
```
