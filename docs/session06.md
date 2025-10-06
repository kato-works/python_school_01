# 第6回：Excelの自動処理（OpenPyXL / Pandas）

ExcelファイルをPythonで操作する方法を学びます。OpenPyXLやPandasを用いて、数式や書式を含むデータの読み書きを体験し、見積書や月報の自動生成につなげます。

## 前回の復習

第5回ではPandasを使ったCSVの集計やデータクレンジングを学びました。今回はその応用として、Excelファイルを直接操作し、業務に役立つ帳票を自動生成します。

## 学習内容

- Excelの読み書き（数式/書式も含む）
- 実務例：見積書や月報の自動生成

既存のテンプレートファイルを利用して、複数シートへの出力やフォーマットの調整を試してみましょう。

### インストール

```bash
pip install openpyxl pandas
```

エラーが出るようであれば、

```bash
pip install --proxy=172.16.10.41:8080 openpyxl pandas
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

既存のファイルを開いて値を取得する例です。

```python
from openpyxl import load_workbook

wb = load_workbook('hello.xlsx')
ws = wb.active
print(ws['A1'].value)
```

## 2. 書式設定と数式

- セルの背景色やフォントを変更する書式設定の方法を紹介します。
- `SUM` などの関数式をセルに設定し、計算式付きのシートを自動生成します。
- テンプレートとなるExcelを読み込み、既存の書式を保ったままデータだけを差し替えるテクニックを学びます。

```python
from openpyxl import Workbook, load_workbook
from openpyxl.styles import Font, PatternFill

wb = Workbook()
ws = wb.active

# フォントや背景色の設定
ws['A1'] = '合計'
ws['A1'].font = Font(bold=True, color='FFFFFF')  # 太字・白文字
ws['A1'].fill = PatternFill(fill_type='solid', fgColor='4F81BD')  # 背景を青に

# 数式を設定
ws['A2'] = '=SUM(1, 2)'
ws['A2'].font = Font(color='7030A0')  # 数式セルは紫文字に
ws['A2'].fill = PatternFill(fill_type='solid', fgColor='E5E0EC')

wb.save('styled.xlsx')

# 数式そのものを取得
formula = ws['A2'].value  # '=SUM(1, 2)'

# 数式の計算結果を取得（Excel などで再計算済みである必要があります）
wb_result = load_workbook('styled.xlsx', data_only=True)
ws_result = wb_result.active
result = ws_result['A2'].value  # -> 再計算済みなら 3

print(formula, result)
```

FFFFFFや、4F81BDは、赤緑青の割合を表したカラーコードです。以下のようなサイトを参考にしてください。

https://www.colordic.org/

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
