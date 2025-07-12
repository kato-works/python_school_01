# 第2回：条件分岐とループ処理

条件に応じて処理を変える `if` 文や、繰り返し処理を行う `for`／`while` 文の使い方を学びます。リストと組み合わせて利用することで、効率的なコードを書けるようになります。

## 学習内容

- `if`, `elif`, `else`
- `for` / `while`
- `range` やリストの扱い方

演習では、簡単な数当てゲームやリストの操作を通じて、条件分岐とループ処理を体験します。

---

## 1. 条件分岐の基本

- `if` 文は条件を満たすときだけ処理を実行します。
- `elif` や `else` を使うことで複数の分岐を表現できます。
- インデントをそろえて読みやすいコードを書くことが重要です。

```python
score = 70
if score > 80:
    print("Excellent")
elif score >= 60:
    print("Good")
else:
    print("Keep trying")
```

## 2. ループ処理 (`for`, `while`)

- `for` 文はリストや `range` から値を順番に取り出して処理します。
- `while` 文は条件が `True` の間、繰り返し続けます。無限ループを避けるため、条件の更新を忘れないようにします。
- 例として、数当てゲームやカウンタを用いた繰り返しを実装してみましょう。

```python
for n in range(3):
    print("for loop", n)

count = 0
while count < 3:
    print("while loop", count)
    count += 1
```

## 3. `range` とリストの活用

- `range(n)` で 0 から `n-1` までの整数列を生成できます。
- ループと組み合わせると、決められた回数だけ処理を繰り返すときに便利です。
- リストの `append` や `len` など基本的なメソッドと併用する方法を紹介します。

```python
# 1 から 5 までの平方数を求める
squares = []
for i in range(1, 6):
    squares.append(i ** 2)
print(squares)
```
