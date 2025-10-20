# 第7回：Webからの情報取得（スクレイピング入門）

インターネット上のデータを自動で取得する「Webスクレイピング」を体験します。`requests` でページを取得し、`BeautifulSoup` で必要な部分を抽出する基本的な流れを学びます。

## 前回の復習

第6回では OpenPyXL と Pandas を使い、Excel ファイルを自動で生成・加工する方法を学びました。今回は外部サイトからデータを取得するスクレイピングに挑戦します。

## 学習内容

- `requests` と `BeautifulSoup`
- 実務例：競合の価格情報、天気情報の取得

対象サイトの利用規約やマナーを確認しつつ、手軽に情報を集める方法を身につけましょう。

### インストール

```bash
pip install requests beautifulsoup4
```

---

## 1. スクレイピングの基本

- HTTP通信の仕組みとステータスコードを理解します。
- `requests.get()` を用いてHTMLを取得し、エラー処理やヘッダー設定の方法を学びます。
- ブラウザの開発者ツールを使い、欲しい情報が含まれるタグを事前に調査する手順を紹介します。

### HTTP通信とは？

Webサイトにアクセスするとき、ブラウザはサーバーに「リクエスト」と呼ばれる要求を送り、サーバーは「レスポンス」としてデータを返します。これがHTTP（HyperText Transfer Protocol）通信です。リクエストにはアクセス先のURLや取得方法（GETやPOSTなど）が含まれ、レスポンスにはステータスコード（200なら成功、404ならページなしなど）や返却されるHTMLなどのデータが含まれます。スクレイピングでは、ブラウザの代わりにPythonがリクエストを送り、返ってきたレスポンスを解析します。

### HTMLとは？

サーバーから返されるデータの代表例がHTML（HyperText Markup Language）です。HTMLはタグ（`<h1>` や `<p>` など）を使ってページの構造や意味を表現するマークアップ言語で、ブラウザはこの構造をもとにページを表示します。スクレイピングでは、HTMLのどのタグに欲しい情報が入っているかを調べ、プログラムでピンポイントに抜き出すのが基本的な作業になります。

```python
import requests

resp = requests.get('https://example.com')
print(resp.status_code)
```

HTMLデータの取り出し

```python
html_text = resp.text
print(html_text)
```

## 2. BeautifulSoupによる解析

- `BeautifulSoup` オブジェクトから `find` / `find_all` を使って要素を抽出する方法を学びます。
- CSSセレクターを使った検索や、テキストの整形・クリーンアップのコツを解説します。
- XPath を併用して要素を取得する方法と、ブラウザの開発者ツールで XPath を調べる手順を紹介します。
- 要素の属性値（`href` など）を取り出して、リンク一覧のような情報にまとめる例を示します。
- 取得したデータをリストやCSVにまとめる処理を実装し、簡単なクローラーを作成します。

### 基本：タグ名で取得

```python
from bs4 import BeautifulSoup

html = """
<html>
  <body>
    <h1>スクレイピング入門</h1>
    <p class="msg">こんにちは</p>
    <p class="msg">こんばんは</p>
  </body>
</html>
"""

soup = BeautifulSoup(html, 'html.parser')

# 最初の <p> 要素だけを取得
first_paragraph = soup.find('p')
print(first_paragraph.text)  # => こんにちは

# 複数要素をリストで取得
all_paragraphs = soup.find_all('p')
for p in all_paragraphs:
    print(p.text)
```

### CSSセレクターでの取得

```python
# class="msg" を持つ段落のみ取得
messages = soup.select('p.msg')
for msg in messages:
    print(msg.get_text(strip=True))

# 子孫セレクターや属性セレクターも利用可能
headline = soup.select_one('body > h1')
print(headline.string)
```

#### ブラウザの開発者ツールで CSS セレクター を調べる手順

1. Chrome や Edge で対象ページを開き、右クリックから「検証」を選択して開発者ツールを開きます。
2. Elements（要素）タブで目的の要素を選択した状態で、右クリック → **Copy > Copy selector** を選びます。
3. 取得した文字列を上記の `soup.select('...')` の `'...'` の部分に貼り付けると、同じ要素を Python から取得できます。

### 属性値の取り出し

```python
html = """
<ul>
  <li><a href="https://example.com/news">ニュース</a></li>
  <li><a href="https://example.com/blog">ブログ</a></li>
</ul>
"""

soup = BeautifulSoup(html, 'html.parser')

for link in soup.select('a'):
    title = link.get_text(strip=True)
    url = link.get('href')  # 属性名を指定して取得
    print(f"{title}: {url}")
```


## 3. マナーと応用例

- robots.txt や利用規約の確認、アクセス頻度を抑えるなど、スクレイピングのマナーを守る重要性を説明します。
- 競合サイトの価格情報を定期取得したり、天気予報サイト（例：Yahoo!天気・災害 https://weather.yahoo.co.jp/weather/jp/13/4410.html ）から必要な情報だけを抜き出す実践例を紹介します。

```python
import requests
from bs4 import BeautifulSoup

url = 'https://weather.yahoo.co.jp/weather/jp/13/4410.html'
headers = {
    'User-Agent': 'Mozilla/5.0',  # 一般的なブラウザを装うことで403エラーを避ける
}

resp = requests.get(url, headers=headers)
resp.raise_for_status()
soup = BeautifulSoup(resp.text, 'html.parser')

# 週間予報テーブルから今日・明日の行だけを取り出す
week_rows = soup.select('#yjw_week table tr')
for row in week_rows[1:3]:  # 0番目はヘッダー行なのでスキップ
    cols = [c.get_text(strip=True) for c in row.select('td')]
    if len(cols) < 4:
        continue
    date, weather, high, low = cols[0], cols[1], cols[2], cols[3]
    print(f'{date}: {weather} / 最高{high} / 最低{low}')
```

## 演習課題

- `requests` で任意の Web ページを取得し、ステータスコードを表示する。
- HTML からタイトルタグの内容を抽出する。
- リスト化された項目を `select` で取得し、1 件ずつ表示する。
- 取得間隔を 1 秒以上空けて複数ページを巡回する。
- ページから画像の URL を取り出し、一覧表示する。
