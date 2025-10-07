# 第1回：導入とPythonの基本構文

この回では、なぜプログラミングを学ぶのかを確認し、Python の環境構築から基本的な構文を学びます。Jupyter Notebook を使った実行方法も紹介します。

[Teamsの要約ページ](https://katohicom-my.sharepoint.com/:v:/g/personal/shohei-kishimoto_kato-works_co_jp/EcLdwCuRbDhLvfZ3upEIk1sBTALju6SYwF5X6BD8J9Ui9Q?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=c5eDYq)

## 学習内容

- なぜプログラミングを学ぶのか？
- Python のインストール方法と Jupyter Notebook 紹介
- 変数、`print`、四則演算、コメント

Python に慣れるため、簡単な計算や文字列操作を実際に入力しながら学習していきましょう。

## 1. なぜプログラミングを学ぶのか？

- **業務効率化**: 手作業で行っているデータ整理やレポート作成を自動化し、作業時間を短縮できます。
- **再現性の高い処理**: 決まった手順をコード化することで、誰が実行しても同じ結果を得られます。
- **新しいアイデアの実現**: データ分析や Web 連携など、ツールを自作することで業務改善の幅が広がります。

## 2. Python のインストール方法と Jupyter Lab 紹介

1. 以下の公式サイトから Python をダウンロードします。
   
   https://www.python.org/downloads/ \
   執筆時点の最新バージョン（3.13.7）
   
   <img width="718" height="514" alt="image" src="https://github.com/user-attachments/assets/c93ecf3f-851e-4775-b43a-0e31ddbce1ae" />

1. インストーラを実行し、Python を実行できるようにします。
   
   インストーラーで「Add Python to PATH」にチェックを入れるのを忘れないようにしましょう。
   
   <img width="656" height="405" alt="image" src="https://github.com/user-attachments/assets/06625925-f03c-4663-ab2f-cc5c593d68b1" />

1. Windowsメニューからコマンドプロンプトを起動します。
 　
   <img width="784" height="680" alt="image" src="https://github.com/user-attachments/assets/0b21fa07-ae58-4a56-8894-148a2b1a9be8" />
   
   (慣れてくれば「Win」+「R」で、ファイル名を指定して実行から、"cmd"と入力)
   
   <img width="399" height="206" alt="image" src="https://github.com/user-attachments/assets/ae6ab647-9f9c-45ec-a647-2c2d58428937" />

   ```bash
   python --version 
   ```

   と実行して"Python 3.13.7"のように表示されることを確認してください。(インストールしたバージョンで表示は変わります。)

   Pythonとだけ表示される又はインストールしたものと異なるバージョンが表示される場合には、パスの設定が失敗しているので、インストーラを再度起動し、"Modify"->"Next"->"Add Python to environment variablesにチェック"->"Install"と実施してください。
   インストール時にエラーとなる場合には、インストーラを起動する際に右クリックで"管理者として実行"（ポップアップにはOK）から起動してインストールしてください。

1. 続いて、pipを使ってJupyter Lab をインストールします。（少し時間がかかります。）

   pipは、Pythonのパッケージやライブラリをインストール、アンインストール、管理するためのパッケージ管理システムです。オンラインのPyPi(https://pypi.org/)というレポジトリ(倉庫)からライブラリをインストールしてくれます。
   
   ```bash
   pip install jupyterlab
   ```

   Successfully installed jupyterlab-X.X.Xのように表示されたらインストール成功です。
   
   ```bash
   Using cached jupyterlab-4.4.6-py3-none-any.whl (12.3 MB)
   Installing collected packages: jupyterlab
   Successfully installed jupyterlab-4.4.6
   ```

   以下のように表示された場合には、インストールが完了していません。

   ```bash
   C:\Users\U004756>pip install jupyterlab
   WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000001ABD4DF56A0>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/jupyterlab/
   WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000001ABD4DCDE50>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/jupyterlab/
   WARNING: Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000001ABD4DCDF90>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/jupyterlab/
   WARNING: Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000001ABD4DCE0D0>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/jupyterlab/
   WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000001ABD4DCE210>, 'Connection to pypi.org timed out. (connect timeout=15)')': /simple/jupyterlab/
   ERROR: Could not find a version that satisfies the requirement jupyterlab (from versions: none)
   ERROR: No matching distribution found for jupyterlab
   ```

   社内のプロキシ・名前解決に失敗しているので、以下を試してみてください。

   (172.16.10.41:8080部分は、環境に合わせて変更。)
   
   ```bash
   set https_proxy=http://172.16.10.41:8080
   pip install jupyterlab
   ```

   もしくは

   ```bash
   python -m pip install jupyterlab -i https://pypi.org/simple --default-timeout=60
   ```

1. プログラムを保存する先のフォルダを作成します。

   ```bash
   mkdir study_python_01
   cd study_python_01
   ```

   mkdirはフォルダを作成するコマンド（make directory）、cdはフォルダへ移動するコマンド（change directory）です。\
   "cd study_python_01"はコマンドプロンプトを起動したら本講習内では毎回実行してください。

1. Jupyter Lab を起動し、ブラウザ上でコードを実行する方法を紹介します。セル単位で実行できるため、学習や実験に便利です。

   ```bash
   jupyter lab
   ```
   
   <img width="800" alt="image" src="https://github.com/user-attachments/assets/cf49688a-6008-4434-9f3b-47e3dab9ecb8" />

   Jupyter Labを終了する際には、ブラウザを閉じて、コマンドプロンプトに"Ctrl"+"C"と入力してください。
   もしくはコマンドプロンプトを"X"ボタンで消してもOKです。

### Jupyter Lab とは

JupyterLabは、Pythonなどのプログラミング言語でデータ分析や可視化を行うための次世代インターフェースとして開発された統合開発環境です。

- 起源は「IPython Notebook」（2011年頃）という、Python専用のインタラクティブなノートブック形式に始まります。
- その後、Python以外の言語（RやJuliaなど）にも対応するために、Jupyter Projectとして独立（2014年）。
- JupyterLabは、Jupyter Notebookの進化版として2018年に正式リリースされました。

以下のような特徴があります。

- 複数ファイル・パネル表示が可能なタブ式UI（エディタ、ノートブック、ターミナルを並べて使える）
- Pythonだけでなく多言語対応（Julia、Rなど）
- 拡張機能が豊富（Git操作、LaTeX表示、コード補完などをプラグインで追加）
- ノートブックの再現性と共有性が高く、再利用しやすい
- Webベースで軽快に動作し、クラウドとも相性が良い（Google Colabとの類似点あり）

実務での利便性や将来性を考えると、JupyterLabは非エンジニアにもおすすめできる強力なツールです。

起動したら、NotebookのPython3をクリックすると、新規のノート（プログラミング場所）が開きます。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/d95ed8a9-df07-4f86-99fb-ae7027b72e07" />

ノートの枠にプログラムを書いて、再生ボタンを押すとプログラムが実行されます。
実行結果はプログラムを書いた枠の下に表示されます。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/01692b62-91a0-44b9-a74d-fe799499093a" />

ノートを保存するには、上のフロッピーマークを押し、ファイル名を指定（lesson01.ipynbなど）、"Rename and Save"ボタンを押します。

<img width="800" alt="image" src="https://github.com/user-attachments/assets/bff9c923-f272-4c57-a728-a898184453f0" />


## 3. 変数、`print`, 四則演算、コメント

- **変数**: 計算結果やテキストを一時的に保存しておく入れ物です。`x = 10` のように値を代入します。（数学的に左右が等しいという意味ではなく、”代入”であることがポイントです。）
- **`print` 関数**: 変数や計算結果を画面に表示する基本的な手段です。`print(x)` のように使います。
- **四則演算**: `+`, `-`, `*`, `/` を使った計算を学びます。例えば `2 + 3 * 4` の結果を求めるなど、計算順序にも注意します。
- **コメント**: `#` から行末までがコメントとなり、メモや説明を残すために活用します。

以下は簡単なサンプルコードです。

```python
# 変数に数値を代入して表示
x = 5
y = 2
print('合計:', x + y)
```

※ Pythonの変数は自由に名前をつけられますが、全角は使えません。

※ = の前後のスペースは読みやすいように入れているものです。なくても動作しますが、入れる習慣をつけましょう。全角スペースをいれると動かなくなるので気をつけましょう。

他にも、printは埋め込み表記("f''"の中に"{}"を書くと、変数を埋め込める。)も出来るので、このような書き方にも慣れておきましょう。

```python
# 変数を埋め込みで表示
score = 80
print(f'点数:{ score }')
```

## 4. 変数の型


ここでいう「型」は、変数に格納されるデータの種類を表し、どのように利用できるかに影響します。

- **`int`（整数）**: 例 `a = 10`
- **`float`（浮動小数点）**: 例 `b = 3.14`
- **`str`（文字列）**: 例 `c = "Hello"`
- **`bool`（真偽値）**: 例 `d = True`

`type()` 関数で変数の型を確認できます。

```python
a = 10
b = 3.14
c = "Hello"
d = True
print(type(a), type(b), type(c), type(d))
```

## 演習課題

Jupyter Lab 上で以下のの実習を実行してみましょう。

- 変数 x に 10、y に 3 を代入し、合計を表示する。
- 自分の名前を変数 name に入れ、`print` で「Hello, name」の形で表示する。
- 5 と 2 の割り算結果を変数 result に保存して表示する。
- 2 つの数値をかけ算し、行末にコメントで式の内容を説明する。
- 文字列と数値を組み合わせたメッセージを出力する。
