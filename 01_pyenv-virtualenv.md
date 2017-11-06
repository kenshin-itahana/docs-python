# Python：pyenv / virtualenv 使い方
  
[&lt;&lt;目次へ戻る](https://github.com/kenshin-itahana/docs-python/blob/master/README.md)
  

### pyenv
---
- Pythonのバージョン管理ツール
- 複数のバージョンのPythonをインストール/アンインストール/切替ができる
- Pythonのバージョン切替に使用
- 基本的にPythonのバージョンごとに管理
- 同一バージョンで複数のPython環境を管理することは不可能。
- 環境は単一なのでバージョンごとに環境切り分けはできない。
　
　

### virtualenv
---
- Pythonの仮想的な環境を作成できるツール
- 基本的にディレクトリ単位で隔離したPythonのバージョン、パッケージを管理
- ディレクトリごとにPythonバージョン/パッケージの管理可能
　
　


### pyenv / virtualenv インストール
---
事前にHomebrewインストール

```bash
# Command Line Tools for Xcodeのインストール
$ xcode-select --install

# Homebrewインストール
$ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

$ brew -v
Homebrew 1.3.6
Homebrew/homebrew-core (git revision 5026; last commit 2017-11-02)

```

　

pyenv と pyenv-virtualenv インストール

```bash
$ brew install pyenv pyenv-virtualenv
$ echo 'export PYENV_ROOT="${HOME}/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="${PYENV_ROOT}/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```

　
　
### pyenv：コマンド
---

■pyenv：インストール可能なPythonバージョン一覧

```bash
$ pyenv install -l
```

　

■pyenv：指定バージョンのPythonインストール

```bash
$ pyenv install 3.6.3
```

  
■pyenv：インストール済みPythonバージョン一覧

```bash
$ pyenv versions
* system (set by /Users/XXXXX/.pyenv/version)
  3.6.3

#＜現在のPythonバージョンの確認＞
$ python -V
Python 2.7.10

```

　
　
　
### virtualenvによるPython仮想環境の作成
---

```bash
# 隔離環境用のディレクトリを作成
#（※必須作業：virtualenvはディレクトリ毎に環境を管理するのでこの作業は必須）
$ mkdir pyenv_test
$ pwd
/Users/XXXXX/work/pyenv_test

# 作成したディレクトリへ移動（※必須作業）
$ cd pyenv_test

# 隔離環境を構築したいディレクトリ下で下記コマンドを実行
pyenv_test $ pyenv virtualenv 3.4.3 test
pyenv_test $ pyenv local test

(test)$    # <- 設定したpyenv-virtualenvが()内に表示される

(test)$ pyenv versions
  system
  3.4.3
* test (set by /Users/XXXXX/work/pyenv_test/.python-version)
```


