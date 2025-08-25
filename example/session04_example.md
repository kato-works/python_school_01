# 第4回：ファイル操作と文字列処理

以下は、回答編です。

## 演習課題 1
"sample.txt" を読み込み、行数を数えて表示する。
```python
with open("sample.txt", encoding="utf-8") as f:
    lines = f.readlines()
print(len(lines))
```

## 演習課題 2

カンマ区切りの文字列を分割し、リストにする。

```python
text = "a,b,c"
items = text.split(",")
print(items)
```

## 演習課題 3

テキスト内の特定の単語を別の単語に置き換えて表示する。

```python
msg = "I like apple"
print(msg.replace("apple", "orange"))
```

## 演習課題 4

"data.csv" を読み取り、1 行ずつ print する。

```python
import csv
with open("data.csv", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

## 演習課題 5

書き込み用ファイルを作成し、任意の文字列を数行保存する。

```python
lines = ["first", "second", "third"]
with open("out.txt", "w", encoding="utf-8") as f:
    for line in lines:
        f.write(line + "\n")
```

## 演習課題 6

ログファイルから "ERROR" を含む行だけを新しいファイルに書き出す。

```python
with open("app.log", encoding="utf-8") as src, \
     open("error.log", "w", encoding="utf-8") as dst:
    for line in src:
        if "ERROR" in line:
            dst.write(line)
```

