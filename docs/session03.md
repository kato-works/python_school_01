# 第3回：関数とモジュール

処理をまとめて再利用するための「関数」や、便利な機能がまとまった「モジュール」の使い方を学習します。自分で作った関数を呼び出して、より読みやすいコードを目指します。

## 前回の復習

第2回では `if` や `while` を用いた条件分岐とループ処理を練習しました。今回はそれらの処理を整理して再利用しやすくするための関数やモジュールに取り組みます。

## 学習内容

- 関数定義と呼び出し
- 引数と戻り値
- 組み込み関数と標準モジュール（`math`, `datetime` など）

演習では、簡単な計算処理を関数化したり、日付や数学計算のモジュールを利用してみます。

---

## 1. 関数の基本

- `def` キーワードを用いて関数を定義します。
- 処理を一箇所にまとめることで、同じコードを何度も書かずに済みます。
- 変数のスコープや戻り値の扱いに注意しながら、シンプルな関数から実践してみましょう。

```python
def greet():
    print("Hello")

greet()
```

## 2. 引数と戻り値

- 関数に値を渡す方法として位置引数、キーワード引数があります。
- 戻り値を `return` で返すことで、計算結果を呼び出し元で利用できます。
- デフォルト引数や可変長引数を利用すると、柔軟なインターフェースを持つ関数を作成できます。

```python
def add(a, b):
    return a + b

result = add(3, 4)
print(result)
```

## 3. モジュールの活用

- Python には `math` や `datetime` などの便利な標準モジュールが用意されています。
- `import` 文を使ってモジュールを読み込み、必要な関数やクラスを利用します。
- 自作モジュールを作成して複数ファイルに分割することで、大きなプログラムでも管理しやすくなります。

```python
# 例: 三角形の面積を求める関数
import math

def triangle_area(base, height):
    return base * height / 2

print(triangle_area(5, 3))
print(math.sin(math.pi / 2))
```

## 演習課題

- 2 つの数値を受け取り足し算して返す関数 `add` を定義し、呼び出す。
- 名前を受け取ってあいさつを返す関数 `greet` を作成する。
- `math` モジュールを読み込み、円の面積を計算する。
- `datetime` モジュールで今日の日付を表示する。
- 自作関数を別ファイルに保存し、モジュールとしてインポートする。
