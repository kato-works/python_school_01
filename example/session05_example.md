# 第5回：表形式データの処理（Pandas入門）

以下は、回答編です。

## 演習課題 1
"sales.csv" を読み込み、先頭の行を表示する。
```python
import pandas as pd

df = pd.read_csv("sales.csv")
print(df.head())
```

## 演習課題 2
金額が 150 を超える行のみ抽出する。
```python
threshold = 150
filtered = df[df["amount"] > threshold]
print(filtered)
```

## 演習課題 3
"amount" 列の平均値を計算する。
```python
mean_amount = df["amount"].mean()
print(mean_amount)
```

## 演習課題 4
カテゴリごとに金額の合計を求める。
```python
summary = df.groupby("category")["amount"].sum()
print(summary)
```

## 演習課題 5
集計結果を新しい CSV ファイルに保存する。
```python
summary.to_csv("summary.csv")
```
