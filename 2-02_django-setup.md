# Django：環境構築
  
Djangoインストール以降の作業は基本的にDjangoの公式ドキュメントを参考にした。
  
  

＜参考URL＞
Django公式ドキュメント：はじめての Django アプリ作成、その 1  
https://docs.djangoproject.com/ja/1.11/intro/tutorial01/  
  
  
＜前提条件＞  
・pyenv と virtualenv はインストール済みであること  
  
  
  
#### ■作業手順
```bash
# 作業ディレクトリ作成
$ mkdir Django

# 作業ディレクトリへ移動
$ cd Django

# 仮想環境の作成
$ pyenv virtualenv 3.6.0 Django_Test
Requirement already satisfied: setuptools in /Users/XXXXX/.pyenv/versions/3.6.0/envs/Django_Test/lib/python3.6/site-packages
Requirement already satisfied: pip in /Users/XXXXX/.pyenv/versions/3.6.0/envs/Django_Test/lib/python3.6/site-packages

# インストール済 Pythonバージョン 一覧
$ pyenv versions
* system
  2.7.9
  3.6.0/envs/Django_Test
  Django_Test

# 現在(カレントディレクトリ)のPythonバージョン確認
$ python -V
Python 3.6.0

# 現在（カレントディレクトリ)のPythonバージョンを設定
# 以下のコマンドでは、先程作成した仮想環境「Django_Test」のPython3.6.0を指定
$ pyenv local Django_Test

# 設定後は（）の中に現在のバージョンが表示される
(Django_Test) $ python -V
Python 3.6.0

$ pyenv versions
  system
  2.7.9
  3.6.0
  3.6.0/envs/Django_Test
* Django_Test (set by /Users/XXXXX/Django/.python-version)

# Djangoインストール準備：pipのアップグレード
$ pip install --upgrade pip
Requirement already up-to-date: pip in /Users/XXXXX/.pyenv/versions/3.6.0/envs/Django_Test/lib/python3.6/site-packages

# Djangoインストール準備：setuptoolsアップグレード
$ pip install --upgrade setuptools
Collecting setuptools
  Using cached setuptools-36.6.0-py2.py3-none-any.whl
Installing collected packages: setuptools
  Found existing installation: setuptools 28.8.0
    Uninstalling setuptools-28.8.0:
      Successfully uninstalled setuptools-28.8.0
Successfully installed setuptools-36.6.0

# Djangoインストール
$ pip install django
Collecting django
  Downloading Django-1.11.6-py2.py3-none-any.whl (6.9MB)
    100% |████████████████████████████████| 7.0MB 221kB/s
Collecting pytz (from django)
  Downloading pytz-2017.3-py2.py3-none-any.whl (511kB)
    100% |████████████████████████████████| 512kB 2.5MB/s
Installing collected packages: pytz, django
Successfully installed django-1.11.6 pytz-2017.3

# インストール済みパッケージ一覧
# （※カレントディレクトリの環境にインストールされているパッケージ一覧）
$ pip freeze
Django==1.11.6
pytz==2017.3

$ ll
total 8
drwxr-xr-x  3  admin  102 11  1 11:12 .
drwx------  8  admin  272 11  1 10:46 ..
-rw-r--r--  1  admin   12 11  1 11:17 .python-version

# Djangoプロジェクト作成
$ django-admin.py startproject mysite

$ ll
total 8
drwxr-xr-x  4  admin  136 11  1 11:21 .
drwx------  8  admin  272 11  1 10:46 ..
-rw-r--r--  1  admin   12 11  1 11:17 .python-version
drwxr-xr-x  4  admin  136 11  1 11:21 mysite

$ ll mysite/
total 8
drwxr-xr-x  4  admin  136 11  1 11:21 .
drwxr-xr-x  4  admin  136 11  1 11:21 ..
-rwxr-xr-x  1  admin  804 11  1 11:21 manage.py
drwxr-xr-x  6  admin  204 11  1 11:21 mysite

$ tree mysite
mysite
├── manage.py
└── mysite
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py

1 directory, 5 files

# プロジェクトのルートディレクトリへ移動
$ cd mysite
  
# 開発用サーバー起動
$ python manage.py runserver

# ブラウザで http://127.0.0.1:8000/ => Welcome to Django が表示されていればOK

```
