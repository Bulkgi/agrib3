# アプリ名
Agrib

# 概要
農産物の提供に特化したフリーマーケットアプリです。
農家の方が生産した農作物を気軽に出品でき、消費者の方は選択した農作物を購入できます。また、購入した農作物の生産者の顔も確認できるため、農家の方は市場拡大ができ、消費者はどこでも新鮮農作物を購入できることの二つを目的としています。

# 本番環境
URL: 

## ログイン情報(テスト用)
 - BasicID:
 - Pass:
 - Eメール: 
 - パスワード:

# 制作背景(意図)
　前職で、新型コロナウイルスの影響で、農作物の売り上げが著しく低下して、農家の方の生活が苦しくなっている現状を知りました。
　朝早くから10aはあろうかという圃場一面の白菜を収穫している農家さんは５キロあたりの単価が100円減少し、どうにかならんものかと悲痛な言葉を口にしておられました。また、多くの農家さんが来年度の水稲の単価もどこまで下がるか分からないような状況に不安を覚えていらっしゃいました。
　農業はお年寄りが多く、生産は可能でも、出荷に関しては卸売にほとんど任せていることが多く、販売に関して市場の拡大ができないのも農家さんの生活を苦しめている原因ではないかと考えました。そこで、農作物を専門とした、手軽に自身の作物を出品できるアプリケーションを作成す流ことを思いつきました。
　このアプリのメリットは3つあると考えています。
　1つ目は農家の方の情報を出品した農作物と一緒に提示することで、ご購入された消費者の方に知ってもらえるということです。
　２つ目は、消費者の方も高品質で美味しい新鮮な作物をご自宅にいるだけで購入でき、生産者の顔も確認できるため、安全も担保できるということです。
　農家の方を中心に考えたアプリでしたが、消費者の方にもメリットがある、winwinなアプリだと思います。

# DEMO



# 今後実装したい機能
 - ログイン、新規登録機能
 - 商品出品機能
 - 商品詳細機能
 - 商品削除機能
 - マイページ機能
 - 購入機能
 - コメント機能
 - SNS承認機能

 
# データベース設計
## usersテーブル

  |Column             |Type Option | Options                  |
  |------------------ |------------|------------------------- |
  |nickname           | string     | null: false              |
  |email              | string     | null: false unique: true |
  |encrypted_password | string     | null: false              |
  |first_name         | string     | null: false              |
  |last_name          | string     | null: false              |
  |first_name_ruby    | string     | null: false              |
  |last_name_ruby     | string     | null: false              |
  |birth_day          | date       | null: false              |
  

### Association
 -  has_many :orders



## ordersテーブル

  |Column             |Type Option  | Options                         |
  |------------------ |-------------|-------------------------------- |
  |product            | references  | null: false, foreign_key: true  |
  |user               | references  | null: false, foreign_key: true  |
  

  

### Association
 -  belongs_to :product
 -  belongs_to :user
 -  has_one    :addresses




 ### addressesテーブル

 | Column        | Type Option | Options                        |
 | ------------- | ----------- | ------------------------------ |
 | postal_code   | string      | null: false                    | 
 | prefecture_id | integer     | null: false                    |
 | address       | string      | null: false                    |
 | building      | string      |                                |
 | phone         | string      | null: false                    |
 | order         | references  | null: false, foreign_key: true |

### Association
 - belongs_to :order


 ### farmer_usersテーブル

 | Column             | Type Option | Options                  |
 | ------------------ | ----------- | ------------------------ |
 | name               | string      | null: false              |
 | name_ruby          | string      | null: false              |
 | from               | string      | null: false              |
 | farm_name          | string      |                          |
 | email              | string      | null: false unique: true |
 | encrypted_password | string      | null: false              |
 | introduction       | text        | null: false              |
 

### Association
 - has_many :products
 - has_many :comments


 ### productsテーブル

 | Column      | Type Option | Options                        |
 | ----------- | ----------- | ------------------------------ |
 | product     | string      | null: false                    |
 | description | text        | null: false                    |
 | price       | integer     | null: false                    |
 | amount      | integer     | null: false                    |
 | unit_id     | integer     | null: false                    |
 | farmer_user | references  | null: false, foreign_key: true |

 ### Association
 - belongs_to :farmer_user
 - has_many :comments
 - has_one :order


### commentsテーブル

 | Column      | Type Option | Options                        |
 | ----------- | ----------- | ------------------------------ |
 | comment     | string      | null: false                    |
 | product     | references  | null: false, foreign_key: true |
 | farmer_user | references  | null: false, foreign_key: true |

 ### Association
 - belongs_to :farmer_user
 - belongs_to :product
