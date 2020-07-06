# チャット形式のアプリケーション（carriewaveによる画像投稿可能)

![image](https://user-images.githubusercontent.com/58540888/83344285-923d9d00-a33f-11ea-9e3d-2c8503170edf.png)

## 開発環境
- Ruby on Rails(5.2.3)
- My SQL 
- JavaScript
- jQuery
- AWS
- Github

## 実装機能


## 実装に苦労した点
- メッセージを各ユーザーが投稿できるが、非同期でメッセージを表示させることに苦労した。（jsの理解が甘かった)
- データーベースの設計が当初理解できておらず、外部キー制約、一意性といった部分に困難を感じた。
- 同じくjs関連での実装だが、インクリメンタルサーチを使ったユーザー検索機能にも大変苦戦した。
- メンターから指摘を受けたが、コントローラの共通処理や、ビューのテンプレート化ができていなかった（改善済み）
- テストが書けていないのが心残り。この時点ではそもそもテストがどんな役割を持っているか理解できていなかった。
- AWSというツールを初めて触ったが、深掘りができなかった。

# DB設計

## group_users table

|Column|Type|Options|
|------|----|-------|
|user_id|reference|null: false, foreign_key: true|
|group_id|reference|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user

## messages table
|Column|Type|Options|
|------|----|-------|
|body|text|---------|
|image|string|------|
|user_id|reference|null :false, foreign_key :true|
|group_id|reference|null :false, foreign_key :true|

### Association
- belongs_to :group
- belongs_to :user

## users table
|Column|Type|Options|
|------|----|-------|
|name|string|null :false, unique :true|
|email|string|null :false, unique :true|

### Association
- has_many :messages
- has_many :groups_users
- has_many :groups, through::groups_users

## groups table
|Column|Type|Options|
|------|----|-------|
|name|string|null :false, unique :true, index|

### Association
- has_many :messages
- has_many :groups_users
- has_many :users through::groups_users
