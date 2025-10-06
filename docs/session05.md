# 第5回：表形式データの処理（Pandas入門）

表計算ソフトのようなデータ操作をPythonで行えるライブラリ「Pandas」を学習します。実務でよく扱うCSVファイルを読み込み、集計やデータクレンジングを体験します。
PandasはExcel並みの集計機能を持ったオープンソースのライブラリです。

## 前回の復習

第4回ではファイル読み書きと文字列処理の基礎を学びました。今回はその知識を活かし、より大きな表形式データを効率的に扱うためにPandasを導入します。

## 学習内容

- Pandasとは
- CSV読み込み、行列の抽出・フィルター
- 実務例：売上表の集計やデータクレンジング

簡単な売上データを題材に、不要な列の削除やグループ化集計を実践します。

### インストール

```bash
!pip install pandas
```

Jupyterの再起動アイコンをクリックする。

---

## 1. Pandasの基本操作

- `DataFrame` と `Series` の概念を理解し、データ構造に慣れます。
- `pd.read_csv()` でCSVを読み込み、`head()` や `describe()` を使って内容を確認します。
- 表形式データならではのインデックスや列名の扱い方を学びます。

```python
import pandas as pd

# SSDSE-F-2023v3.csvというファイルを、文字コードShift-JISで、２行目をヘッダとして読み込む
df = pd.read_csv('SSDSE-F-2023v3.csv', encoding='sjis', header=1)
# 
df.head()
```

データの概要を把握できるdescribe()という関数が用意されているので、実行してみましょう。
列ごとの平均・標準偏差・最小値・最大値・中央値・1/4量値などが表示され、分析の指針を得ることができます。

```python
df.describe()
```

全行を表示したいときには、以下のようなオプションを設定します。

```python
# 全行表示
pd.set_option('display.max_rows', None)
```

もとに戻すには以下のように設定してください。

```python
# 元に戻す
pd.reset_option('display.max_rows')
```

全列を表示したいときには、以下のようなオプションを設定します。

```python
# 全列表示
pd.set_option('display.max_columns', None)
```

もとに戻すには以下のように設定してください。

```python
# 元に戻す
pd.reset_option('display.max_columns')
```

## 2. データの抽出とフィルタリング

- 行・列の選択には `loc` と `iloc` を使用します。
- 条件式を用いた行フィルタや、列の追加・削除の方法を紹介します。
- 欠損値の処理やデータ型変換といったクレンジングの基本操作もここで取り上げます。

df[カラム名]とすることで、Excelの列のように取り出すことができます。

```python
# '日最高気温の平均'の列のデータを表示
df['日最高気温の平均']
```

行を指定してデータを表示してみましょう。

```python
# 40行目を抽出
df.iloc[40]
```

pythonでは配列データをset()にいれることで、一意なデータにすることができます。

```python
# '月・年'というカラムにどんなデータが含まれるか一覧をチェック
set(df['月・年'])
```

月別のデータの他に、年間データが含まれているので、集計のじゃまになるので取り除きます。
データ分析では、このように目的から外れるデータを取り除くことをクレンジングと呼びます。
クレンジングには、今回のような統計対象でないデータを除く他に、外れ値やノイズも対象となることがあります。
クレンジングしすぎることで、恣意的になり分析結果に分析者によるバイアス（偏り）が入ることもあるので注意が必要です。

```python
# df['月・年'] != '年' とすることで、'年'に一致しない行が選択されます。
df_clean = df[df['月・年'] != '年']
df_clean
```

最高気温日の平均が30度を越える県・月を選択してみます。

```python
pd.set_option('display.max_rows', None)
df_over_30 = df_clean[df_clean['日最高気温の平均'] > 30.0]
print(df_over_30[['都道府県', '月・年','日最高気温の平均']])
pd.reset_option('display.max_rows')
```

## 3. 集計と出力

- `groupby` や `pivot_table` を使ってデータを集計する方法を実践します。
- 集計結果を新しいCSVとして保存し、Excelへの受け渡しや可視化ツールへの連携方法に触れます。

groupbyで、集計を行う列を指定します。集計の計算対象を配列で渡すことで、

```python
# '都道府県'で集計を行い、['日最高気温30℃以上の日数','日最低気温0℃未満の日数']それぞれの、合計（sum）を求めます。
df_group_by = df_clean.groupby('都道府県')[['日最高気温30℃以上の日数','日最低気温0℃未満の日数']].sum()
df_group_by
```

`pivot_table` を使うと Excel のピボットテーブルのように、行・列・集計値を一度に指定したクロス集計が行えます。
`order_id,date,region,product,quantity,unit_price` という列を持つ `example/sales_2023.csv` を読み込み、地域×商品別の売上合計を計算してみましょう。

```python
import pandas as pd

sales = pd.read_csv('sales_2023.csv')

# 売上金額を計算して列として追加
sales['sales_amount'] = sales['quantity'] * sales['unit_price']

pivot = pd.pivot_table(
    sales,
    index='region',      # 行方向：地域
    columns='product',   # 列方向：商品
    values='sales_amount',
    aggfunc='sum',
    fill_value=0         # 集計結果が存在しない組み合わせは 0 を入れる
)

print(pivot)
```

実行すると、地域（行）と商品（列）ごとの売上金額が一覧で確認でき、需要の高い地域や商品を素早く把握できます。

計算結果をCSVファイルとして保存してみましょう。

```python
df_group_by.to_csv("df_group_by.csv", encoding="shift-jis")
```

## 演習課題

- Pandas で "SSDSE-F-2023v3.csv" を読み込み、先頭 5 行を表示する。
- 特定の列で条件（日最低気温の平均が0℃を下回る行）フィルターを行い、抽出結果を確認する。
- 列 "標高" の平均値を求める。
- 加工した結果を新しい CSV ファイルに保存する。
