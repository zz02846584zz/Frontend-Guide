# 條件語句/迴圈規範

## 條件語句/迴圈

### 條件語句

1. if 語句，即使只有單行，也要用花括號括起來，例如:

   ```javascript
   // (錯誤)
   if (condition) statement;

   // (正確)
   if (condition) {
     statement;
   }
   ```

2. 使用三元運算子，替代單一的 if else 語句。例如:

   ```javascript
   if (val != 0) {
     return foo();
   } else {
     return bar();
   }

   // 可以寫作:
   return val ? foo() : bar();
   ```

3. if/else/while/for 條件表達式必須有小括號，且自佔一行。

4. (建議) 利用 && 和 || 短路來簡化程式:

   ```javascript
   function foo(opt_win) {
     var win;
     if (opt_win) {
       win = opt_win;
     } else {
       win = window;
     }
     // ...
   }

   // 可以寫作:
   function foo(opt_win) {
     var win = opt_win || window;
     // ...
   }
   ```

   && 短路:

   ```javascript
   if (node) {
     if (node.kids) {
       if (node.kids[index]) {
         foo(node.kids[index]);
       }
     }
   }

   // 可以寫作:
   if (node && node.kids && node.kids[index]) {
     foo(node.kids[index]);
   }

   // 或者
   var kid = node && node.kids && node.kids[index];
   if (kid) {
     foo(kid);
   }
   ```

5. (建議) 使用嚴格的條件判斷符。用 === 代替 ==，用!== 代替 !=。

### 迴圈

1. 盡量避免 for-in 迴圈，只用於 object/hash 的遍歷，陣列的遍歷使用 for 迴圈。

2. for-in 迴圈體中必須用 hasOwnProperty 方法檢查成員是否為自身成員，避免來自原型鏈上的污染。

3. 避免在 if 和 while 語句的條件部分進行賦值。例如:

   ```javascript
   // (錯誤)
   var i = 10;
   while ((i = i - 2)) {
     statement;
   }
   // 應該寫作: (正確)
   var i = 10;
   while (i > 0) {
     statement;
     i = i - 2;
   }
   ```
