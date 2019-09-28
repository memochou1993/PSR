PSR-12：增修程式碼風格指南
===

本文件所使用之「必須」、「不可」、「需要」、「應」、「不應」、「應該」、「不應該」、「推薦」、「可以」和「選擇性的」等描述性詞彙，在 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 有詳細的解釋。

## 1. 概述

這份指南擴充並取代了 PSR-2 程式碼風格指南，並要求遵守 PSR-1 基本程式寫作標準。

與 PSR-2 相同，這份指南的目的是為了降低在閱讀來自不同開發者的程式碼時，所產生的認知分歧，期許透過一組共享的規則來格式化 PHP 程式碼。

PSR-12 希望提供一種程式碼風格工具可以實現的設置方式，任何專案都可以聲明遵守這些程式碼風格，從而減少開發者的認知分歧，使得開發者可以輕鬆地協調不同專案。這份指南有助於當多個開發者在多個專案中協作時，使用同一套準則。因此，這份指南的好處不在於規則本身，而在於分享這些規則。

PSR-2 在 2012 年被接受，在那之後，PHP 語言做了一系列的改變，對程式碼風格指南造成了一些影響。雖然 PSR-2 非常全面地介紹了當時已經存在的 PHP 功能，但對於新功能的規範過於鬆散。因此，這份指南試圖在更現代的背景下描述並勘誤 PSR-2 的內容。

### 1.1 先前的語言版本

如果你的專案的 PHP 版本不支援這份指南的任何說明，你「可以」選擇忽略他們。

### 1.2 範例

以下程式碼包含了一些規則，可作為概覽。

```PHP
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
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
        // 方法內容
    }
}
```

## 2. 一般

### 2.1 基本程式寫作標準

程式碼「必須」遵循 PSR-1 中列出的所有規則。

PSR-1 中的術語 StudlyCaps「必須」被釐清為 PascalCase，表示所有單字的首字母為大寫，包括第一個單字。

### 2.2 檔案

所有的 PHP 檔案「必須」只能以 Unix LF 作為換行字元。

所有的 PHP 檔案「必須」以非空白行（non-blank line）結尾，並以單個 LF 終止。

在只包含了 PHP 程式碼的檔案中，「必須」省略結尾 `?>` 標籤。

### 2.3 行

「不可」強制限制行的長度。

行的長度的非強制性限制「必須」是 120 個字符。

每行「不應該」超過 80 個字符，如果超過的話，「應該」被拆分成每行不超過 80 個字符的行。

結尾「不可」有空白（trailing whitespace）。

除非明確禁止，否則「可以」添加一個空白行（blank lines）來提高程式碼的可閱讀性，並區分出相關的程式碼區塊。

每行「不可」超過一條陳述式。

### 2.4 縮排

程式碼中的每個縮排「必須」使用 4 個空格（spaces），「不可」使用 tabs 來縮排。

### 2.5 關鍵字和型別

所有 PHP 保留的關鍵字和型別「必須」使用小寫字母。

未來 PHP 版本中添加的任何關鍵字和型別「必須」使用小寫字母。

型別的關鍵字「必須」使用縮寫形式，以 `bool` 代替 `boolean`、以 `int` 代替 `integer`。

## 3. 宣告陳述式、命名空間和引入陳述式

所有的 PHP 檔案，頭部「可以」包含多個不同的區塊。每個區塊「必須」由一個空白行分隔，且區塊中「不可」包含空白行。

每個區塊「必須」按照以下順序，不相關的區塊可以省略。

- 起始 `<?php` 標籤。
- 檔案級別（file-level）的文件註解。
- 一個或多個宣告陳述式。
- 檔案的命名空間宣告。
- 一個或多個以類別為基礎的（class-based）`use` 引入陳述式。
- 一個或多個以函數為基礎的（function-based）`use` 引入陳述式。
- 一個或多個以常數為基礎的（constant-based）`use` 引入陳述式。
- 剩餘的程式碼。

當一個檔案混合了 HTML 和 PHP 程式碼時，上述的所有規則仍然適用。他們「必須」出現在文件的頭部，即使剩餘的程式碼包含 PHP 的結尾標籤，最後才是 HTML 和 PHP 的混合程式碼。

當 PHP 的起始 `<?php` 標籤位於檔案的第一行時，它「必須」獨占一行，且不添加其他陳述式，除非檔案中包含了其他的標記式語言。

引入陳述式「不可」以反斜線開始，而且「必須」是完整名稱。

以下是一個包含各種區塊的程式碼範例：

```PHP
<?php

/**
 * 這個檔案包含了一些程式碼風格。
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar 是一個範例類別。
 */
class FooBar
{
    // 其他程式碼
}
```

「不可」使用超過兩個深度的複合命名空間，以下程式碼是允許的最大複合深度：

```PHP
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

以下程式碼則不被允許：

```PHP
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

在包含標記式語言的檔案中，如果要在 PHP 起始標籤和結尾標籤中宣告嚴格模式（strict types），其陳述式「必須」在檔案頭部的第一行，並且包含起始標籤、嚴格模式的宣告和結尾標籤。

例如：

```PHP
<?php declare(strict_types=1) ?>
<html>
<body>
    <?php
        // 其他程式碼
    ?>
</body>
</html>
```

宣告陳述式「必須」明確地使用 `declare(strict_types=1)` （與一個「選擇性的」分號結束），且「不可」包含空格。

宣告陳述式可以作為一個區塊，「必須」呈現如下，特別留意大括號和空白的位置：

```PHP
declare(ticks=1) {
    // 一些程式碼
}
```

## 4. 類別、屬性和方法

此處的 class 泛指所有的類別（classes）、介面（interfaces）和特徵機制（traits）。

任何結束大括號「不可」緊跟著任何註解或陳述式。

當實例化一個新類別時，即使沒有傳遞任何參數給建構子（constructor），也始終「必須」添加小括號。

```PHP
new Foo();
```

### 4.1 繼承和實作

`extends` 和 `implements` 關鍵字「必須」宣告在與類別名稱同一行。

起始大括號「必須」獨占一行，且結束大括號「必須」在常數、屬性或方法之後的下一行。

起始大括號「必須」獨占一行，且之前或之後「不可」有空白行。

結束大括號「必須」獨占一行，且之前「不可」有空白行。

```PHP
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // 常數、屬性和方法
}
```

所有 `implements` 的項目（在介面的情況下）「可以」被拆分成多行，每行都「必須」縮排一次。第一個項目「必須」在下一行，且每行「必須」只能有一個介面。

```PHP
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // 常數、屬性和方法
}
```

### 4.2 使用特徵機制

在類別的內部使用 `use` 關鍵字來實作特徵機制的時候，「必須」宣告在起始大括號之後的一行。

```PHP
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

引入到類別中的每個個別的特徵機制都「必須」獨占一行，且「必須」各自使用 `use` 關鍵字。

```PHP
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;
use Vendor\Package\SecondTrait;
use Vendor\Package\ThirdTrait;

class ClassName
{
    use FirstTrait;
    use SecondTrait;
    use ThirdTrait;
}
```

如果類別中的 `use` 引入陳述式之後沒有任何程式碼，結束大括號「必須」在 `use` 引入陳述式的下一行。

```PHP
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;
}
```

否則，在 `use` 引入陳述式之後，「必須」有一個空白行。

```PHP
<?php

namespace Vendor\Package;

use Vendor\Package\FirstTrait;

class ClassName
{
    use FirstTrait;

    private $property;
}
```

使用 `insteadof` 和 `as` 運算子時，「必須」按照以下方式使用，特別留意縮排、空格和空行：

```PHP
<?php

class Talker
{
    use A, B, C {
        B::smallTalk insteadof A;
        A::bigTalk insteadof C;
        C::mediumTalk as FooBar;
    }
}
```

### 4.3 屬性和常數

所有的屬性都「必須」宣告可視性。

如果你的專案的 PHP 版本支援宣告常數的可視性（PHP 7.1 以上版本）的話，所有的常數都「必須」宣告可視性。

「不可」使用 `var` 關鍵字宣告屬性。

每個陳述式「必須」只有一個屬性被宣告。

屬性名稱「不可」以底線（`_`）來表示受保護的（protected）或私有的（private）可視性。意即，以底線作為前綴毫無意義。

在型態宣告和屬性名稱之間「必須」有一個空格

一個屬性的宣告陳述式看起來如下：

```PHP
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

### 4.4 方法和函數

所有的方法都「必須」宣吿可視性。

方法名稱「不可」以底線（`_`）來表示受保護的（protected）或私有的（private）可視性。意即，以底線作為前綴毫無意義。

方法和函數名稱之後，「不可」有空格。起始大括號「必須」獨占一行，結束大括號「必須」在方法或函數內容之後獨占一行。起始小括號之後「不可」有空格，結束小括號之前「不可」有空格。

```PHP
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // 方法內容
    }
}
```

一個函數的宣告陳述式看起來如下，特別留意小括號、逗號和大括號的位置：

```PHP
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // 函數內容
}
```

### 4.5 方法和函數參數

在參數列表中，每個逗號之前「不可」有空格；每個逗號之後，「必須」有一個空格。

方法或函數中若參數帶有預設值，則「必須」放置在參數列表的尾部。

```PHP
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // 方法內容
    }
}
```

所有的參數「可以」被拆分成多行，每行都「必須」縮排一次。第一個參數「必須」在下一行，且每行「必須」只能有一個參數。結束小括號和起始大括號「必須」一起放在一個獨立的行上，且他們之間要有一個空格分隔。

```PHP
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // 方法內容
    }
}
```

當存在一個返回值的型別宣告時，在冒號之後「必須」有一個空格，並緊跟著一個型別宣告。冒號和宣告「必須」與參數列表的結束小括號在同一行，且結束小括號和冒號之間沒有任何空格。

```PHP
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
```

在可為空值的型別宣告中，問號和型別之間「不可」有空格。

```PHP
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

當在一個參數前面使用 `&` 運算子時，他們之間「不可」有空格。

在可變參數的三點運算子和參數名稱之間「不可」有空格。

```PHP
public function process(string $algorithm, ...$parts)
{
    // 處理
}
```

當組合了引用運算子和可變參數的三點運算子時，他們之間「不可」有空格。

```PHP
public function process(string $algorithm, &...$parts)
{
    // 處理
}
```

### 4.6 abstract、final 和 static

當使用 `abstract` 和 `final` 關鍵字時，「必須」宣告在可視性宣吿之前。

當使用 `static` 關鍵字時，「必須」宣告在可視性宣告之後。

```PHP
<?php

namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // 方法內容
    }
}
```

### 4.7 方法和函數調用

在調用一個方法或函數時，「不可」有空格在方法或函數名稱與起始小括號之間，「不可」有空格在起始小括號之後，「不可」有空格在結束小括號之前。在參數列表中，每個逗號之前「不可」有空格，每個逗號之後「必須」有一個空格。

```PHP
<?php

bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

所有的參數「可以」被拆分成多行，每行都「必須」縮排一次。第一個參數「必須」在下一行，且每行「必須」只能有一個參數。

```PHP
<?php

$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

將一個參數（可能是閉包或陣列）拆分成多行，並不算是一種參數列表的拆分。

```PHP
<?php

somefunction($foo, $bar, [
  // ...
], $baz);

$app->get('/hello/{name}', function ($name) use ($app) {
    return 'Hello ' . $app->escape($name);
});
```

## 5. 控制流程

控制流程的通用規則如下：

- 控制流程的關鍵字之後「必須」有一個空格。
- 起始小括號之後「不可」有空格。
- 結束小括號之前「不可」有空格。
- 結束小括號和起始大括號之間「必須」有一個空格。
- 結構主體「必須」縮排一次。
- 結構主體「必須」從起始大括號的下一行開始。
- 結束大括號「必須」在結構主體之後獨占一行。
- 每個結構主體「必須」使用大括號包圍。

這標準化了控制流程的外觀，並減少新增行到結構主體時出錯的可能性。

### 5.1 if、elseif 和 else

一個 `if` 結構如下所示。特別留意小括號、空格和大括號的位置，以及 `else` 和 `elseif` 與他們的前一個結束大括號放在同一行。

```PHP
<?php

if ($expr1) {
    // if 內容
} elseif ($expr2) {
    // elseif 內容
} else {
    // else 內容
}
```

「應該」使用 `elseif` 來取代 `else if`，這使得所有的控制關鍵字看起來都像單個單字。

小括號中的表達式「可以」被拆分成多行，每行都「必須」縮排一次。第一個條件「必須」在下一行。結束小括號和起始大括號「必須」在獨立的同一行上，且他們之間要有一個空格分隔。條件之間的布林運算子「必須」始終在行的開頭或結尾，而不是兩者混用。

```PHP
<?php

if (
    $expr1
    && $expr2
) {
    // if 內容
} elseif (
    $expr3
    && $expr4
) {
    // elseif 內容
}
```

### 5.2 switch 和 case

一個 `switch` 結構如下所示。特別留意小括號、空格和大括號的位置。 `case` 陳述式「必須」比 `switch` 多縮排一次，`break` 關鍵字（或其他終止關鍵字）「必須」在與 `case` 內容相同的級別上縮排。如果要故意貫穿（fall-through）在一個非空值的 `case` 內容時，「必須」在其內部結尾添加一個註解，像是 `// no break`。

```PHP
<?php

switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

小括號中的表達式「可以」被拆分成多行，每行都「必須」縮排一次。第一個條件「必須」在下一行。結束小括號和起始大括號「必須」在獨立的同一行上，且他們之間要有一個空格分隔。條件之間的布林運算子「必須」始終在行的開頭或結尾，而不是兩者混用。

```PHP
<?php

switch (
    $expr1
    && $expr2
) {
    // 結構內容
}
```

### 5.3 while 和 do while

一個 `while` 陳述式如下所示。特別留意小括號、空格和大括號的位置。

```PHP
<?php

while ($expr) {
    // 結構內容
}
```

小括號中的表達式「可以」被拆分成多行，每行都「必須」縮排一次。第一個條件「必須」在下一行。結束小括號和起始大括號「必須」在獨立的同一行上，且他們之間要有一個空格分隔。條件之間的布林運算子「必須」始終在行的開頭或結尾，而不是兩者混用。

```PHP
<?php

while (
    $expr1
    && $expr2
) {
    // 結構內容
}
```

一個 `do while` 陳述式如下所示。特別留意小括號、空格和大括號的位置。

```PHP
<?php

do {
    // 結構內容
} while ($expr);
```

小括號中的表達式「可以」被拆分成多行，每行都「必須」縮排一次。第一個條件「必須」在下一行。條件之間的布林運算子「必須」始終在行的開頭或結尾，而不是兩者混用。

```PHP
<?php

do {
    // 結構內容
} while (
    $expr1
    && $expr2
);
```

### 5.4 for

一個 `for` 陳述式如下所示。特別留意小括號、空格和大括號的位置。

```PHP
<?php

for ($i = 0; $i < 10; $i++) {
    // for 內容
}
```

小括號中的表達式「可以」被拆分成多行，每行都「必須」縮排一次。第一個表達式「必須」在下一行。結束小括號和起始大括號「必須」在獨立的同一行上，且他們之間要有一個空格分隔。

```PHP
<?php

for (
    $i = 0;
    $i < 10;
    $i++
) {
    // for 內容
}
```

### 5.5 foreach

一個 `foreach` 陳述式如下所示。特別留意小括號、空格和大括號的位置。

```PHP
<?php

foreach ($iterable as $key => $value) {
    // foreach 內容
}
```

### 5.6 try、catch 和 finally

一個 `try-catch-finally` 區塊如下所示。特別留意小括號、空格和大括號的位置。

```PHP
<?php

try {
    // try 內容
} catch (FirstThrowableType $e) {
    // catch 內容
} catch (OtherThrowableType | AnotherThrowableType $e) {
    // catch 內容
} finally {
    // finally 內容
}
```

## 6. 運算子

運算子的風格規範取決於條件式有幾個運算元（operands）。

空格「可以」被添加在運算子（operator）的前後，用來增加可閱讀性。

### 6.1 一元運算子

增值／減值運算子（increment/decrement operators）「不可」有空格在運算子和運算元的中間。

型別轉換運算子（type casting operators）「不可」有空格在小括號之間。

```PHP
$intValue = (int) $input;
```

### 6.2 二元運算子

在所有二元運算子之前和之後，「必須」至少有一個空格，包括[算術運算子](http://php.net/manual/en/language.operators.arithmetic.php)、[比較運算子](http://php.net/manual/en/language.operators.comparison.php)、[指派運算子](http://php.net/manual/en/language.operators.assignment.php)、[位元運算子](http://php.net/manual/en/language.operators.bitwise.php)、[邏輯運算子](http://php.net/manual/en/language.operators.logical.php)、[字串運算子](http://php.net/manual/en/language.operators.string.php)和[型別運算子](http://php.net/manual/en/language.operators.type.php)。

```PHP
if ($a === $b) {
    $foo = $bar ?? $a ?? $b;
} elseif ($a > $b) {
    $foo = $a + $b * $c;
}
```

### 6.3 三元運算子

在三元運算子（`?` 和 `:` 字元）之前和之後，「必須」至少有一個空格。

```PHP
$variable = $foo ? 'foo' : 'bar';
```

當中間的運算元被省略時，「必須」遵循和二元運算子相同的風格。

```PHP
$variable = $foo ?: 'bar';
```

## 7. 閉包

閉包宣告「必須」在 `function` 關鍵字之後添加一個空格，並且在 `use` 關鍵字之前和之後添加一個空格。

起始大括號「必須」在同一行上，並且結束大括號「必須」在緊跟著主體的下一行上。

參數列表或變數列表的起始小括號之後「不可」有空格，結束小括號之前「不可」有空格。

在參數列表或變數列表中，每個逗號前面「不可」有空格，每個逗號之後「必須」有一個空格。

閉包中帶有預設值的參數，「必須」放置在參數列表的尾部。

若已宣告回傳型態，則「必須」遵循一般方法和函數的規則；若是 `use` 關鍵字被宣告，冒號「必須」在 `use` 列表的結束小括號之後，且兩字元之間無空格

一個閉包宣告如下所示，特別留意小括號、逗號、空格和大括號的位置：

```PHP
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // 內容
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // 內容
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // 內容
};
```

參數列表和變數列表「可以」拆分成多行，每行都「必須」縮排一次。列表中的第一個項目「必須」在下一行，並且每行「必須」只能有一個參數或變數。

當列表被拆分成多行時，結束小括號和起始大括號「必須」在同一行上，並且使用一個空格分隔。

以下是閉包中參數列表和變數列表拆分成多行的範例：

```PHP
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // 內容
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // 內容
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // 內容
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // 內容
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // 內容
};
```

特別注意，這個格式規範也適用於直接在函數或方法調用中使用閉包作為參數的情況。

```PHP
<?php

$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // 內容
    },
    $arg3
);
```

## 8. 匿名類別

匿名類別（anonymous classes）「必須」遵循與上一節的閉包相同的準則和原則。

```PHP
<?php

$instance = new class {};
```

只要 `implements` 的介面列表不拆分成多行，起始大括號可以和 `class` 關鍵字放在同一行上。

假如介面列表拆分成多行時，起始大括號「必須」放在最後一個介面的下一行上。

```PHP
<?php

// Brace on the same line
$instance = new class extends \Foo implements \HandleableInterface {
    // Class content
};

// Brace on the next line
$instance = new class extends \Foo implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // Class content
};
```

---

原文：https://www.php-fig.org/psr/psr-12/
