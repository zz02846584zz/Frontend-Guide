# 命名規範

## 變數命名

1. 宣告變數必須加上關鍵字 `let` 或 `const`，避免使用未宣告的變數。

   除非必要，不要使用 var 宣告變數，避免因作用域產生的問題及全域污染。 (特殊情況需要經專案負責人批准)

2. 變數的命名，不得使用 js 保留字。 js 保留字列表:

   ```javascript
   abstract boolean break byte case catch char class const continue default do
   double else extends false final finally float for function goto if implements
   import in instanceof int interface long native new null package private
   protected public return short static super switch synchronized this throw throws
   transient true try var void while with
   ```

3. 精簡短小，見名知意。變數名使用英文大小寫和數字命名，使用**駝峰命名**規則，例如: getStyle、addEvent。

4. 不能使用沒有任何意義的變數名 (迴圈的指針變數除外，見下文 15)

   例如: var a = 1; var xx = true; 避免無意義的簡寫，例如: MouseEventHandler 寫作 MseEvtHdlr。

5. `常數使用全大寫`作為變數名，多個單詞之間用下劃線(\_)分隔。例如: NAME_LIKE_THIS。

6. `函數內保存 DOM 引用和定時器的變數，使用完後必須顯式銷毀`， 從而可以及時的執行內存回收。例如設置該變數為 null; 定時器變數銷毀，請執行 clearInterval 或者 clearTimeout。

7. 私有化變數和方法名應該以下劃線 `_` 開頭 (僅限有跨作用域的變數或方法等).

8. (建議) 布林變數、返回值為 boolean 的函數/方法前可以添加前綴 is/has/can/should。

9. (建議) 避免產生歧義的命名，例如: isNotError，isNotFound。

10. (建議) for 迴圈中的臨時重復變數建議以 i，j，k，m，n ... 命名。

11. (建議) 多個變數宣告時，適當換行表示，參照 var 關鍵字位置保持縮進。

---

## 自定義物件(類別)命名

1. 自定義物件(類別)

   命名，每個單詞首字母均需要大寫，例如: ModuleDialog。
   內部物件 (不會導出的構造器或靜態物件)，使用 \_ 開頭來定義，例如: \_BaseTab;

2. 物件的方法

   駝峰命名方式，必須是動詞或者動詞短語，例如: obj.getSomeValue()。
   函數的參數個數不固定時，應該添加最後一個取名為 `args` 的參數.
   可選和可變參數應該在 @param (Optional) 標記中說明清楚.

### 變數賦值及定義

1. 下面類型的物件不建議用 new 構造，是使用直接量賦值:
   new Number，new String，new Boolean，new Object (用{}代替)，new Array(用[]代替)。

2. 禁止陣列或者 JSON 中出現冗余的逗號，IE 下會拋出語法錯誤。
   例如: var testArray = [1，，，; 或者 var jsonExample = { 'key1': value1，'key2': value2，;

3. 禁止污染內置物件的原型，例如 Object.prototye、Array.prototype、Function.prototype。

4. 不要使用連等進行賦值。例如:

   ```javascript
   (function () {
     var numberA = (numberB = 3); // 這裡產生的 numberB 是全域變數
   })();
   alert(numberB); // return 3
   ```

5. 如果一個賦值語句是用函數和物件來賦值，可能需要跨多行，一定切記要在賦值語句末加上分號。

6. (建議) 陣列和物件初始化時，如果初始值不是很長，盡量保持寫在單行上; JSON 物件中，比較長的 key/value，不必為了美觀以冒號對齊。

7. (建議) 沒必要在每次宣告變數時就將其初始化，但使用變數之前一定要確保變數已經初始化。
