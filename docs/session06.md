# 第6回：Excelの自動処理（OpenPyXL / Pandas）

ExcelファイルをPythonで操作する方法を学びます。OpenPyXLやPandasを用いて、数式や書式を含むデータの読み書きを体験し、見積書や月報の自動生成につなげます。

## 学習内容

- Excelの読み書き（数式/書式も含む）
- 実務例：見積書や月報の自動生成

既存のテンプレートファイルを利用して、複数シートへの出力やフォーマットの調整を試してみましょう。

### インストール

```bash
pip install openpyxl pandas
```

---

## 1. OpenPyXLによる基本操作

- `Workbook` と `Worksheet` の概念を理解し、セルの読み書きを行います。
- 既存のExcelファイルを開き、値を取得したり更新する方法を解説します。
- 新規ファイルを作成して保存するまでの流れを実践します。

```python
from openpyxl import Workbook

wb = Workbook()
ws = wb.active
ws['A1'] = 'Hello'
wb.save('hello.xlsx')
```

## 2. 書式設定と数式

- セルの背景色やフォントを変更する書式設定の方法を紹介します。
- `SUM` などの関数式をセルに設定し、計算式付きのシートを自動生成します。
- テンプレートとなるExcelを読み込み、既存の書式を保ったままデータだけを差し替えるテクニックを学びます。

```python
from openpyxl.styles import Font
ws['A2'] = '=SUM(1, 2)'
ws['A1'].font = Font(bold=True)
wb.save('styled.xlsx')
```

## 3. Pandasとの連携

- 大量の表データを扱う場合は、一度 `DataFrame` で加工し、`to_excel()` で出力すると効率的です。
- 複数シートへの書き込みや、グラフ作成用のデータ整形など、実務でよくある処理を例示します。

```python
from openpyxl import load_workbook
import pandas as pd

wb = load_workbook('template.xlsx')
ws = wb['Sheet1']
ws['B2'] = 1000  # 値の更新

sales = pd.read_csv('sales.csv')
sales.to_excel('report.xlsx', index=False)
wb.save('result.xlsx')
```

## 演習課題

- "sample.xlsx" を読み込み、A1 の値を表示する。
- 新規シートを作成して任意のデータを 5 行書き込む。
- `DataFrame` を Excel に書き出してみる。
- 既存のテンプレートファイルを読み込み、セルの書式を変更して保存する。
- 複数シートにデータを書き込む処理を試す。
