# 第7回：Webからの情報取得（スクレイピング入門）

以下は、回答編です。

## 演習課題 1
`requests` で任意の Web ページを取得し、ステータスコードを表示する。
```python
import requests
resp = requests.get("https://example.com")
print(resp.status_code)
```

## 演習課題 2

HTML からタイトルタグの内容を抽出する。

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(resp.text, "html.parser")
print(soup.title.text)
```

## 演習課題 3

リスト化された項目を `select` で取得し、1 件ずつ表示する。

```python
for item in soup.select("li"):
    print(item.get_text(strip=True))
```

## 演習課題 4

取得間隔を 1 秒以上空けて複数ページを巡回する。

```python
import time
urls = ["https://example.com/page1", "https://example.com/page2"]
for url in urls:
    resp = requests.get(url)
    print(url, resp.status_code)
    time.sleep(1)
```

## 演習課題 5

ページから画像の URL を取り出し、一覧表示する。

```python
for img in soup.select("img"):
    print(img["src"])
```
