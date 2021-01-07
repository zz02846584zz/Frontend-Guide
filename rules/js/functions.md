# 函數/閉包

## 函數

1. 一個函數的內容不宜太長，較復雜的邏輯，需拆分成多個函數來實現，使程式邏輯清晰。

2. 對外暴露的 API 型函數，盡量保持輸入輸出的穩定，減小調用者修改程式的成本和風險。

3. 可以嵌套函數，用於減少重復程式，隱藏一些局部函數等，但不要在塊內宣告一個函數。因為 JS
   並不支持塊級作用域，雖然很多 js 引擎都支持塊內宣告函數，但它不屬於 ECMAScript 規範 (見 ECMA-262，第
   13 和 14 條)。各個瀏覽器糟糕的實現相互不兼容，有些也與未來 ECMAScript 草案相違背。ECMAScript 只允
   許在腳本的根語句或函數中宣告函數. 如果確實需要在塊中定義函數，建議使用函數表達式來初始化變數。例如:

   ```javascript
   // (錯誤)
   if (x) {
     function foo() {}
   }
   // 應該寫作: (正確)
   if (x) {
     var foo = function () {};
   }
   ```

4. 有很多方法可以給構造器添加方法或成員，我們更傾向於使用如下的形式:

   ```javascript
   Foo.prototype.bar = function () {
     /* ... */
   };
   ```

5. 僅在物件構造器、方法、閉包中使用 `this` 物件，避免 this 亂用出現的指代不明。 `this`
   的語義很特別。有時它引用一個全局物件(大多數情況下)，調用者的作用域(使用 eval 時)，DOM
   樹中的節點(添加事件處理函數時)，新創建的物件(使用一個構造器)，或者其他物件(如果函數被 call() 或
   apply())。

6. 引用物件成員用 obj.propName 代替 obj['propName']，除非屬性名是變數或是接口數據的引用。

## 函數參數

1. 函數的必選參數，必須檢查是否傳遞了合法的參數，避免參數類型不對帶來的異常。

2. 函數參數寫在同一行上。如果一行超過 80 字符，請按照縮進原則進行換行，並保持適當縮進。

## 閉包

1. 由於閉包保留了一個指向它封閉作用於的指針，所以在給 DOM 元素附加閉包時候，要避免產生循環引用，從而導致內存洩露。例如:

   ```javascript
   // (錯誤)
   function foo(element, a, b) {
     element.onclick = function () {
       /* 使用變數 a 和 b */
     };
   }
   ```

   這裡，即使沒有使用 element，閉包也保留了 element，a 和 b 的引用，由於 element
   也保留了對閉包的引用，這就產生了循環引用，這就不能被 GC 回收. 這種情況下，可將程式重構為:

   ```javascript
   function foo(element, a, b) {
     element.onclick = handle(a, b);
   }
   function handle(a, b) {
     return function () {
       /* 使用變數 a 和 b */
     };
   }
   ```

2. 通常我們需要給模組提供 destroy 接口方法，在這個方法做好模組的善後工作，防止內存開銷過大，如。

   ```javascript
   /**
    * var loader = ImageLoader(...);
    * loader.load();
    * loader.destroy();
    */
   var ImageLoader = functiono(images) {
     // binding onload event etc
     ...

     return {
       load: function() {
         ...
       },
       destory: function() {
         images.forEach(functiono() {
           img.onload = null;
           img = null;
         });
         images = null;
       }
     };
   };
   ```
