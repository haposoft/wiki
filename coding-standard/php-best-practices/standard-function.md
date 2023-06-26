# Sử dụng các hàm chuẩn
- Hãy tận dụng các hàm chuẩn của PHP để giảm sự lặp lại và tăng tính module hóa của code. Các hàm chuẩn bao gồm các chức năng xử lý chuỗi, mảng, thời gian và cơ sở dữ liệu
    ```php
        <?php
            // Mã "bad"
            $date = date('Y-m-d');
            $uppercaseName = strtoupper("John Doe");
            $arrayLength = count($myArray);
        ?>
    ```
    - Trong ví dụ trên, chúng ta thực hiện các xử lý chuỗi, thời gian và mảng bằng cách sử dụng các hàm được tích hợp sẵn trong PHP. Tuy nhiên, chúng ta không tận dụng các hàm chuẩn một cách tối đa và lại lặp lại các đoạn mã xử lý

- Mã "good"
    ```php
        <?php
        // Mã "good"
        $date = date('Y-m-d');
        $uppercaseName = strtoupper("John Doe");
        $arrayLength = count($myArray);

        // Sử dụng các hàm chuẩn để tăng tính module hóa của code
        function getCurrentDate() {
            return date('Y-m-d');
        }

        function convertToUppercase($string) {
            return strtoupper($string);
        }

        function getArrayLength($array) {
            return count($array);
        }

        // Sử dụng các hàm chuẩn để thực hiện xử lý
        $date = getCurrentDate();
        $uppercaseName = convertToUppercase("John Doe");
        $arrayLength = getArrayLength($myArray);
        ?>
    ```
    - Trong ví dụ này, chúng ta đã tận dụng các hàm chuẩn để giảm sự lặp lại và tăng tính module hóa của code. Chúng ta đã tạo ra các hàm getCurrentDate(), convertToUppercase(), và getArrayLength() để thực hiện các xử lý tương ứng. Bằng cách này, chúng ta chỉ cần gọi các hàm này để thực hiện các xử lý, thay vì lặp lại các đoạn mã xử lý trong nhiều nơi.

    - Sử dụng các hàm chuẩn giúp giảm sự lặp lại mã nguồn, tăng tính module hóa và dễ bảo trì. Ngoài ra, nếu cần thay đổi logic xử lý, chúng ta chỉ cần sửa đổi một lần trong hàm tương ứng, không cần phải sửa đổi từng đoạn mã được lặp lại trong code.