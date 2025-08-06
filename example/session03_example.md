# 第3回：関数とモジュール

以下は、回答編です。

## 演習課題 1
2 つの数値を受け取り足し算して返す関数 `add` を定義し、呼び出す。
```python
def add(a, b):
    return a + b
print(add(2, 3))
```

## 演習課題 2

名前を受け取ってあいさつを返す関数 `greet` を作成する。

```python
def greet(name):
    return f"Hello, {name}"
print(greet("Taro"))
```

## 演習課題 3

`math` モジュールを読み込み、円の面積を計算する。

```python
import math
r = 3
area = math.pi * r ** 2
print(area)
```

## 演習課題 4

`datetime` モジュールで今日の日付を表示する。

```python
from datetime import date
print(date.today())
```

## 演習課題 5

自作関数を別ファイルに保存し、モジュールとしてインポートする。\
`utils.py`:

```python
def double(x):
    return x * 2
```

メインコード:

```python
import utils
print(utils.double(5))
```

