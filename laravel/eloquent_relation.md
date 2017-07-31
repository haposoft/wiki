#Eloquent Relation
## One to Many Relation 

## Many to Many Relation

Ví dụ: Ta có hai bảng tils và tags có quan hệ nhiều nhiều với nhau. Để định nghĩa quan hệ này trong Eloquent,
ta khai báo như function `tils` và `tags` như bên dưới:
``` 
 class Tag extends Model
 {
     protected $table = 'tags';
 
     /**
      * Many to Many relation
      *
      * @return \Illuminate\Database\Eloquent\Relations\belongToMany
       */
      public function tils()
      {
         return $this->belongsToMany(Til::class);
      }
  }
  ```
  ```
   class Til extends Model
 {
     protected $table = 'tils';
 
     /**
      * Many to Many relation
      *
      * @return \Illuminate\Database\Eloquent\Relations\belongToMany
       */
      public function tags()
      {
         return $this->belongsToMany(Tag::class);
      }
  }
  ```


Đối với many to many relation (n-n), Laravel thường mặc định bảng lưu lại quan hệ theo thứ tự alphabet(alphabetical order).
Ví dụ bảng `tils` và `tags` có quen hệ n-n với nhau thì bảng lưu quan hệ giữa chúng sẽ là `tag_til` 
chứ không phải là `til_tag`, nên đặt tên theo rule của Laravel sẽ ít cần config hơn.

Ngoài ra, có thể chỉ định tên của bảng chứa quan hệ này, 
bằng cách thêm params thứ 2 vào hàm `belongsToMany` của cả hai Eloquent class.
Ví dụ: muốn chỉ định bảng quan hệ nhiều nhiều giữa Tag và Til là bảng `til_tag`: 
```
return $this->belongsToMany(Til::class, 'til_tag');
```

```
return $this->belongsToMany(Tag::class, 'til_tag');
```

## Polymorphic Relation 
