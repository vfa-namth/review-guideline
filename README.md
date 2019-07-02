# PHP Standard Style

## 1. Tại sao phải sử dụng các quy chuẩn của PHP(PSR):

### Lý do bạn nên viết code theo tiêu chuẩn PSR:

- Dù mỗi dev có 1 cách code khác nhau và code vẫn chạy ổn định, nhưng nếu số lượng dev tăng lên quá lớn, lượng code dự án sẽ trở nên lộn xộn và khó kiểm soát.
- PSR là tiêu chuẩn code được áp dụng vào các dự án lớn hoặc framework PHP (Zend, Laravel, Cakephp, Composer, Phalcon, Magento,Opencart …).
- Viết code chuẩn giúp bạn và đồng đội dễ dàng hiểu code của nhau.
- Thống nhất chung về cách thức viết code, tổ chức các class,…
- Dễ dàng đọc, hiểu, trình bày khỏi mất công bản thân "tự chế" kiểu code không giống ai.
- Vì vậy với 1 quy chuẩn chung trong dự án, nó sẽ giúp: + Cải thiện khả năng đọc/review code. + Việc bảo trì, phát triển code dễ dàng hơn. + Và Quốc có Quốc pháp, Code có Code quy!

### PSR là gì?

Đây là chuẩn code chung tất cả các lập trình viên code PHP thì ít nhất cũng phải nên xem 1 lần, ở đây mình chỉ nói sơ qua những ý chính, còn cụ thể và chi tiết hơn thì các bạn nên lên trang chủ xem nhé [link](http://www.php-fig.org/psr/).

- PSR có nghĩa là PHP Standards Recommendations, nó là tiêu chuẩn được khuyến nghị áp dụng khi lập trình PHP và được các lập trình viên, tổ chức chấp nhận sử dụng.
- PSR được soạn thảo, đánh giá và khuyến khích sử dụng bởi một nhóm chuyên gia PHP những người phát triển cho các Framework và hệ thống PHP phổ biến (thành viên PSR).
- PSR bao gồm 20 chuẩn, nhưng ở đây mình chỉ nói 3 chuẩn là PSR-1, PSR-2, PSR-3(Đây là 3 chuẩn bất kỳ người nào review code PHP cần phải nắm rõ). - PSR-1: Basic Coding Standard (Tiêu chuẩn cơ bản khi viết code PHP). - PSR-2: Coding Style Guide (Tiêu chuẩn trình bày code). - PSR-3: Logger Interface (Giao diện logger).
  > Chú ý: Các bạn nên đọc để hiểu hết 17 chuẩn còn lại nhé.

## 2. Các chuẩn cơ bản cần tuân thủ khi review PHP(PSR):

### 2.1. PSR-1: Basic Coding Standard

#### 2.1.1. Overview

- Các file code PHẢI sử dụng thẻ <?php hoặc <?
- File code PHP sử dụng encode: UTF-8 without BOOM
- Các Files NÊN hoặc dùng để khai báo các thành phần PHP (các lớp, hàm, hằng …) hoặc dùng với mục đích làm hiệu ứng phụ (như include, thiết lập ini cho PHP …), nhưng KHÔNG NÊN dùng cả 2 cùng lúc trong 1 file (Xem ví dụ này ở Ví dụ 1)
- Các Namespace và classes PHẢI theo chuẩn “autoloading” PSR: [PSR-4]
- Tên lớp PHẢI có dạng NameClass (chữ không nameclass, Nameclass, namClass …)
- Hằng số trong class tất cả PHẢI viết HOA và chia ra bởi dấu \_ (ví dụ ahdsoft_member).
- Tên phương thức của lớp PHẢI ở dạng camelCase (từ đầu viết thường, ví dụ: helloWorld).

#### 2.1.2. Files

#### 2.1.2.1. PHP Tags

- Các file code PHẢI sử dụng thẻ `<?php` hoặc `<?`, nguyên tắc này khá đơn giản phải không nào, đầu file php phải bắt đầu bằng `<?php` nếu dùng short tag thì sẽ là `<?= ?>`;

#### 2.1.2.2. Character Encoding

- File code PHP sử dụng encode: UTF-8 without BOM

#### 2.1.2.3. Side Effects

- Các Files NÊN dùng để khai báo các thành phần PHP (các lớp, hàm, hằng …) hoặc dùng với mục đích làm Side Effects (như include, thiết lập ini cho PHP …), nhưng KHÔNG NÊN dùng cả 2 cùng lúc trong 1 file.
- Side Effects là có nghĩa là thực hiện logic không liên quan trực tiếp đến khai báo lớp, hàm, hằng số, v.v. Xem ví dụ nhé các bạn:

  ````
  <?php
  // Side Effects: đổi thiết lập ini
  ini_set('error_reporting', E_ALL);

      	// Side Effects: nạp file vào
      	include "file.php";

      	// Side Effects: xuất dữ liệu
      	echo 'https://chungnguyen.xyz';

      	// khai báo hàm
      	function foo()
      	{
      		// function body
      	}
      	```

  > Như vậy trong file php trên vừa kèm hiệu ứng phụ lại vừa có khai báo hàm trong file như vậy là không nên thôi các bạn nhé, còn đúng thì code chạy được là đúng rồi. Như vậy ở ví dụ trên mình sẽ tách phần khai báo hàm ra một file riêng có tên common.php

      	```
      	<?php
      	// khai báo hàm
      	function foo()
      	{
      		// function body
      	}

      	// điều kiện không phải là hiệu ứng phụ nhé
      	if (! function_exists('bar')) {
      		// khai báo hàm
      		function bar()
      		{
      			// function body
      		}
      	}
      	```

  > Như vậy file php bị vi phạm nguyên tắc trên được sửa thành:

      	```
      	<?php
      	// hiệu ứng phụ: đổi thiết lập ini
      	ini_set('error_reporting', E_ALL);

      	// hiệu ứng phụ: nạp file vào
      	include "file.php";

      	// hiệu ứng phụ: xuất dữ liệu
      	echo 'https://chungnguyen.xyz';

      	// hiệu ứng phụ: nạp file vào
      	include "common.php";
      	```
      	>Trong file toàn bộ là Side Effects vậy là ok rồi phải không nào các bạn
  ````

#### 2.1.3. Namespace and Class Names

- Namespace và lớp PHẢI theo chuẩn “autoloading” PSR: [[PSR-0](https://www.php-fig.org/psr/psr-0/), [PSR-4](https://www.php-fig.org/psr/psr-4/)].
- Có nghĩa là mỗi lớp được khai báo trên mỗi file PHP riêng và namespace tối thiểu có một cấp, cấp đầu là tên vendor.
- Tên lớp lại PHẢI đúng dạng StudlyCaps nha.
- Code được viết cho PHP 5.3 trở về sau PHẢI sử dụng các namespace.

#### 2.1.4. Class Constants, Properties, and Methods

Thuật ngữ "Class" liên quan đến tất cả các lớp, interfaces và traits.

#### 2.1.4.1. Constants

- Hằng phải viết HOA toàn bộ và dùng dấu gạch ngang để ngăn cách nhé
- Ví dụ bạn định đặt một hằng có ý nghĩa là: "Tôi đẹp trai" thì như thế nào ?

  ````
  <?php
  namespace Vendor\Model;

      	class Foo
      	{
      	    const VERSION = '1.0';
      	    const DATE_APPROVED = '2012-06-01';
      	    const TOI_DEP_TRAI = true;
      	}
      	```
  ````

#### 2.1.4.2. Properties

- Về cách thức đặt tên thuộc tính chuẩn PSR-1 không quy định cụ thể là nên đặt loại nào, nhưng khuyên bạn chọn loại nào thì dùng nhất quán luôn, cụ thể có một số chuẩn đặt tên thuộc tính như sau:
  `$DayLaThuocTinh: kiểu này viết hoa mấy chữ cái đầu $dayLaThuocTinh: kiểu này là kiểu lạc đà, chữ đầu tiên viết thường, mấy chữ sau viết hoa chữ cái đầu. $day_la_thuoc_tinh: kiểu này là underscore, viết thường hết và ngăn cách bằng dấu gạch dưới.` >Thông tin thêm: Laravel Framework chọn cách số 2 để đặt tên cho thuộc tính

#### 2.1.4.3. Methods

- Toàn bộ các hàm (chú ý: hàm này là hàm trong lớp nha các bạn) phải đặt tên theo kiểu lạc đà (camelCase()).

### 2.2. PSR-2: Coding Style Guide

#### 2.2.1. Overview

- Code PHẢI tuân thủ PSR-1
- Code PHẢI sử dụng 4 ký tự space để lùi khối (không dùng tab)
- Mỗi dòng code PHẢI dưới 120 ký tự, NÊN dưới 80 ký tự.
- PHẢI có 1 dòng trắng sau namespace, và PHẢI có một dòng trắng sau mỗi khối code.
- Ký tự mở lớp { PHẢI ở dòng tiếp theo, và đóng lớp } PHẢI ở dòng tiếp theo của thân class.
- Ký tự { cho hàm PHẢI ở dòng tiếp theo, và ký tự } kết thúc hàm PHẢI ở dòng tiếp theo của thân hàm.
- Các visibility (public, private, protected) PHẢI được khai báo cho tất cả các hàm và các thuộc tính của lớp;
- Các từ khóa điều khiển khối(if, elseif, else) PHẢI có một khoảng trống sau chúng; hàm và lớp thì KHÔNG ĐƯỢC làm như vậy.
- Mở khối { cho cấu trúc điều khiển PHẢI trên cùng một dòng; và đóng khối này } với ở dòng tiếp theo của thân khối.
- Hằng số true, false, null PHẢI viết với chữ thường.
- Từ khóa extends và implements phải cùng dòng với class.
- implements nhiều lớp, thì mỗi lớp trên một dòng
- keyword var KHÔNG ĐƯỢC dùng sử dụng khai báo property.
- Tên property KHÔNG NÊN có tiền tố \_ nhằm thể hiện thuộc protect hay private.
- Tham số cho hàm, phương thức: KHÔNG được thêm space vào trước dấu , và PHẢI có một space sau ,. Các tham số CÓ THỂ trên nhiều dòng, nếu làm như vậy thì PHẢI mỗi dòng 1 tham số.
- abstract, final PHẢI đứng trước visibility, còn static phải đi sau.

#### 2.2.2. Ví dụ

- Ở trên nói nhiều như thế nhưng đây là 1 ví dụ đầy đủ cho tất cả trường hợp trên.

  ````
  <?php
  namespace Vendor\Package;

      use FooInterface;
      use BarClass as Bar;
      use OtherVendor\OtherPackage\BazClass;

      class Foo extends Bar implements FooInterface
      {
          public function sampleMethod($a, $b = null)
         {
      	if ($a === $b) {
      		bar();
      	} elseif ($a > $b) {
      		$foo->bar($arg1);
      	} else {
      		BazClass::bar($arg2, $arg3);
      	}
          }

         final public static function bar()
         {
      	// method body
         }
      }
      ```

  Cụ thể chi tiết hơn thì các bạn xem link sau nhé: [PSR-2 Coding Style Guide](https://www.php-fig.org/psr/psr-2/)
  ````

### 2.3. PSR-3: Logger Interface

#### 2.3.1. Concept Logger

- Rất nhiều ứng dụng tự xây dựng cho mình các cơ chế ghi lại nhưng thông tin hoạt động của ứng dụng, đó là các dấu vết để sử dụng với nhiều mục đích, thường các thông tin ghi lại trên một (log file), cơ chế để có thể ghi lại thông tin mới mục đích giám sát hoạt động như vậy được gọi là logger.
- Trong tiêu chuẩn PSR-3 đưa ra giao diện mẫu dùng để xây dựng nên các thư viện Logger. Về cơ bản ứng dụng phải làm việc được với đối tượng tạo ra từ giao diện Psr\Log\LoggerInterface và ghi lại log ra file một cách đơn giản, sau đây là các vấn đề xoay quanh LoggerInterface.

#### 2.3.2. Specification

##### 2.3.2.1. Basics

- Giao diện LoggerInterface đưa ra tám cấp độ khi ghi lại các log gồm có: debug, info, notice, warning, error, critical, alert, emergency mỗi mức độ này có một hàm cùng tên tương ứng. Có một hàm thứ chín tên là log nó chấp nhận cấp độ như tham số để ghi lại log. Tiêu chuẩn đưa ra là việc gọi hàm log đi kèm tham số là hằng số cấp độ PHẢI có kết quả tương ứng với gọi hàm thành phần (8 hàm trên). Khi gọi hàm này với hằng số cấp độ không được định nghĩa thì throw một exception Psr\Log\InvalidArgumentException.

##### 2.3.2.1. Message

- Mọi phương thức của giao diện đều có chấp nhận một chuỗi ký tự như là thông điệp cần ghi lại, hoặc một đối tượng có hàm \_\_toString(), khi triển khai giao diện CÓ THỂ đưa ra các sử lý đặc biệt cho các đối tượng chuyển đến, nếu không đưa ra thì lớp triển khai cần chuyển đối tượng (cast) thành chuỗi.
- Các message chuyển đến hàm log có thể có chứa các placeholder (giữ chỗ), lớp triển khai CÓ THỂ thay thế các placeholder bằng các giá trị từ một mảng chuyển tới.
- Các tên placeholder PHẢI tương ứng với key của mảng dữ liệu chuyển tới. Tên này trong message PHẢI được xác định bắt đầu từ ký tự { và kết thúc bởi }. KHÔNG ĐƯỢC CÓ khoảng trắng trong tên placeholder, và NÊN sử dụng các ký tự A-Z a-z 0-9 \_ . các ký tự khác để dành.
- Đây là một ví dụ về placeholder dùng để cập nhật mảng `$context` vào `$message` tham khảo:

  ````
  <?php

      	function interpolate($message, array $context = array())
      	{
      	    $replace = array();
      	    foreach ($context as $key => $val) {
      		// check that the value can be casted to string
      	        if (!is_array($val) && (!is_object($val) || method_exists($val, '__toString'))) {
      		    $replace['{' . $key . '}'] = $val;
      	        }
      	    }

      	    return strtr($message, $replace);
      	}

      	$message = "User {username} created";

      	$context = array('username' => 'bolivar');

      	echo interpolate($message, $context);
      	```
  ````

##### 2.3.2.3. Context

- Mọi phương thức đều chấp nhận một mảng dữ liệu (gọi là context), về nguyên tắc mảng có thể chứa bất kỳ thứ gì. Lớp triển khải PHẢI đảm bảo xử lý thỏa đáng dữ liệu context này ngoài ra các giá trị trong context KHÔNG ĐƯỢC phát sinh các exceptions.

##### 2.3.2.4. Package

- Từ các khái niệm, yêu cầu tiêu chuẩn ở trên, đây là các giao diện mẫu bạn cần áp dụng để tuân thủ PRS-3.

      ```
      <?php

      namespace Psr\Log;

      interface LoggerInterface
      {

         public function emergency($message, array $context = array());

         public function alert($message, array $context = array());

         public function critical($message, array $context = array());

         public function error($message, array $context = array());

         public function warning($message, array $context = array());

         public function notice($message, array $context = array());

         public function info($message, array $context = array());

         public function debug($message, array $context = array());

         public function log($level, $message, array $context = array());
      }
      ```
      ```
      <?php

      namespace Psr\Log;
      interface LoggerAwareInterface
      {

      	public function setLogger(LoggerInterface $logger);
      }
      ```
      ```
      <?php

      namespace Psr\Log;
      class LogLevel
      {
          const EMERGENCY = 'emergency';
          const ALERT     = 'alert';
          const CRITICAL  = 'critical';
          const ERROR     = 'error';
          const WARNING   = 'warning';
          const NOTICE    = 'notice';
          const INFO      = 'info';
          const DEBUG     = 'debug';
      }
      ```

  > Các bạn hãy xem chi tiết tại đây nhé [link](https://www.php-fig.org/psr/psr-3/)

---

# Khái niệm review chéo:

### 1. Tại sao phải review chéo:

- Dự án quá lớn với nhiều tính năng có độ phức tạp cao, mỗi developer chỉ có thể đảm nhận 1 tính năng đó.
- Số lượng developer tăng lên, với nhiều stype code khác nhau.
- Trong team luôn có những cấp độ code khác nhau, người giỏi logic, người tốt cách trình bày,...

### 2. Cách thực hiện:

- Có 1 review Leader, nhận trách nhiệm review toàn bộ PR của các dev, bên cạnh đó assing thêm 1 (hoặc có thể hơn) developer vào review cùng.
- Reviewer kỳ vọng chỉ ra được những điểm cần cải thiện.
- Nếu là tích cực, hãy để lại một tín hiệu tốt hay một lời khen nào đó, điều này tăng hiệu ứng cho coder làm việc.
- Nếu có vấn đề, cần chỉ rõ, diễn tả tốt và nếu có thể, nên gợi ý luôn cách làm của reviewer cho PR đó.
- Để đạt được hiệu quả tốt mang tính xây dựng, nên chia nhỏ các PR để review dễ dàng hơn, ngoại trừ những trường hợp bất khả kháng.

### 3. Hiệu quả đạt được:

- Khả năng đồng bộ code và thông tin dự án của các thành viên tăng lên, sẵn sàng cho các trường hợp "Lấp lỗ trống".
- Review tốt giúp kiểm soát được sự đồng đều trong chất lượng code và các stype code.
- Đảm bảo được đầu ra cuối cùng của dự án luôn là hoàn thiện nhất.
- Trình độ và khả năng giữa các developer có thể tăng lên nhờ sự học hỏi lẫn nhau.

### 4. Gợi ý mẫu các bước khi review 1 PR bao gồm:

- Kiểm tra thông tin PR(Pull request), bao gồm title, description, labels, reviewer đúng chuẩn, đúng yêu cầu.
- Nắm các chuẩn/quy tắc riêng với từng dự án cụ thể (role riêng của dự án).
- Đọc/nắm nội dung/yêu cầu của Task.
- Review logic song song với review standard PHP.
- Check pass/fail của CI/CD nếu có trên PR(Pull request).
