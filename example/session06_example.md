# 第6回：Excelの自動処理（OpenPyXL / Pandas）

以下は、回答編です。

## 演習課題 1
`"sample.xlsx"` を読み込み、A1 の値を表示する。
```python
from openpyxl import load_workbook
wb = load_workbook("sample.xlsx")
ws = wb.active
print(ws["A1"].value)
```

## 演習課題 2

新規シートを作成して任意のデータを 5 行書き込む。

```python
ws2 = wb.create_sheet("Data")
for i in range(1, 6):
    ws2.append([f"item {i}", i])
wb.save("sample.xlsx")
```

## 演習課題 3

`DataFrame` を Excel に書き出してみる。

```python
import pandas as pd
df = pd.DataFrame({"A": [1, 2], "B": [3, 4]})
df.to_excel("df.xlsx", index=False)
```

## 演習課題 4

既存のテンプレートファイルを読み込み、セルの書式を変更して保存する。

```python
from openpyxl.styles import Font
tpl = load_workbook("template.xlsx")
ws = tpl.active
ws["A1"].font = Font(bold=True)
tpl.save("result.xlsx")
```

## 演習課題 5

複数シートにデータを書き込む処理を試す。

```python
with pd.ExcelWriter("multi.xlsx") as writer:
    pd.DataFrame({"A": [1, 2]}).to_excel(writer, sheet_name="first", index=False)
    pd.DataFrame({"B": [3, 4]}).to_excel(writer, sheet_name="second", index=False)
```
