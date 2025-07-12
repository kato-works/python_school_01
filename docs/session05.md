# 第5回：表形式データの処理（Pandas入門）

表計算ソフトのようなデータ操作をPythonで行えるライブラリ「Pandas」を学習します。実務でよく扱うCSVファイルを読み込み、集計やデータクレンジングを体験します。

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

## 2. データの抽出とフィルタリング

- 行・列の選択には `loc` と `iloc` を使用します。
- 条件式を用いた行フィルタや、列の追加・削除の方法を紹介します。
- 欠損値の処理やデータ型変換といったクレンジングの基本操作もここで取り上げます。

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
