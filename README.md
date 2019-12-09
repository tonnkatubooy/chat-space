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