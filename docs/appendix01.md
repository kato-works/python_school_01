## SyntaxError 練習問題

1. **問題:**
   
   ```python
   print("Hello"
   ```
   
   ```python
     print("Hello"
                 ^
   SyntaxError: incomplete input
   ```

   **解説:** `print` 関数の呼び出しで閉じ括弧が不足しているため、式が最後まで完結していません。Python は行末まで読んでも構文が成立しないと判断し、このエラーを出します。
   **ヒント:** 括弧や引用符が正しく閉じられているか確認し、必要な閉じ括弧を追加しましょう。


2. **問題:**

   ```python
   if x == 10 print(x)
   ```

   ```python
       if x == 10 print(x)
                  ^
   SyntaxError: invalid syntax
   ```

   **解説:** `if` 文で条件のあとにコロン `:` が必要ですが、それが欠けているため文全体が不正な構文になります。
   **ヒント:** 条件のあとにコロンを入れ、条件が真のときに実行する処理を次の行でインデントして書きましょう。

3. **問題:**

   ```python
   if True:
   print("OK")
   ```

   ```python
       print("OK")
       ^
   IndentationError: expected an indented block after 'if' statement on line 1
   ```

   **解説:** `if True:` の後にはインデントされたブロックが必要ですが、次の行がインデントされていないためエラーになっています。
   **ヒント:** `if` 文の内部で実行したい行はスペースまたはタブでインデントしてください。

4. **問題:** 

   ```
   message = "Hello
   ```
   
   ```python
       message = "Hello
                 ^
   SyntaxError: unterminated string literal (detected at line 1)
   ```

   **解説:** 文字列を開始したものの、終わりの引用符がないため文字列が閉じられていません。
   **ヒント:** 開始と終了の引用符が対になっているかを確認し、抜けている側を補いましょう。


5. **問題:**

   ```python
   class = "Math"
   ```

   ```python
       class = "Math"
             ^
   SyntaxError: invalid syntax
   ```

   **解説:** `class` は Python の予約語であり、変数名として使用できません。そのため構文エラーが発生しています。
   **ヒント:** 予約語ではない別の名前を変数として使用しましょう。

6. **問題:**

   ```python
   def greet:
       print("Hi")
   ```

   ```python
    def greet:
             ^
   SyntaxError: expected '('
   ```

   **解説:** 関数定義では関数名のあとに丸括弧が必要ですが、それが省略されているため構文エラーになります。
   **ヒント:** 関数名の後ろに `()` を追加し、引数を定義しましょう。

7. **問題:** 
   
   ```python
   print('Alice's cat')
   ```
  
   ```python
       print('Alice's cat')
                         ^
   SyntaxError: unterminated string literal (detected at line 1)
   ```

   **解説:** 文字列をシングルクォートで囲む途中に同じクォートが現れ、文字列が意図せず途切れています。
   **ヒント:** 文字列内のクォートをエスケープするか、別の種類の引用符で文字列を囲みましょう。

8. **問題:** 
   
   ```python
   x　= 1
   ```

   ```python
       x　= 1
        ^
   SyntaxError: invalid non-printable character U+3000
   ```

   **解説:** 代入文の `=` の前に全角スペースが含まれており、Python が無効な文字として認識しています。
   **ヒント:** 全角スペースを半角スペースに置き換えてください。

9. **問題:** 
   
   ```python
   x = 1
   print(f'x = { X }')
   ```

   ```python
         1 x = 1
   ----> 2 print(f'x = { X }')

   NameError: name 'X' is not defined
   ```

   **解説:** F 文字列内で `X` という変数を参照していますが、その名前の変数が定義されていないため NameError が発生しています。
   **ヒント:** 参照したい変数名が正しいか確認し、定義済みの名前を用いるか必要なら変数を定義してください。

10. **問題:**
    
    ```python
    if x = 1:
        pass
    ```
    
    ```python
    if x = 1:
         ^
    SyntaxError: invalid syntax. Maybe you meant '==' or ':=' instead of '='?
    ```

    **解説:** `if` 文の条件式で代入演算子 `=` を使用しているため、比較式として解釈できず構文エラーになります。
    **ヒント:** 値の比較を行いたい場合は等価演算子 `==` を用いましょう。
