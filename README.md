# Django環境構築
このリポジトリでは、Djangoの環境構築の手順と、プロジェクトのディレクトリ構成について解説しています。
<br/>
<br/>

## 目次
- [リポジトリのクローン](#リポジトリのクローン)
- [環境構築の手順](#環境構築の手順)
  - [1. ディレクトリ構成](#1-python３のインストール)
  - [2. 開発環境構築](#2-仮想環境の設定)
  - [3. Djangoのインストール](#3-djangoのインストール)
  - [4. プロジェクトの作成](#4-プロジェクトの作成)
  - [5. 環境設定の変更](#5-環境設定の変更)
  - [6. データベースのセットアップ](#6-データベースのセットアップ)
  - [7. 開発サーバの起動](#7-開発サーバの起動)
- [ディレクトリ構成](#ディレクトリ構成)
<br/>
<br/>

## リポジトリのクローン
Python3でインストール済みでクローンだけしたい場合、以下のコマンドを実行します。
```sh
git clone git@github.com:dai-gi/djanog-introduction.git
cd djanog-introduction
source divenv/bin/activate
python3 manage.py migrate
python3 manage.py runserver
```
「[http://127.0.0.1:8000/](http://127.0.0.1:8000/)」にアクセスし、以下の画面が表示されればクローン成功です。  

![スクリーンショット 2024-03-24 0 38 13](https://github.com/dai-gi/djanog-introduction/assets/59759668/7f246a34-7090-4200-be67-36f043e8c7e2)
<br/>
<br/>

## 環境構築の手順
MacOSでPython3を使用した、Djangoの環境構築手順について解説していきます。
<br/>
<br/>

### 1. Python３のインストール
以下のコマンドを実行し、現在のバージョンを確認します。  
もし `Python 3.x.x` のようにPython3系のバージョンが表示されなければ、インストールを行いましょう。

```sh
python -V 
```
<br/>
以下のコマンドを実行し、Python3.12をインストールします。

```sh
brew install python3.12
```  
<br/>
インストールしたpython3.12の実行ファイルのシンボリックリンクを作成します。  

```sh
ln -s /usr/local/opt/python@3.12/bin/python3.12 /usr/local/bin/python3
```
これによって、pythonコマンドが実行できるようになります。`python3 -V` コマンドを実行し、`Python 3.12.x` のようにメジャーバージョンとマイナーバージョンが `3.12` と表示されていたらインストール成功です。
<br/>
<br/>

### 2. 仮想環境の設定
python3の標準機能である「venv」を使用して任意の名前で仮想環境を作成します。
ここでは「divenv」の名前で作成しています。
```sh
python3 -m venv divenv
```
これによって、仮想環境ごとにインストールするパッケージを管理することができます。
- [**-m**](https://misprochef.com/posts/python-m-option/)：Pythonが持つモジュールを実行するためのオプション  
- **venv**：仮想環境を作成するPythonの標準モジュール  
<br>
「.gitignore」ファイルを作成し、各ファイルをgitの管理化から外します。  
```sh
divenv
db.sqlite3
__pycache__
```
仮想環境を実行します。  
```sh
source divenv/bin/activate
```
ターミナルに「divenv」と表示さていれば、仮想環境に内にいることになります。  
<br/>
<br/>

### 3. Djangoのインストール
「requirements.txt」ファイルを作成し、下記を記載します。
```sh
echo "Django==5.0" >> requirements.txt
```
「requirements.txt」ファイルにパッケージを記載することでまとめてインストールすることができます。  
Pythonパッケージは [PyPI](https://pypi.org/project/Django/5.0/) で管理されています。  
<br/>

パッケージをインストールします。
```sh
pip3 install -r requirements.txt
```
- [**-r**](https://packaging.python.org/ja/latest/guides/installing-using-pip-and-virtual-environments/)：このオプションを与えることで「requirements.txt」に記載されているパッケージを全てインストールすることができます。  
<br/>
<br/>

### 4. プロジェクトの作成
任意の名前でプロジェクトを作成します。ここでは「app」の名前で作成します。  
末尾に「.」をつけることで、カレントディレクトリ直下にプロジェクトが作成されるようになります。
```sh
django-admin startproject app .
```
コマンドを実行することで、「app/」「manage.py」「db.sqlite3」が作成されます。  
<br/>
<br/>

### 5. 環境設定の変更
タイムゾーンと言語のデフォルト設定を日本に変更します。  

**app/setting.py**
```py
LANGUAGE_CODE = 'ja'

TIME_ZONE = 'Asia/Tokyo'
```
- [LANGUAGE_CODE](https://docs.djangoproject.com/en/5.0/ref/settings/#language-code)：言語のデフォルト値を変更することができます。
- [TIME_ZONE](https://docs.djangoproject.com/ja/5.0/topics/i18n/timezones/#default-time-zone-and-current-time-zone)：タイムゾーンのデフォルト値を変更することができます。
<br/>
<br/>

### 6. データベースのセットアップ
プロジェクト作成時にデフォルトで設定されたマイグレーション情報をデータベースに反映させます。
```sh
python3 manage.py migrate
```
<br/>

### 7. 開発サーバの起動
開発サーバーを起動させます。
```sh
python3 manage.py runserver
```
「[http://127.0.0.1:8000/](http://127.0.0.1:8000/)」にアクセスし、以下の画面が表示されればDjangoの環境構築は成功です。  

![スクリーンショット 2024-03-24 0 38 13](https://github.com/dai-gi/djanog-introduction/assets/59759668/7f246a34-7090-4200-be67-36f043e8c7e2)

<br/>
<br/>

## ディレクトリ構成
完成系のディレクトリ構成になります。

```py
.
├── app
│   ├── __pycach__
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── divenv
├── .gitignore
├── README.md
├── manage.py
├── db.sqlite3
└── requirements.txt
```
- **app/**  
Djangoアプリケーション全体を管理するためのフォルダ

- **_ _ pycach _ _ /**  
コンパイルされたモジュールのキャッシュが「.pyc」ファイルとして管理される。
これにより、プログラムの実行速度が速くなる。

- **_ _ init _ _.py**  
「app/」をPythonのモジュールとして認識させる役割を持ち、また、「app/」がインポートされた際に初期化したい処理を記述する場所としても機能する。

- **asgi.py**  
非同期通信を行うための設定ファイル。

- **settings.py**  
Djangoアプリケーションの設定ファイル。

- **urls.py**  
ルーティングを設定するためのファイル。

- **wsgi.py**  
WEBサーバとAPサーバ間の通信を仲介する設定ファイル。

- **divenv/**  
仮想環境を管理するフォルダ。

- **manage.py**  
仮想環境を作成するPythonの標準モジュール

- **db.sqlite3**  
SQLiteデータベースの実体。Djangoではデフォルトのデータベースとして設定されている。

- **requirements.txt**  
pythonパッケージをまとめてインストールするためのファイル。

