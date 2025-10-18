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

```python
import requests

resp = requests.get('https://example.com')
print(resp.status_code)
```

## 2. BeautifulSoupによる解析

- `BeautifulSoup` オブジェクトから `find` / `find_all` を使って要素を抽出する方法を学びます。
- CSSセレクターを使った検索や、テキストの整形・クリーンアップのコツを解説します。
- 取得したデータをリストやCSVにまとめる処理を実装し、簡単なクローラーを作成します。

```python
from bs4 import BeautifulSoup

html = '<p class="msg">hi</p>'
soup = BeautifulSoup(html, 'html.parser')
print(soup.find('p').text)
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
