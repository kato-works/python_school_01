# 第5回：表形式データの処理（Pandas入門）

表計算ソフトのようなデータ操作をPythonで行えるライブラリ「Pandas」を学習します。実務でよく扱うCSVファイルを読み込み、集計やデータクレンジングを体験します。

## 前回の復習

第4回ではファイル読み書きと文字列処理の基礎を学びました。今回はその知識を活かし、より大きな表形式データを効率的に扱うためにPandasを導入します。

## 学習内容

- Pandasとは
- CSV読み込み、行列の抽出・フィルター
- 実務例：売上表の集計やデータクレンジング

簡単な売上データを題材に、不要な列の削除やグループ化集計を実践します。

### インストール

```bash
pip install pandas
```

---

## 1. Pandasの基本操作

- `DataFrame` と `Series` の概念を理解し、データ構造に慣れます。
- `pd.read_csv()` でCSVを読み込み、`head()` や `describe()` を使って内容を確認します。
- 表形式データならではのインデックスや列名の扱い方を学びます。

```python
import pandas as pd

df = pd.read_csv('sales.csv')
print(df.head())
```

## 2. データの抽出とフィルタリング

- 行・列の選択には `loc` と `iloc` を使用します。
- 条件式を用いた行フィルタや、列の追加・削除の方法を紹介します。
- 欠損値の処理やデータ型変換といったクレンジングの基本操作もここで取り上げます。

```python
high = df[df['amount'] > 100]
print(high[['category', 'amount']])
```

## 3. 集計と出力

- `groupby` や `pivot_table` を使ってデータを集計する方法を実践します。
- 集計結果を新しいCSVとして保存し、Excelへの受け渡しや可視化ツールへの連携方法に触れます。

```python
import pandas as pd

df = pd.read_csv('sales.csv')
summary = df.groupby('category')['amount'].sum()
print(summary)
summary.to_csv('summary.csv')
```

## 演習課題

- Pandas で "sales.csv" を読み込み、先頭 5 行を表示する。[解答](../example/session05_example.md#演習課題-1)
- 特定の列で条件フィルターを行い、抽出結果を確認する。[解答](../example/session05_example.md#演習課題-2)
- 列 "amount" の平均値を求める。[解答](../example/session05_example.md#演習課題-3)
- "category" ごとの合計を `groupby` で集計する。[解答](../example/session05_example.md#演習課題-4)
- 加工した結果を新しい CSV ファイルに保存する。[解答](../example/session05_example.md#演習課題-5)
