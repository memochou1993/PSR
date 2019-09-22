PSR-1：基本程式寫作標準
===

此標準制定了程式寫作基本元素的相關標準，用以確保共用的 PHP 程式碼之間有高度的技術互用性（technical interoperability）。

本文件所使用之「必須」、「不可」、「需要」、「應」、「不應」、「應該」、「不應該」、「可以」和「可選的」等描述性詞彙，在 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 有詳細的解釋。

## 1. 概述

- 所有的 PHP 檔案「必須」只使用 `<?php` 和 `<?=` 標簽。
- 所有的 PHP 檔案「必須」以沒有位元組順序記號（BOM）的 UTF-8 字元編碼。
- 所有的 PHP 檔案「應該」只能宣告 symbols（類別、函數、常數等），或是產生 side effects（例如：產生輸出、變更 .ini 設定等）， 但是「不應該」兩個都做。
- 命名空間和類別「必須」遵守 autoloading PSR。
- 類別名稱「必須」以大駝峰式命名法（StudlyCaps）命名。
- 類別常數「必須」以大寫和底線命名。
- 方法名稱「必須」以小駝峰式命名法（camelCase）命名。

## 2. 檔案

### 2.1 PHP 標籤

PHP 程式碼「必須」使用長標籤 `<?php ?>` 或短標籤（short-echo）`<?= ?>`；「不可」使用其他標籤。

### 2.2 字元編碼

PHP 程式碼「必須」只使用沒有位元組順序記號（BOM）的 UTF-8 字元編碼。

### 2.3 Side Effects

一個檔案裡「應該」宣告新的 symbols（類別、函數、常數等）而不導致 side effects，或是「應該」執行帶有 side effects 的邏輯，但是「不應該」兩個都做。

Side effects 指的是，執行的邏輯不直接相關於宣告類別、函數、常數等，只與引入檔案有關。

Side effects 包括但不限於產生輸出、明確地使用 `require` 或 `include` 關鍵字、連結外部服務、變更 .ini 設定、發送錯誤或例外、修改全域或靜態變數，以及讀取或寫入檔案等。

以下是同時包含了宣告和 side effects 的範例；意即以下的範例應該避免：

```PHP
<?php
// side effect: 變更 .ini 設定
ini_set('error_reporting', E_ALL);

// side effect: 引入檔案
include "file.php";

// side effect: 產生輸出
echo "<html>\n";

// 宣告
function foo()
{
    // 函數內容
}
```

以下範例是沒有 side effects 的宣告；是可以仿效的範例：

```PHP
<?php
// 宣告
function foo()
{
    // 函數內容
}

// 條件陳述式不算是 side effect
if (! function_exists('bar')) {
    function bar()
    {
        // 函數內容
    }
}
```

## 3. 命名空間和類別名稱

命名空間和類別「必須」遵守 autoloading PSR。

意即一個檔案只會有一個類別，並且至少有一層命名空間──最上層的 vendor 名稱。

類別名稱「必須」以大駝峰式命名法命名。

PHP 5.3 以上的程式碼「必須」使用正式的命名空間，例如：

```PHP
<?php
// PHP 5.3 以上版本：
namespace Vendor\Model;

class Foo
{
}
```

PHP 5.2.x 以下的程式碼「應該」遵守偽命名空間（pseudo-namespacing）慣例，類別名稱使用 `Vendor_` 前綴，例如：

```PHP
<?php
// PHP 5.2.x 以下版本：
class Vendor_Model_Foo
{
}
```

## 4. Class 常數、屬性和方法

此處的 class 泛指所有的類別（classes）、介面（interfaces）和特徵機制（traits）。

### 4.1 常數

常數名稱「必須」以大寫和底線命名。

```PHP
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2 屬性

屬性名稱可以使用大駝峰式命名法（`$StudlyCaps`）、小駝峰式命名法（`$camelCase`）或底線式命名法（`$under_score`）命名，本規範不強制要求。

無論使用何種命名準則，在合理範圍內「應該」要保持一致性。這個範圍可以是團隊級別（vendor-level）、套件級別（package-level）、類別級別（class-level）或方法級別（method-level）。

### 4.3 方法

方法名稱「必須」以小駝峰式命名法命名，像是 `camelCase()`。

---

原文：https://www.php-fig.org/psr/psr-1/
