---
title: Asynchronous JavaScript and XML
date: 2025-01-21
tags: AJAX
---

# jQuery AJAX 常用參數說明

<style>
    .innerMargin details {
        margin:3px 0px
    }
</style>
<div class="innerMargin" style="font-size:1.2rem;text-align: justify;" >
<details>
  <summary>
  url 要請求的 URL。
  </summary>
  
``` JavaScript
  url: "https://www.thef2e.com/api/tagList",
```
</details>

<details>
  <summary>
    type HTTP 方法，常見的有 GET、POST 等，默認為 GET。
  </summary>

```JavaScript
  type:"GET",
```

</details>
<details>
  <summary>
    method 與 type 等價，建議使用 method（因為與標準的 'fetch' 方法一致）。
  </summary>

```JavaScript
  method : "POST"
```

</details>

<details>
  <summary>data 傳遞到伺服器的資料，可以是物件或字串。 </summary>

```JavaScript
1. data: { name: 'John Doe', age: 30 }, //PSOT
2. data: 'name=John Doe&age=30',  //GET
3. var formData = new FormData();
   formData.append("name", "John Doe");

   data: formData,
```

</details>

<details>
  <summary>dataType 預期的返回數據類型，例如 'json'、'xml'、'html' 或 'text'。</summary>

```JavaScript
dataType: 'json'
```

</details>

<details>
  <summary>contentType 請求的內容類型（默認為 'application/x-www-form-urlencoded; charset=UTF-8'）。</summary>

```JavaScript
1. contentType : 'application/x-www-form-urlencoded; charset=UTF-8',
2. contentType : 'application/json', // 請求的主體（data）包含的是 JSON 格式的數據
3. contentType: false, // 禁用內容類型，通常與文件上傳一起使用
```

</details>

<details>
  <summary>async 是否以非同步方式發送請求（默認為 'true'）。</summary>

```
  async:true; //開啟非同步
```

</details>
<details>
  <summary>
    cache 是否對請求的結果進行快取（默認為 true）。
  </summary>

```JavaScript
cache : true,
```

</details>
                                
<details>
  <summary>headers 自訂 HTTP 標頭，例如：'{ 'Authorization': 'Bearer token' }'。</summary>
  
  ``` JavaScript
    //適合標頭的設置是固定的，無需根據請求過程中的動態條件進行調整
    headers: {
        'Authorization': 'Bearer YOUR_TOKEN_HERE',  // 自訂 Authorization 標頭
    },
    ```

</details>
<details>
  <summary>timeout 設定請求的超時時間（以毫秒為單位）。</summary>

```JavaScript
timeout: 5000,  // 設定超時為 5000 毫秒（即 5 秒）
```

</details>
<details>
  <summary>beforeSend  發送請求之前執行的回調函數（function），接受一個 'jqXHR'(XML HttpRequest) 對象作為參數。</summary>
  
``` JavaScript
  /*
    1. 比直接在header寫的好處：可以根據條件動態地設置 Authorization 標頭，這對於需要根據不同情況設置標頭
    2. 可以將請求的設置邏輯抽象出來，保持代碼的靈活性。
  
   */
 beforeSend: function(xhr) {
        // 在請求發送前，設置自訂標頭
        xhr.setRequestHeader('Authorization', 'Bearer YOUR_TOKEN');
        console.log('請求發送前進行設置');
    },
```

</details>
<details>
  <summary>complete 無論成功或失敗，都會執行的回調函數（function）。</summary>

```JavaScript
//無論成功或者失敗都會執行到此程式
complete: function(xhr, status) {
      // 顯示請求結束的訊息
      console.log('請求已完成，狀態:', status);
  }

```

</details>
<details>
<summary>success 請求成功時執行的回調函數（function），接收回應的數據、文字狀態以及 `jqXHR` 對象作為參數。</summary>

```JavaScript
  success: function(response) {
        console.log('請求成功:', response);
    },
```

</details>

<details>
<summary>error 請求失敗時執行的回調函數（function），接收 `jqXHR` 對象、文字狀態和錯誤訊息作為參數。</summary>

```JavaScript
 error: function(xhr, status, error) {
        console.log('請求失敗:', error);
    },
```

</details>
<details>
<summary>processData 是否將數據轉換為查詢字串（對於 'GET' 和 'POST' 默認為 'true'）。</summary>

```JavaScript
 data: { name: 'Alice', age: 25 },
 processData: true, // data 物件 ({ name: 'Alice', age: 25 }) 會被轉換為查詢字串：?name=Alice&age=25，並附加到 URL。
```

</details>
<details>
<summary>crossDomain(Cross-Origin Requests) 是否允許跨域請求（通常自動判斷）。</summary>

```JavaScript
//當 crossDomain 設置為 true 時，jQuery 會顯式告訴瀏覽器這是一個跨域請求。
//當 crossDomain 設置為 false（默認值）時，jQuery 會自動根據 URL 判斷是否為跨域請求。

    crossDomain: true,// 顯式設置為 true，表明這是一個跨域請求

```

</details>

<details>
<summary>xhrFields 用於設定 XMLHttpRequest 對象的屬性，例如'{ withCredentials: true }'。</summary>

```JavaScript
xhrFields: {
        withCredentials: true  // 設置為 true，表示攜帶憑證（如cookies）
    },

xhrFields: {
    responseType: 'json'
     } //覽器會自動解析返回的 JSON 數據，並將其轉換為 JavaScript 物件。這樣你就不需要手動解析 JSON.parse()，而是直接獲得一個物件


xhrFields: { responseType: 'json' } 是瀏覽器層級的設置，告訴瀏覽器如何處理數據。
dataType: 'json' 是 jQuery 層級的設置，告訴 jQuery 如何處理伺服器返回的數據。
```

</details>

# 使用 AJAX 範例

### **1.引入 Jquery**

```JavaScript
<head>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
```

</div>

### 簡單版本

```JavaScript
<script>

$.ajax({
  url: "", //呼叫的URL
  method: "", //HTTP method
  success: function (response) {
  },
  error: function (xhr, status, error) {
  },
});
</script>

```

### beforeSend/complete 隱藏/顯示

```JavaScript
<script>

$.ajax({
  url: 'api/test/fetchData',
  method: 'GET',
  beforeSend: function() {
    // 請求發送之前的處理，通常是顯示加載動畫
    $('#loading').show(); // 顯示加載動畫
  },
  success: function(response) {
    console.log('成功響應:', response);
  },
  error: function(xhr, status, error) {
    console.log('錯誤:', error);
  },
  complete: function() {
    // 請求完成後的處理，無論成功或失敗都會觸發
    $('#loading').hide(); // 隱藏加載動畫
  }
});

</script>

```

### 回傳後修改資料

```JavaScript

<button type="button" onclck="fetchData()" >Click Me </button>

<label id="testlable">123</label>

<input type="text" id="testinput" />

<select id="testlable">
<option value='0'>第0個</option>
<option select value='1'>第1個</option>
</select>

<script>
    function fetchData(){
        $.ajax({
        url: 'api/test/fetchData',
        method: 'POST',
        success: function(response) {
            //$('#testlable').text("新的內容");
            //$('#testinput').val("新的內容");
            //$("#testlable").val("1"); 修改為1
        },
        error: function(xhr, status, error) {
        }});
    }

</script>

```
