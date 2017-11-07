# Scrapy


### ■Scrapyとは
- クローリング + スクレイピング に関する様々な機能が実装されているPython製フレームワーク。  
- 主要な昨日はコンポーネントに分かれている。
- 各コンポーネントに関連するクラスなどを作成してクローリング＆スクレイピング処理を実装していく。
- いくつかの設定 + 簡潔な記述だけでスクレイピング処理が実装できる。
- Scrapy Cloud というクラウドサービスと連携でき、作成したクローラーをコマンド１つでデプロイ&実行できる。


#### クローリング
WEBページのリンクを辿りながら保存する作業

#### スクレイピング
保存したページから特定の情報を抽出する作業
  　
#### Scrapy日本語ドキュメント
Ver.1.2だけど  
http://scrapy-ja.readthedocs.io/ja/latest/index.html
  


### ■Architecture & Components
---

![Scrapy - Architecture &amp; Components -](https://github.com/kenshin-itahana/docs-python/blob/master/assets/img/Scrapy%20-%20Architecture%20&%20Components%20-.png)



### Component

##### Scrapy Engine
- フレームワーク全体のデータ処理をコントロールする部分
- コンポーネント間のデータフローを制御を担当
- 特定のアクションが発生したら、イベントを発生


##### Scheduler
- Engineからのリクエストを受け取り、キューイングとスケジューリングを担当
- scrapy.Requestオブジェクト（urlとcallback関数を持つオブジェクト）を受け取ってキューに積み、Engineから要求があった時にキューを返す


##### Downloader
- 実際のダウンロード処理を担当
- Download middleware で処理を差し込むことが可能


##### Spiders
- ユーザーが作成するカスタムクラス
- 取得したURL、抽出したい部分を記述する
- ダウンロードしたコンテンツをスクレイピングして、itemを作成


##### Item Pipeline
- スパイダーによって抽出されたアイテムの出力処理
- データのクレジング、バリデーション
- 永続化（JSON・File・DB・Mail）
  


### データフロー
　　※参照：Scrapyアーキテクチャの図  

1. EngineがSpiderからスタートURLを取得
2. EngineはスケジューラにスタートURLを持つRequestオブジェクトを渡す + 次のURLを聞く
3. Schedulerが次のURLを返す
4. Engineが取得した次のURLをDownloaderに渡す
5. Downloaderがページのデータを取得し、ResponseオブジェクトをENGINEに返す
6. Engineは受け取ったResponseをSpiderへ渡す
7. Spiderはページのデータを解析し、データが入ったItemオブジェクトと次にスクレイピングするURLを持つResponseオブジェクトをEngineに返す
8. Engineはそれらを受け取り、ItemオブジェクトをItem Pipelineに、RequestオブジェクトをSchedulerにそれぞれ渡す

※上記Step2〜7をキューがなくなるまで繰り返す

-----



### ■Scrapy インストール
```bash
$ pip install scrapy
```
  
  
### ■Scrapy 使い方（概要）
1. プロジェクト作成
2. スパイダー(クローラー)生成
3. items.py：抽出データを定義
4. スパイダー(クローラー)作成
    - 巡回開始アドレスの指定
    - 巡回条件の指定
    - データ抽出条件の指定
5. pipelines.py：取り出したitemオブジェクトの処理。DB保存等の処理などはここで行う。
6. settings.py：各種設定
7. 実行：クローリング＆スクレイピング


  
### ■Scrapy 使い方（手順）
1. プロジェクト作成
```bash
$ scrapy startproject my_project
```
  
2. スパイダー(クローラー)生成
```bash
# プロジェクトディレクトリへ移動
$ cd my_project

# Spider作成
# scrapy genspider [options] <spider-file-name> <domain(巡回対象ドメイン)>
# 　-tオプション
# 　　crawl: WEBサイトクロール用
# 　　cmlfeed: XMLフィードクロール用
# 　　csvfeed: CSVフィードクロール用
$ scrapy genspider -t crawl example example.com
```
  
3. 自動生成されるファイルを編集
  
以下のファイルをそれぞれ編集して処理を実装する。  

[ 編集するファイル ]
- items.py
- spiders/<spider-file-name>.py
- pipelines.py
- settings.py 
  
  

```bash
# プロジェクトのディレクトリツリー表示
$ tree my_project
my_project/                 # プロジェクトルートディレクトリ
├── my_project
│   ├── __init__.py         # ScrapyプロジェクトはPythonモジュール
│   ├── __pycache__
│   ├── items.py            # Item定義ファイル
│   ├── middlewares.py
│   ├── pipelines.py        # Item Pipeline定義ファイル
│   ├── settings.py         # プロジェクト設定ファイル
│   └── spiders             # Spider格納ディレクトリ
│       ├── __init__.py
│       ├── __pycache__
│       └── example.py      # Spiderファイル
└── scrapy.cfg              # クローラーのデプロイに関する設定ファイル
```
  
4. 実行：クローリング＆スクレイピング
```bash
# scrapy crawl <spider-name> [options]
$ scrapy crawl example

# JSON出力
# 　日本語を含むページをクロールする場合
# 　　settings.pyに以下を追記
# 　　FEED_EXPORT_ENCODING='utf-8'
$ scrapy crawl example -o example.json
```
  
  

### Scrapy 
### ■クローリング時の遵守事項
- データの収集/公開は著作権法に十分に配慮して行う
- robots.txtに記載されたアクセス制限を守る
- APIが用意されている場合はそちらを利用する
- サーバーへアクセスする間隔は最低でも1秒以上あけるようにする
- 会員のみが閲覧できるページは利用規約を守る
  

  
### ■参考URL
- [Pythonでスクレイピング - Scrapy入門最初の2歩目(Qiita)](https://qiita.com/ttomoaki/items/05d3dc104a695f939d63)
- [Scrapy入門（１）(Qiita)](https://qiita.com/checkpoint/items/038b59b29df8e1e384a2)
- [ざっくり理解するScrapyの使い方](https://anopara.net/2017/02/26/%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E7%90%86%E8%A7%A3%E3%81%99%E3%82%8Bscrapy%E3%81%AE%E4%BD%BF%E3%81%84%E6%96%B9/
)


