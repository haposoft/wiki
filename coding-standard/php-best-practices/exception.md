# Xử lý lỗi
- Sử dụng cơ chế xử lý lỗi trong PHP để bắt và xử lý các lỗi một cách chính xác. Đảm bảo rằng mã của bạn có khả năng xử lý các tình huống lỗi và cung cấp thông báo lỗi dễ hiểu.
    ```php
        <?php
        // Mã "bad"
        $number1 = 10;
        $number2 = 0;
        $result = $number1 / $number2;
        echo "Kết quả: " . $result;
        ?>
    ```
    - Trong ví dụ trên, chúng ta chia một số cho 0, gây ra lỗi chia cho 0 (division by zero). Mã này không xử lý lỗi và sẽ gây ra một lỗi ngoại lệ (exception) không được xử lý một cách chính xác gây khó khăn cho người dùng hoặc dev fix

        ```php
            <?php
            // Mã "good"
            $number1 = 10;
            $number2 = 0;
            try {
            if ($number2 === 0) {
            throw new Exception("Số bị chia không thể là 0.");
            }
            $result = $number1 / $number2;
            echo "Kết quả: " . $result;
            } catch (Exception $e) {
            echo "Đã xảy ra lỗi: " . $e->getMessage();
            }
            ?>
        ```
    - Trong ví dụ này, chúng ta đã sử dụng cơ chế xử lý lỗi trong PHP bằng cách sử dụng câu lệnh try-catch. Chúng ta chỉ đơn giản in ra thông báo lỗi, nhưng bạn cũng có thể thực hiện các xử lý khác như ghi log, gửi email thông báo lỗi, hoặc chuyển hướng người dùng đến trang lỗi
# Quản lý exception
- Sử dụng các cấu trúc try-catch để xử lý ngoại lệ một cách rõ ràng và kiểm soát các lỗi không mong muốn. Điều này giúp ứng dụng của bạn trở nên bền vững và dễ bảo trì.
    ```php
        <?php
        function divideNumbers($number1, $number2) {
        if ($number2 === 0) {
        echo "Lỗi: Số bị chia không thể là 0.";
        return;
        }
        $result = $number1 / $number2;
        echo "Kết quả: " . $result;
        }

        divideNumbers(10, 0);
        ?>
    ```
    - Trong ví dụ trên, chúng ta kiểm tra điều kiện trước khi thực hiện phép chia và in ra thông báo lỗi nếu số bị chia là 0. Tuy nhiên, việc in ra thông báo lỗi trực tiếp trong hàm divideNumbers() là một cách xử lý lỗi không tốt. Nếu chúng ta muốn xử lý lỗi khác hoặc thay đổi cách thông báo lỗi, chúng ta phải sửa đổi mã nguồn của hàm này.

        ```php
        <?php
        function divideNumbers($number1, $number2) {
        if ($number2 === 0) {
        throw new Exception("Số bị chia không thể là 0.");
        }
        $result = $number1 / $number2;
        return $result;
        }

        try {
        $result = divideNumbers(10, 0);
        echo "Kết quả: " . $result;
        } catch (Exception $e) {
        echo "Đã xảy ra lỗi: " . $e->getMessage();
        }
        ?>
        ```
- Trong ví dụ này, chúng ta sử dụng cấu trúc try-catch để quản lý ngoại lệ. Hàm divideNumbers() ném ra một ngoại lệ nếu số bị chia là 0. Trong khối try, chúng ta gọi hàm divideNumbers() và gán kết quả vào biến $result. Nếu có ngoại lệ xảy ra, khối catch sẽ được thực thi và chúng ta có thể xử lý ngoại lệ đó bằng cách in ra thông báo lỗi.