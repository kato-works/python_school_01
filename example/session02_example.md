# 第2回：条件分岐とループ処理

以下は、回答編です。

## 演習課題 1
変数 score の値に応じて「合格」または「不合格」を表示する `if` 文を書く。
```python
score = 75
if score >= 60:
    print("合格")
else:
    print("不合格")
```

## 演習課題 2

1 から 5 までの整数を `for` で出力する。

```python
for n in range(1, 6):
    print(n)
```

## 演習課題 3

リスト animals を `for` で回して要素を表示する。

```python
animals = ["cat", "dog", "bird"]
for animal in animals:
    print(animal)
```

## 演習課題 4

0 から 3 まで数える `while` ループを作成する。

```python
count = 0
while count <= 3:
    print(count)
    count += 1
```

## 演習課題 5

`range` を使い、1 から 10 までの合計を求める。

```python
total = sum(range(1, 11))
print(total)
```

## 演習課題 6

好きな数を当てる簡単なゲームを作ってみる。

```python
import random
answer = random.randint(1, 10)
while True:
    guess = int(input("1~10の数を当ててください: "))
    if guess == answer:
        print("正解!")
        break
    elif guess < answer:
        print("もっと大きいです")
    else:
        print("もっと小さいです")
```
