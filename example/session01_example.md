# 第1回：導入とPythonの基本構文

以下は、回答編です。

## 演習課題 １

変数 x に 10、y に 3 を代入し、合計を表示する。

```python
# 変数 x に 10、y に 3 を代入
x = 10
y = 3

# 合計を計算
result = x + y

# 結果を表示
print(f'x + y = { result }')
```

## 演習課題 2

自分の名前を変数 name に入れ、`print` で「Hello, name」の形で表示する。

```python
# 自分の名前を変数 name に入れ
name = '加藤製作所'

# 「Hello, name」の形で表示する
print(f'Hello, { name }')
```

## 演習問題 3

5 と 2 の割り算結果を変数 result に保存して表示する。

```python
# 計算対象を、変数に代入する
x = 5
y = 2

# 割り算結果を変数 result に保存
result = x / y

# 表示する
print(f'x / y = { result }')
```

## 演習問題 4

2 つの数値をかけ算し、行末にコメントで式の内容を説明する。

```python
# 計算対象を、変数に代入する
x = 5
y = 2

# xとyを掛け合わせて、resultに代入する
result = x * y

# 表示する
print(f'x * y = { result }')
```

## 演習問題 5

文字列と数値を組み合わせたメッセージを出力する。

```python
# 文字列
name = 'KATO'
# 数字
x = 1895

# 組み合わせて表示
print(f'{name}, {x}')

# こう書くとどうなるでしょう
print(name * x)
```
