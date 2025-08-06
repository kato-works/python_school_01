# 第8回：まとめ・応用演習

以下は、回答編です。

## 演習課題 1
業務で使えそうな自動化アイデアを 3 つ書き出す。
- 受信メールの整理  
- 売上データの集計  
- ログのエラー抽出  

## 演習課題 2
必要な入力データと出力結果を紙にまとめる。
| Input      | Output             |
|------------|--------------------|
| mails.csv  | important.xlsx     |
| sales.csv  | sales_summary.csv  |
| access.log | error.log          |

## 演習課題 3
小さなスクリプトを作り、データの読み込みから出力まで一連の流れを実装する。
```python
import pandas as pd
df = pd.read_csv("mails.csv")
df[["Date", "From", "Subject"]].to_excel("mails.xlsx", index=False)
```

## 演習課題 4

作ったコードを他の人に共有し、改善点をフィードバックしてもらう。\
（例: 社内チャットで共有し、コメントをもらう）

## 演習課題 5

今後学びたいことや応用したいことをメモしておく。

* Web API の活用
* 自動テストの導入
* クラウド連携

```
```

