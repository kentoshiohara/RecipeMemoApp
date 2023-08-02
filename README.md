## アプリケーション名
Recipe Memo

## アプリケーション概要
レシピの登録、編集、更新、削除を行えるメモアプリ

## アプリケーションを作成した背景
料理をする都度、冷蔵庫の中の材料を確認して、その材料で作れるレシピをググっているが、レシピサイトが数多く存在していて作るものを見つけるのに時間がかかる。
お気に入りのレシピをブックマークしても、冷蔵庫の中にある材料で作れるかどうかは一目で確認できないため、お気に入りのレシピをまとめて検索、管理できるアプリがあれば
それらの手間を省くことができると考えたためです。
また、CRUD機能を盛り込んだアプリを開発することで、Laravelの基礎的な構文を理解する為にこのアプリを作成しました。

## 洗い出した要件
[要件定義シート](https://docs.google.com/spreadsheets/d/1k_HfhNildvtE2nmj8IILHJtEignsNJj2mvZuSAlQf0Q/edit#gid=113521568)

## 実装した機能についての画像やGIF
- ユーザー管理機能
  - ユーザー新規登録画面
[![Image from Gyazo](https://i.gyazo.com/b6adbf95332f3198328a76309fa6a5be.gif)](https://gyazo.com/b6adbf95332f3198328a76309fa6a5be)
  - ユーザーログイン画面
[![Image from Gyazo](https://i.gyazo.com/8cf2cd71af28613e9bbddd56ad202941.gif)](https://gyazo.com/8cf2cd71af28613e9bbddd56ad202941)

- レシピ一覧機能
[![Image from Gyazo](https://i.gyazo.com/b6a2f51bf302b476578c7286c86bbc00.gif)](https://gyazo.com/b6a2f51bf302b476578c7286c86bbc00)

- レシピ登録機能
[![Image from Gyazo](https://i.gyazo.com/c6fe372fb68786735d6e13f3e62175cd.gif)](https://gyazo.com/c6fe372fb68786735d6e13f3e62175cd)

- レシピ削除機能
[![Image from Gyazo](https://i.gyazo.com/a97eda829d8ed9fcb7b9633e2133755d.gif)](https://gyazo.com/a97eda829d8ed9fcb7b9633e2133755d)

- 材料登録機能
[![Image from Gyazo](https://i.gyazo.com/f4af8efd8941e112cc4fbf3d54287d2a.gif)](https://gyazo.com/f4af8efd8941e112cc4fbf3d54287d2a)


## データベース設計
[![Image from Gyazo](https://i.gyazo.com/500af20fb23d3e7fce3a305061111334.png)](https://gyazo.com/500af20fb23d3e7fce3a305061111334)

## 画面遷移図
[![Image from Gyazo](https://i.gyazo.com/0e2f7c156dc60659d7983b35d136522d.png)](https://gyazo.com/0e2f7c156dc60659d7983b35d136522d)

## 開発環境
- フロントエンド：HTML&CSS / JavaScript
- バックエンド：PHP / Laravel
- インフラ：Docker
- テスト：RSpec
- テキストエディタ：Visual Studio Code
- タスク管理：github

## 単体テスト
[単体テスト](https://docs.google.com/spreadsheets/d/187SWW7xIxMeRcOsH3XWQ1abtCAw_pp-KC4k7mpfplb8/edit#gid=2056348641)

## 結合テスト
[結合テスト](https://docs.google.com/spreadsheets/d/1dwBHz6Grukjv0iCGeJH38pPb34ptBHpfZ0a5LW4UXPM/edit#gid=2092012291)

## ローカルでの動作方法
以下のコマンドを順に実行
% git clone https://github.com/kentoshiohara/random_trip.git
% cd xxxxxx
% bundle install
% yarn install

## テーブル設計

## users テーブル

| Column                | Type       | Options                  |
| --------------------- | ---------- | ------------------------ |
| id                    | int        | primary key              |
| name                  | string(20) | not null: false          |
| kana                  | string(20) | not null: false          |
| email                 | string(50) | not null, unique: true   |
| payment               | tinyint    | not null                 |
| created_at            | datetime   |                          |
| updated_at            | datetime   |                          |

### Association
- has_many :recipes

## recipes テーブル
| Column                | Type         | Options                  |
| --------------------- | ------------ | ------------------------ |
| id                    | int          | primary key              |
| name                  | string(100)  | not null                 |
| link                  | string(2084) | nullable                 |
| rating                | tinyint      |                          |
| status                | tinyint      | not null                 |
| comment               | text         |                          |
| created_at            | datetime     |                          |
| user_id               | references   |                          |

### Association
- belongs_to :user
- has_many :ingredients, through :ingredient_recipe

## ingredientsテーブル
| Column                | Type        | Options           |
| --------------------- | ----------- | ----------------- |
| id                    | int         | primary key       |
| name                  | string(100) |                   |

### Association
- has_many :recipes, through :ingredient_recipe

## ingredient_recipeテーブル
| Column               | Type       | Options           |
| -------------------- | ---------- | ----------------- |
| id                   |            | primary key       |
| recipe_id            | references | not null          |
| ingredient_id        | references | not null          |

### Association
- belongs_to :recipe
- belongs_to :ingredient
