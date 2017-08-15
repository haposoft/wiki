# REST API

## Input

### 1. Create

- Sử dụng method: `POST`.
- Url bao gồm tên model và `/create`.  
Ví dụ: `/posts/create`, `users/create`

### 2. Read

- Sử dụng method: `GET`
- Url bao gồm tên model và `id`, `slug` ... (key để có thể truy xuất được từ database).  
Ví dụ: `/posts/1`, `users/1`, `/customers/12345/orders`

### 3. Update

- Sử dụng method: `PUT`
- Url bao gồm tên model và `id`, `slug` ... (key để có thể truy xuất được từ database).
Ví dụ: `/posts/1`, `users/1`, `/customers/12345/orders/2`

### 4. Delete

- Sử dụng method: `DELETE`
- Url bao gồm tên model và `id`, `slug` ... (key để có thể truy xuất được từ database).
Ví dụ: `/posts/1`, `users/1`, `/customers/12345/orders/2`

## Response

### Status code
Một vài status code thông dụng :
- Action `Create` success : `201`
- Action `Read` success : `200`
- Action `Update` success : `200`
- Action `Delete` success : `200`
- Bad Request : `400`
- Unauthorized : `401`
- Forbidden : `403`
- Not Found : `404`
- Method Not Allowed : `405`
- Internal Server Error : `500`
- Not Implemented : `501`
- Bad Gateway : `502`
- Service Unavailable : `503`
- Gateway Timeout : `504`

## Cấu trúc response trả về

Data trả về sẽ dưới dạng json, `Status code` sẽ cho biết kết quả của request đó.  
Cấu trúc json sẽ theo format dưới đây :  

```
    message : 'Success',
    data : {
        'user' : {
            id: 1,
            name: 'Haposoft',
            ...
        },
        ...
    }
```
- 2 key chính bắt buộc là `message` và `data`. 
- Trong trường hợp request thực hiện thành công hoặc 
có lỗi thì nội dung thông báo lỗi sẽ được trả về trong `message`.
- Các nội dung data trả về sẽ được liệt kê trong object `data` với các key tương ứng với nội dung của data.