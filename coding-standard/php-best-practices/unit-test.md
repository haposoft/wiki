# clean code trong việc viết unit test
## 1. Sử dụng tên test case mô tả chính xác và rõ ràng:
- Tên phải nêu rõ mục tiêu và kỳ vọng của test

**bad**
```php
public function test1() {
    // ...
}
```
**good**
```php
public function testViewListContractSuccess() {
    // ...
}
```
## 2. Giới hạn mỗi test case chỉ kiểm tra 1 điều kiện
- Mỗi test case nên tập trung vào kiểm tra 1 tính năng, giúp dễ dàng xác định nguyên nhân khi test case không thành công.

**bad**
```php
public function testViewCreateSuccessAndCreateContractSuccess() {
    // ...
}
```
**good**
```php
public function testViewCreateContractSuccess() {
    // ...
}

public function testCreateContractSuccess() {
    // ...
}
```
## 3. Sử dụng dữ liệu mẫu cho việc khởi tạo và chuẩn bị dữ liệu
- Đảm bảo rằng dữ liệu được khởi tạo và chuẩn bị đúng cách trước khi thực hiện test case
- Sử dụng kiểu dữ liệu mẫu cho việc khởi tạo dữ liệu giúp giảm sự phức tạp và tăng tính nhất quán của test case

**bad**
```php
public function testFunctionAddItemToCartSuccess() {
    // Arrange
    $cart = new Cart();
    $item = new Item("Sample Item", 10.99);
    
    // Act
    $cart->addItem($item);
    
    // Assert
    $this->assertEquals(1, $cart->getItemCount());
}
```
**good**
```php
public function testFunctionAddItemToCartSuccess() {
    // Arrange
    $cart = new Cart();
    $item = $this->createSampleItem();
    
    // Act
    $cart->addItem($item);
    
    // Assert
    $this->assertEquals(1, $cart->getItemCount());
}

private function createSampleItem() {
    return new Item("Sample Item", 10.99);
}
```
## 4. Sử dụng helper functions để tránh lặp lại code:
- Nếu có một đoạn code được sử dụng nhiều lần trong các test case khác nhau, nên tạo các  helper functions để tái sử dụng code và giảm sự lặp lại.

**bad**
```php
public function testAddItemToCart() {
    // Arrange
    ...
    
    // Act
    $cart->addItem($item);
    
    // Assert
    $this->assertEquals(1, $cart->getItemCount());
    $this->assertTrue($cart->containsItem($item));
}

public function testRemoveItemFromCart() {
    // Arrange
    ...
    
    // Act
    $cart->removeItem($item);
    
    // Assert
    $this->assertEquals(0, $cart->getItemCount());
    $this->assertFalse($cart->containsItem($item));
}
```
**good**
```php
public function testAddItemToCart() {
    // Arrange
    ...
    
    // Act
    $cart->addItem($item);
    
    // Assert
    $this->assertCartContainsItem($cart, $item);
}

public function testRemoveItemFromCart() {
    // Arrange
    ...
    $cart->addItem($item);
    
    // Act
    $cart->removeItem($item);
    
    // Assert
    $this->assertCartDoesNotContainItem($cart, $item);
}

//helper function

private function assertCartContainsItem(Cart $cart, Item $item) {
    $this->assertEquals(1, $cart->getItemCount());
    $this->assertTrue($cart->containsItem($item));
}

private function assertCartDoesNotContainItem(Cart $cart, Item $item) {
    $this->assertEquals(0, $cart->getItemCount());
    $this->assertFalse($cart->containsItem($item))
}
```