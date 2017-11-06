# Python：Django 基礎
  
[&lt;&lt;目次へ戻る](https://github.com/kenshin-itahana/docs-python/blob/master/README.md)
  
#### ■公式マニュアル
https://docs.djangoproject.com/ja/1.11/  
  
  
  
#### ■Djangoパッケージ
便利パッケージがいろいろある  
https://djangopackages.org/  
  
  

#### ■バッチ作成方法
http://wannabe-jellyfish.hatenablog.com/entry/2017/03/19/230958  
  
  
  
#### ■ディレクトリツリー
```bash
mysite				ルートディレクトリ（※ディレクトリ名の変更可）  
├── manage.py		        コマンドラインユーティリティ  
└── mysite			本プロジェクトのパッケージ名  
　　　├── __init__.py		このファイルが保存されているディレクトリがPythonパッケージであることを定義している空ファイル  
　　　├── settings.py	        設定ファイル  
　　　├── urls.py		URLディスパッチャー  
　　　└── wsgi.py		プロジェクトをサーブするためのWSGI互換Webサーバーとのエントリーポイント  
```
  
  
  
####  ■モデル
  
##### ＜モデルの作成/更新＞
１．models.py　モデルを定義/変更する  
  
２．１．の変更のためのマイグレーションファイルを作成する為に以下のコマンドを実行する  
  
```bash  
$ python manage.py makemigrations  
```  
  
３．DBへ変更を適用  
```bash  
$ python manage.py migrate
```  

※マイグレーションの作成とDB適用のコマンドが分割されている理由  
マイグレーションをバージョン管理システムにコミットし、アプリとともに配布するため。  
これにより、他の開発者との開発環境とソースの共有が容易になり、チーム開発を円滑に進めることができる。  
  


  
#### ■Django Admin（Django管理インタフェース）
Djangoでは管理インタフェースの構築は無駄な作業と捉えて、そのすべてを完全に自動化している。
  

＜管理ユーザーを作成する＞
```bash
$ python manage.py createsuperuser

Username: admin(任意のユーザー名)

Email address: hoge@who.bar

Password: ********
Password (again): ********
Superuser created successfully.
```
  
  

#### ■ビューのレスポンス
ビューが返すレスポンスは以下の２パターンのみ。

１．HttpResponse  
２．例外  
  
  
  
#### ■プロジェクト作成
  
１．プロジェクト配備用ディレクトリを作成
```bash
$ mkdir mysite
```
  
２．Djangoプロジェクト作成
```bash
$ django-admin startproject mysite
```

３．作成したプロジェクトのディレクトリツリーの確認
```bash
　　$ tree mysite
　　mysite
　　├── manage.py
　　└── mysite
   　　 ├── __init__.py
    　　├── settings.py
    　　├── urls.py
    　　└── wsgi.py

　　1 directory, 5 files
```

４．プロジェクトのルートディレクトリに移動
```bash
　　$ ls -al
　　drwxr-xr-x  4   admin  136 11  2 13:34 .
　　drwxr-xr-x  4   admin  136 11  2 13:34 ..
　　drwxr-xr-x  6   admin  204 11  2 13:34 mysite
　　-rwxr-xr-x  1   admin  805 11  2 13:34 manage.py
```
  
５．アプリケーションの作成  
```bash
　　$ python manage.py startapp myapp
```
  
６．プロジェクトのディレクトリツリーの確認  
```bash
　　$ tree mysite/
　　mysite/
　　　　├── api （←５．で作成したアプリケーションはこの階層に作成される）
　　　　│   　　　├── __init__.py
　　　　│   　　　├── admin.py
　　　　│   　　　├── apps.py
　　　　│   　　　├── migrations
　　　　│   　　　│   　　　└── __init__.py
　　　　│   　　　├── models.py
　　　　│   　　　├── tests.py
　　　　│   　　　└── views.py
　　　　├── mysite
　　　　│   　　　├── __init__.py
　　　　│   　　　├── __pycache__
　　　　│   　　　│   　　　├── __init__.cpython-36.pyc
　　　　│   　　　│   　　　└── settings.cpython-36.pyc
　　　　│   　　　├── settings.py
　　　　│   　　　├── urls.py
　　　　│   　　　└── wsgi.py
　　　　└── manage.py
```
  
  
  
#### ■開発用サーバーの起動

１．プロジェクトのルートディレクトリ直下へ移動

２．サーバー起動コマンド実行
```bash
　　$ python manage.py runserver
```
