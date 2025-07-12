# 第7回：Webからの情報取得（スクレイピング入門）

インターネット上のデータを自動で取得する「Webスクレイピング」を体験します。`requests` でページを取得し、`BeautifulSoup` で必要な部分を抽出する基本的な流れを学びます。

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

## 2. BeautifulSoupによる解析

- `BeautifulSoup` オブジェクトから `find` / `find_all` を使って要素を抽出する方法を学びます。
- CSSセレクターを使った検索や、テキストの整形・クリーンアップのコツを解説します。
- 取得したデータをリストやCSVにまとめる処理を実装し、簡単なクローラーを作成します。

## 3. マナーと応用例

- robots.txt や利用規約の確認、アクセス頻度を抑えるなど、スクレイピングのマナーを守る重要性を説明します。
- 競合サイトの価格情報を定期取得したり、天気予報サイトから必要な情報だけを抜き出す実践例を紹介します。

```python
import requests
from bs4 import BeautifulSoup

resp = requests.get('https://example.com')
soup = BeautifulSoup(resp.text, 'html.parser')
for item in soup.select('.price'):
    print(item.get_text(strip=True))
```
