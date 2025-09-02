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


2. **問題:**

   ```python
   if x == 10 print(x)
   ```

   ```python
       if x == 10 print(x)
                  ^
   SyntaxError: invalid syntax
   ```

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

4. **問題:** 

   ```
   message = "Hello
   ```
   
   ```python
       message = "Hello
                 ^
   SyntaxError: unterminated string literal (detected at line 1)
   ```


5. **問題:**

   ```python
   class = "Math"
   ```

   ```python
       class = "Math"
             ^
   SyntaxError: invalid syntax
   ```

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

7. **問題:** 
   
   ```python
   print('Alice's cat')
   ```
  
   ```python
       print('Alice's cat')
                         ^
   SyntaxError: unterminated string literal (detected at line 1)
   ```

8. **問題:** 
   
   ```python
   x　= 1
   ```

   ```python
       x　= 1
        ^
   SyntaxError: invalid non-printable character U+3000
   ```

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
