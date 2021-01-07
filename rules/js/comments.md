# 程式註解規範

> 註解，給以後需要理解你的程式的人(或許就是你自己)留下信息是非常有用的。註解應該和它們所註解的代
> 碼一樣是書寫良好且清晰明了。 避免冗長或者情緒化的註解。

## 文件頭部註解

1. 所有 js，css 文件頭部，必須有文件註解，用於簡要說明:
   文件的主要功能(含模組信息)、作者(含作者郵箱)、版權等信息。 文件頭註解格式如下:

   ```javascript
   /**
    * Basic lang utilities functions ...
    *
    * @author Allex Wang
    * @module clib/lang
    */
   define('lang', function(require, exports, module) {
     ...
   });
   ```

2. 註解需要簡潔明了，從已解決的方案到未開發的功能，註解必須與程式相關。

3. **及時地更新註解，錯誤的註解會讓程序更加難以閱讀和理解。**

4. (建議) 公用模組文件，請添加範例程式。

5. (建議) 所有的註解請盡量使用英文(跨平台編輯)。

6. (建議) // 用作程式行註解，/_..._/ 形式用作對整個程式段的註解，較正式的宣告中， 如函數參數、功能、文件功能等的描述中。

7. (建議) 如果可能，文件頭部的註解，還要包含文件依賴關系、版本號、第三方程式來源 url 信息等。

---

## 程式內部註解

1. 大量的變數宣告後面須添加註解，說明變數用途。

2. 每個對外暴露的 API 方法，需要加註解說明其用途。註解需要包括: 函數的用途、參數、返回值等，此三項為強制要求。

3. 生澀的程式就沒有必要添加註解了，首先您需要重寫它們。

4. 註解沒有必要每行都添加，只在重要的邏輯、或者較復雜的邏輯處，增加必要的註解。

5. 通俗易懂的語句壓根兒不需要添加註解，合理的變數命名其實是最直接的註解。

6. 刪除註解掉的程式塊，只要提交了 git，程式可以隨時找回，無需保留被註解的廢棄程式。

---

## 模組註解規範

1. 類註解

   每個類的定義都要附帶一份註解，描述類的功能和用法. 也需要說明構造器參數. 如果該類繼承自其它類， 應該使用 @extends 標記. 如果該類是對接口的實現，應該使用 @implements 標記.

   ```javascript
   /**
    * Class making something fun and easy.
    * @param {String} arg1 An argument that makes this more interesting.
    * @param {Array} arg2 List of numbers to be processed.
    * @constructor
    * @extends {goog.Disposable}
    */
   project.MyClass = function (arg1, arg2) {
     // ...
   };
   goog.inherits(project.MyClass, goog.Disposable);
   ```

2. 方法與函數的註解

   提供參數的說明. 使用完整的句子，並用第三人稱來書寫方法說明.

   ```javascript
   /**
    * Converts text to some completely different text.
    * @param {String} arg1 An argument that makes this more interesting.
    * @return {String} Some return value.
    */
   MyClass.prototype.someMethod = function (arg1) {
     // ...
   };

   /**
    * Operates on an instance of MyClass and returns something.
    * @param {project.MyClass} obj Instance of MyClass which leads to a long
    *     comment that needs to be wrapped to two lines.
    * @return {boolean} Whether something occured.
    */
   function PR_someMethod(obj) {
     // ...
   }
   ```

   對於一些簡單的，不帶參數的 getters，說明可以忽略.

   ```javascript
   /**
    * @return {Element} The element for the component.
    */
   Component.prototype.getElement = function () {
     return this._element;
   };
   ```

3. 屬性註解

   ```javascript
   /**
    * Maximum number of things per pane.
    * @type {Number}
    */
   project.MyClass.prototype.someProperty = 4;
   ```

4. 類型轉換的註解

   有時，類型檢查不能很准確地推斷出表達式的類型， 所以應該給它添加類型標記註解來明確之，並且必須在表達式和類型標簽外面包裹括號.

   ```javascript
   function setFoo(x) (/* @type {Number} */ x) { ... }
   ```

5. 枚舉

   ```javascript
   /**
    * Enum for tri-state values.
    * @enum {Number}
    */
   project.TriState = {
     TRUE: 1,
     FALSE: -1,
     MAYBE: 0,
   };
   ```

   注意一下，枚舉也具有有效類型，所以可以當成參數類型來用.

   ```javascript
   /**
    * Sets project state.
    * @param {project.TriState} state New project state.
    */
   project.setState = function (state) {
     // ...
   };
   ```

6. 模組使用範例註解:

   ```javascript
   /**
    * @example
    *  var bleeper = makeBleep(3);
    *  bleeper.flop();
    */
   ```

7. Typedefs:

   有時類型會很復雜. 比如下面的函數，接收 Element 參數

   ```javascript
   /**
    * @param {String} tagName
    * @param {String|Element|Text|Array} contents
    * @return {Element}
    */
   goog.createElement = function(tagName, contents) {
       ...
   };
   ```

   你可以使用 @typedef 標記來定義個常用的類型表達式

   ```javascript
   /** @typedef {String|Element|Text|Array} */
   goog.ElementContent;

   /**
    * @param {String} tagName
    * @param {goog.ElementContent} contents
    * @return {Element}
    */
   goog.createElement = function(tagName, contents) {
       ...
   };
   ```

## 參考

1. [JSDoc](https://jsdoc.app/)
2. [JSDoc 中文版](https://www.css88.com/doc/jsdoc/index.html)
