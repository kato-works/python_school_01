# 第4回：ファイル操作と文字列処理

ファイルの読み書き方法と、テキストを扱う際の基本的な文字列処理を学びます。実務例として、ログファイルを整形する簡単なスクリプトを作成します。

## 前回の復習

第3回では関数の定義方法や標準モジュールの活用法を学びました。今回はそれらを応用し、ファイル操作と文字列処理を組み合わせた実務的なスクリプト作成に挑戦します。

## 学習内容

- ファイル読み書き（CSV, TXT）
- 文字列の分割・置換
- 実務例：ログファイルの自動整形

実際にサンプルデータを読み込み、不要な行を除いたりフォーマットを変える演習を行います。

---

## 0. 統計データのダウンロード

以下のサイトから、都道府県庁所在市別・月別の気象データ平年値をダウンロードします。
https://www.nstac.go.jp/use/literacy/ssdse/#SSDSE-F

以下のコードを実行するとCSVデータをダウンロードします。
今回は、このままコピーして実行してください。

```python
import requests

# 都道府県庁所在市別・月別の気象データ平年値
url = "https://www.nstac.go.jp/sys/files/SSDSE-F-2023v3.csv"

# CSVデータを取得
response = requests.get(url)
response.raise_for_status()  # エラー時は例外発生

# テキストとして読み込む
csv_text = response.text

with open('SSDSE-F-2023v3.csv', mode='w') as f:
    f.write(csv_text)
```

## 1. 基本的なファイル操作

- `open` 関数と `with` 構文を使った安全なファイルの読み書きを学びます。
- テキストファイルだけでなく CSV ファイルを扱う際の注意点も確認します。
- 読み込んだ内容を一行ずつ処理する方法や、書き込みモードの違い (`w`, `a`) にも触れます。

```python
# ファイルの書き込み
with open('sample.txt', mode='w', encoding='sjis') as f:
    f.write('hello\n')

# ファイルの読み込み
with open('sample.txt', mode='r', encoding='sjis') as f:
    line = f.read()
    print(line)
```

## 2. 文字列処理の基礎

- `split` や `join` を利用した区切り文字による分解・結合の方法を紹介します。
- `replace`、スライス、`strip` などを使って不要な文字を除去したり置き換えるパターンを解説します。
- 正規表現を使った高度な検索・置換の入り口も紹介し、実務への応用例を示します。

```python
text = 'apple,banana,orange'
items = text.split(',')
print(','.join(items))
print(text.replace('banana', 'grape'))
```

## 3. CSVの抽出をしてみよう

- 例として、必要な行だけを抽出して CSV にまとめる処理を作成します。
- 文字列処理とファイル出力を組み合わせ、整形後のデータをグラフ化するなど、次の分析ステップへつなげる方法に触れます。

```python
# 例: 統計情報から東京都のみを抽出
lines = []
with open('SSDSE-F-2023v3.csv', mode='r', encoding='sjis') as f:
    for line in f:
        if ('都道府県' in line) or ('東京都' in line):
            print(line)
            lines.append(line)

with open('tokyo.csv', mode='w',  encoding='sjis') as f:
    for line in lines:
        f.write(line)
```

## 演習課題

- "SSDSE-F-2023v3.csv" を読み込み、行数を数えて表示する。
- テキスト内の特定の単語を別の単語に置き換えて表示する。
- "SSDSE-F-2023v3.csv" を読み取り、"北海道"の出てきた回数を表示する。
- 書き込み用ファイルを作成し、任意の文字列を数行保存する。
