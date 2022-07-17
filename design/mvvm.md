# MVVM

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [MVVM](#mvvm)
  - [MVVM + Repository](#mvvm-repository)
  - [各コンポーネントのルール](#各コンポーネントのルール)
  - [View](#view)
    - [1. 役割](#1-役割)
    - [2. ViewModelとの関係性](#2-viewmodelとの関係性)
  - [ViewModel](#viewmodel)
    - [1. 役割](#1-役割-1)
    - [2. Repositoryとの関係性](#2-repositoryとの関係性)
  - [Repository](#repository)
    - [1. 役割](#1-役割-2)
    - [2. Modelとの関係性](#2-modelとの関係性)
  - [Model](#model)
    - [1. 役割](#1-役割-3)
    - [2. DBとの関係性](#2-dbとの関係性)

<!-- /code_chunk_output -->

## MVVM + Repository

- View
- ViewModel
- (Repository)
- Model
- (Remote Data Source)

## 各コンポーネントのルール

- 各コンポーネントは、下方向にのみ参照可能
- 下のメソッドを利用するなどして、データを取得する

---

## View

- `View`は、UI表示のためのコンポーネント

### 1. 役割

- UIを表示すること
  - > 例) ユーザ情報を取得し、ユーザ名とポイント数を表示
- ユーザ操作を検知すること
  - > 例) ボタン押下で画面遷移

### 2. ViewModelとの関係性

- UIを表示するために必要なデータの取得処理、ユーザ操作によるでターの更新処理を`ViewModel`に委任する
  - > 例) `ViewModel`で定義された「ユーザ情報取得メソッド」を呼び出す

---

## ViewModel

### 1. 役割

- `View`がUIを表示するために必要なデータを取得し、`View`が使いやすい形で準備する
  - > 例) `Repository`からユーザ情報(Userクラス)を取得し、ユーザー名(user.name)のみを`View`に渡す
- `View`から送られてきた値を保存するためのメソッドを呼ぶ
  - > 例) 入力されてきたテキストをもとに、Userクラスのインスタンスを作成し、それを保存する

### 2. Repositoryとの関係性

- モデルクラスに落とし込んで整えられたデータの取得/保存を`Repository`に委任する
  - > 例) `Repository`のユーザ情報(Userクラス)取得/保存メソッドを呼ぶ

---

## Repository

- `Repository`は`ViewModel`に含まれる場合もある
- `Repository`を設置することで、`ViewModel`の負担を減らすことができる
- `Model`からのデータ取得を`Repository`に全て委任することで、`Repository`がデータの取得先を変更しても、`ViewModel`を変更する必要がなくなる

### 1. 役割

- データの取得方法・保存方法を把握
  - > 例) ユーザ情報の取得先はリモートのDB  
  そのデータをローカルのDBに保存する  
  リモートでユーザ情報が更新されれば随時読み込んでローカルのDBに保存  
  ローカルのDBに対象ユーザのアカウントが存在する場合、リモートではなくローカルのデータを取得する  
- アプリ内で扱いやすいように整えられたAPIを提供
  - > 例) jsonファイルから得られたレスポンスを、UserクラスやUserクラスのコンストラクタの型に当てはめて、データを取得する

### 2. Modelとの関係性

- `Model`からデータを取得する

---

## Model

- データを実体として保存しているコンポーネント

### 1. 役割

- データを永続化する
  - > 例) ユーザ情報を実体として永続的に保存する

### 2. DBとの関係性

- Roomライブラリでは、DAOを通してDBにデータを挿入、取得する
  - > 例) Userクラスで実体化されたデータを、DBの使用に合わせて保存する  
  逆に、DBからデータを読み込みUserクラスとして取得する