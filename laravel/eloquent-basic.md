 
# Eloquent

- [1. Giới thiệu](#introduction)
- [2. Tạo models](#defining-models)
- [3. Các quy tắc mặc định của Eloquent model](#eloquent-model-conventions)
	- [Tên bảng](#table-name)
	- [Khóa chính](#primary-key)
	- [Timestamps](#timestamps)
- [4. Các hàm lấy dữ liệu từ DB hay sử dụng](#retrieving-models)
- [5. Thêm và cập nhật models](#insert-update-model)
- [6. Xoá model](#deleting-models)
    - [Soft Deleting](#soft-deleting)
    - [Thực hiện query với soft delete records](#querying-soft-deleted-models)

<a name="introduction"></a>
## 1. Giới thiệu

Eloquent là một phương tiện cung cấp bởi Laravel để giúp chúng ta làm việc với database. Mỗi bảng trong database tương ứng với một Model. Model giúp chúng ta truy vấn dữ liệu trong các bảng, cũng như thêm dữ liệu mới vào bảng.
Trước khi bắt đầu, hãy chắc chắn rằng bạn đã cài đặt thông tin database trong file `.env`

<a name="defining-models"></a>
## 2. Tạo model

Artisan queries:

```php
// tạo model User trong app/Http
php artisan make:model User

// tạo model đồng thời tạo file migration trong database/migrations
php artisan make:model User --migration
php artisan make:model User -m
```
<a name="eloquent-model-conventions"></a>
## 3. Các quy tắc mặc định của Eloquent model
<a name="table-name"></a>
#### Tên bảng
Mặc định, Model tên là `User` sẽ tương ứng với bảng `users`, Model `Student` sẽ tương ứng với bảng `students` và tương tự thế ...

Để thay đổi tên bảng mà Model tương tác, sử dụng thuộc tính `protected $table`

```php
class Flight extends Model
{
   	/**
	* The table associated with the model.
	*
	* @var string
	*/
	protected $table = 'my_flights';

	public function index(){
		//....
	}
	
	//....
}
```

<a name="primary-key"></a>
#### Khóa chính

Eloquent mặc định là mỗi bảng có một primary key tên là `id`. Để thay đổi primary key sử dụng thuộc tính `protected $primaryKey`.

Ngoài ra, Eloquent mặc định rằng primary key là 1 biến int tự tăng (incremeting). Để thay đổi dùng thuộc tính `public $incrementing` và `protected $keyType`.

```php
{
	public $incrementing = false;
	protected $keyType = 'string';
	protected $primaryKey = 'indentify';	

	public function index(){
		//....
	}
	//....
}
```

<a name="timestamps"></a>
#### Timestamps
Mặc định, Eloquent cần hai cột `created_at` và `updated_at` có mặt trong các table. Nếu bạn không muốn những columns này tự động được quản lý bởi Eloquent, thiết lập thuộc tính `$timestamps` thành `false`:
```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Flight extends Model
{
    /**
     * Indicates if the model should be timestamped.
     *
     * @var bool
     */
    public $timestamps = false;
}
```
Nếu bạn muốn thay đổi định dạng của timestamp, thay đổi thuộc tính `protected $dateFormat` trong model. Thuộc tính này xác định cách mà các thuộc tính kiểu date được lưu trong database cũng như cách format khi được serialize thành array hay JSON:

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Flight extends Model
{
    /**
     * The storage format of the model's date columns.
     *
     * @var string
     */
    protected $dateFormat = 'U';
}
```

<a name="retrieving-models"></a>
## 4. Các hàm lấy dữ liệu từ DB hay sử dụng

- #### `all()`: Lấy toàn bộ bản ghi

```php
$flights = App\Flight::all();
```
- #### `get()`: Lấy dữ liệu qua query builder

```php
$flights = App\Flight::where('active', 1)
               ->orderBy('name', 'desc')
               ->take(10)
               ->get();
```
> Vì các Eloquent models thực chất cũng là query builders, bạn có thể sử dụng tất cả các hàm của query builder qua Eloquent model.

- #### `chunk()`: Lấy 1 số lượng bản ghi nhất định

```php
App\Flight::chunk(200, function($flights){
	foreach($flights as $flight){
		// ....
	}
}
```
- #### `cursor()`: Sử dụng khi thao tác với bảng có lượng bản ghi lớn để giảm lượng bộ nhớ cần dùng

```php
foreach (Flight::where('foo', 'bar')->cursor() as $flight) {
    //
}
```

> `cursor` sử dụng [`PHP Generator`](https://viblo.asia/p/su-dung-php-generators-trong-cai-thien-hieu-nang-cua-ung-dung-web-MLzGObXxvpq) để thao tác với dữ liệu

- #### Lấy 1 bản ghi duy nhất: `find`, `first`, `findOrFail`, `firstOrFail`
 
```php
// Sử dụng primary key
$flight = App\Flight::find(1);

// Lấy bản ghi đầu tiên phù hợp điều kiện
$flight = App\Flight::where('active', 1)->first();

// Trường hợp primary key là nhiều trường, sử dụng mảng các primary key
$flight = App\Flight::find([1, 2, 3]);

// Lấy về bản ghi đầu tiên hoặc trả về 1 Exception nếu thất bại
$model = App\Flight::findOrFail(1);
$model = App\Flight::where('legs', '>', 100)->firstOrFail();
```
> Exception do `findOrFail` và `firstOrFail` trả về là 1 instance của `Illuminate\Database\Eloquent\ModelNotFoundException`, nếu Exception này không được `catch`, một `404 status response` sẽ được trả về cho user. Vì thế bạn không bắt buộc phải kiểm tra để return `404` status khi dùng các hàm này 

- *Hàm trên tập hợp*: `sum`, `avg`, `max`, ...

```php
$count = App\Flight::where('active', 1)->count();

$max = App\Flight::where('active', 1)->max('price');
```
<a name="insert-update-model"></a>
## 5. Thêm và cập nhật Models
- #### `save()`: thêm hoặc cập nhật 1 bản ghi
 
```php
public function store(Request $request)
    {
        // Validate the request...

        $flight = new Flight;

        $flight->name = $request->name;

        $flight->save();
    }
```
> Nếu đã được khai báo trong db, các trường `created_at`(khi tạo mới) và `updated_at` của bảng được tự động thêm vào giá trị `current Datetime (thời gian hiện tại)` khi sử dụng hàm `save()`

Nếu bản ghi đã tồn tại trong DB, hàm `save()` cũng có thể dc dùng để update dữ liệu đó:

```php
$flight = App\Flight::find(1);

$flight->name = 'New Flight Name';

$flight->save();
```

- #### `update()`: update nhiều bản ghi cùng lúc

```php
// Hoãn tất cả chuyến bay có trạng thái active và điểm đến là `San Diego`

App\Flight::where('active', 1)
          ->where('destination', 'San Diego')
          ->update(['delayed' => 1]);
```

- #### Sử dụng hàm `create()`:

Phương thức này được sử dụng để lọc các thông tin nhạy cảm trước khi lưu vào database. Trước khi sử dụng hàm `create()`, bạn cần khai báo trường `$fillable` hay `$guarded` trong Model. 

Chỉ những trường được khai báo trong fillable được lưu vào database

```php
// App/Model/Flight

class Flight extends Model
{
    protected $fillable = ['name'];
}

// Somewhere, ex: FlightController
$flight = App\Flight::create(['name' => 'Flight 10']);
```
Nếu đã khởi tạo một đối tượng của Model, có thể sử dụng hàm `fill()` để gán giá trị các trường của Model instance thông qua 1 mảng, chỉ những trường khai báo trong `fillable` được gán giá trị.
```php
$flight->fill(['name' => 'Flight 22']);

// Lưu vào DB
$flight->save();
```
> Ngược lại với `fillable` là `guarded`, những trường được khai báo trong `guarded` không được lưu vào DB. Bạn chỉ nên sử dụng 1 trong 2 thuộc tính này.

- #### Một số hàm khác: 
	- `firstOrCreate`: Nếu chưa có thì tạo 1 bản ghi trong DB
	- `firstOrNew`: Nếu chưa có thì tạo 1 model, chưa lưu vào DB
	- `updateOrCreate`: Cập nhật hoặc tạo 1 bản ghi trong DB

```php
$flight = App\Flight::firstOrCreate(['name' => 'Flight 10']);

// Retrieve flight by name, or create it with the name and delayed attributes...
$flight = App\Flight::firstOrCreate(
    ['name' => 'Flight 10'], ['delayed' => 1]
);

// Retrieve by name, or instantiate...
$flight = App\Flight::firstOrNew(['name' => 'Flight 10']);

// Retrieve by name, or instantiate with the name and delayed attributes...
$flight = App\Flight::firstOrNew(
    ['name' => 'Flight 10'], ['delayed' => 1]
);

// If there's a flight from Oakland to San Diego, set the price to $99.
// If no matching model exists, create one.
$flight = App\Flight::updateOrCreate(
    ['departure' => 'Oakland', 'destination' => 'San Diego'],
    ['price' => 99]
);
```
<a name="deleting-models"></a>
## 6. Xóa Models

- #### Xóa qua 1 instance:
```php
$flight = App\Flight::find(1);

$flight->delete();
```
- #### Xóa qua primary key

```php
App\Flight::destroy(1);

App\Flight::destroy([1, 2, 3]);

App\Flight::destroy(1, 2, 3);
```
- #### Xóa qua query

```php
//Xóa toàn bộ bản ghi có active = 0
$deletedRows = App\Flight::where('active', 0)->delete();
```

<a name="soft-deleting"></a>
### Soft deleting
Thay vì thực sự xoá các bản ghi khỏi database, Eloquent cũng cung cấp kiểu `soft delete` (xoá mềm). Khi 1 model sử dụng `soft delete`, chúng được thêm một trường là deleted_at trong database table. Để kích hoạt `Soft Delete` cho một model, sử dụng trait `Illuminate\Database\Eloquent\SoftDeletes` trên model và thêm vào cột `deleted_at` vào trong thuộc tính `$dates` của model:

```php
class Flight extends Model
{
    use SoftDeletes;

    /**
     * The attributes that should be mutated to dates.
     *
     * @var array
     */
    protected $dates = ['deleted_at'];
}
```

Tất nhiên là bạn cần phải thêm cột `deleted_at` vào trong table. Điều này có thể thực hiện trong `migration` bằng hàm `softDeletes()` của `schema builder`:

```php
Schema::table('flights', function ($table) {
    $table->softDeletes();
});
```
Khi 1 model được set `Soft Delete`, khi bạn gọi hàm `delete()`, cột `deleted_at` sẽ được gán giá trị `current datetime (thời gian hiện tại)`. Và khi thực hiện query, các bản ghi đã được `soft deleted` sẽ tự động bị loại khỏi tất cả các kết quả query.

Để xác định nếu một model instance đã bị `soft delete` hay chưa, sử dụng hàm `trashed()`:

```php
if ($flight->trashed()) {
    //
}
```

<a name="querying-soft-deleted-models"></a>
### Thực hiện query các soft deleted records

#### Thêm các soft delete model vào kết quả
Bạn có thể làm các bản ghi đã soft delete xuất hiện trên tập kết quả bằng cách sử dụng hàm `withTrashed()`:

```php
$flights = App\Flight::withTrashed()
                ->where('account_id', 1)
                ->get();
```
#### Chỉ lấy các soft deleted records

```php
$flights = App\Flight::onlyTrashed()
                ->where('airline_id', 1)
                ->get();
```
#### Phục hồi các soft deleted records
Sử dụng hàm `restore()`
```php
$flight->restore();
```

```php
App\Flight::withTrashed()
        ->where('airline_id', 1)
        ->restore();
```
#### Xóa vĩnh viễn records trong soft delete model
Sử dụng hàm `forceDelete()`

```php
// Force deleting a single model instance...
$flight->forceDelete();

// Force deleting all related models...
$flight->history()->forceDelete();
```






