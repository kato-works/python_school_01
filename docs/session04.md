# 第4回：ファイル操作と文字列処理

ファイルの読み書き方法と、テキストを扱う際の基本的な文字列処理を学びます。実務例として、ログファイルを整形する簡単なスクリプトを作成します。

## 学習内容

- ファイル読み書き（CSV, TXT）
- 文字列の分割・置換
- 実務例：ログファイルの自動整形

実際にサンプルデータを読み込み、不要な行を除いたりフォーマットを変える演習を行います。

---

## 1. 基本的なファイル操作

- `open` 関数と `with` 構文を使った安全なファイルの読み書きを学びます。
- テキストファイルだけでなく CSV ファイルを扱う際の注意点も確認します。
- 読み込んだ内容を一行ずつ処理する方法や、書き込みモードの違い (`w`, `a`) にも触れます。

```python
with open('sample.txt', 'w', encoding='utf-8') as f:
    f.write('hello')

with open('sample.txt', 'r', encoding='utf-8') as f:
    print(f.read())
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

## 3. 実務で役立つログ整形

- 例として、アクセスログやエラーログを読み込み、必要な行だけを抽出して CSV にまとめる処理を作成します。
- 文字列処理とファイル出力を組み合わせ、整形後のデータをグラフ化するなど、次の分析ステップへつなげる方法に触れます。

```python
# 例: ログファイルから日付とメッセージを抽出
cleaned = []
with open('sample.log', 'r', encoding='utf-8') as f:
    for line in f:
        if 'ERROR' in line:
            date, msg = line.split(' - ', 1)
            cleaned.append(f'{date},{msg.strip()}')

with open('error.csv', 'w', encoding='utf-8') as f:
    f.write('\n'.join(cleaned))
```

## 演習課題

- "sample.txt" を読み込み、行数を数えて表示する。
- カンマ区切りの文字列を分割し、リストにする。
- テキスト内の特定の単語を別の単語に置き換えて表示する。
- "data.csv" を読み取り、1 行ずつ `print` する。
- 書き込み用ファイルを作成し、任意の文字列を数行保存する。
- ログファイルから "ERROR" を含む行だけを新しいファイルに書き出す。
